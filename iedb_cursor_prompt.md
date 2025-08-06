# IEDB WordPress Plugin - Development Brief for Cursor

## Instructions for Cursor

This is a **BRAND NEW PROJECT**. Build everything from scratch following the specifications below. 

**Key Points:**
1. Use `IEDB`/`iedb` naming throughout
2. Start with Phase 1 priorities and build incrementally
3. Follow WordPress coding standards and security best practices
4. Test each feature thoroughly before moving to next phase
5. Document all code with comprehensive comments and headers
6. Build a professional entertainment database plugin that rivals premium solutions

---

## Project Overview

**Plugin Name:** IEDB (Inquiral Entertainment Database)  
**Purpose:** WordPress plugin for managing movies, TV shows, and cast/crew with TMDB API integration  
**Current Status:** NEW PROJECT - Build from scratch  
**Target User:** Entertainment websites, movie databases, streaming platforms  

## Project Requirements

### Core Functionality Needed
- Custom post types for movies, TV shows, and people
- TMDB API integration for content import
- Admin interface for content management
- Frontend templates for content display
- Search and filtering capabilities
- Image management and galleries

### Naming Convention
**CRITICAL:** Everything should use `IEDB` or `iedb` prefix:
- Constants: `IEDB_VERSION`, `IEDB_PLUGIN_DIR`
- Classes: `class IEDB_Movies`, `class IEDB_API`
- Functions: `iedb_get_movie()`, `iedb_format_date()`
- Post types: `iedb_movie`, `iedb_tv_show`, `iedb_person`
- Meta fields: `_iedb_tmdb_id`, `_iedb_rating`
- CSS classes: `.iedb-movie-card`, `.iedb-rating`

## Required File Structure

```
iedb/
├── iedb.php                                   ← Main plugin file
├── includes/
│   ├── class-iedb-post-types.php             ← Custom post types
│   ├── class-iedb-tmdb-api.php               ← TMDB API integration
│   ├── class-iedb-importer.php               ← Content importer
│   ├── class-iedb-movies.php                 ← Movie functionality
│   ├── class-iedb-tv-shows.php               ← TV show functionality
│   ├── class-iedb-cast.php                   ← Cast/crew functionality
│   ├── class-iedb-cron.php                   ← Automated sync jobs
│   ├── class-iedb-shortcodes.php             ← Shortcode handlers
│   └── iedb-functions.php                    ← Helper functions
├── admin/
│   ├── class-iedb-admin.php                  ← Admin enhancements
│   ├── class-iedb-settings.php               ← Settings page
│   ├── class-iedb-import-page.php            ← Import interface
│   └── views/
│       ├── dashboard.php                     ← Dashboard template
│       └── meta-boxes/
│           ├── movie-details.php             ← Movie meta box
│           ├── tv-show-details.php           ← TV show meta box
│           ├── person-details.php            ← Person meta box
│           └── tmdb-sync.php                 ← Sync meta box
├── blocks/                                    ← Gutenberg blocks
│   ├── src/
│   │   ├── movie-card/
│   │   │   ├── index.js                      ← Movie card block
│   │   │   ├── edit.js                       ← Block editor
│   │   │   └── save.js                       ← Block output
│   │   ├── movies-grid/
│   │   │   ├── index.js                      ← Movies grid block
│   │   │   ├── edit.js
│   │   │   └── save.js
│   │   ├── tv-show-card/
│   │   ├── cast-list/
│   │   └── search-form/
│   ├── build/                                ← Compiled blocks
│   └── blocks.php                            ← Block registration
├── assets/
│   ├── css/
│   │   ├── admin.css                         ← Admin styles
│   │   ├── design-system.css                 ← Core design system variables
│   │   ├── components.css                    ← Reusable UI components
│   │   ├── frontend.css                      ← Frontend layout styles
│   │   ├── blocks.css                        ← Gutenberg block styles
│   │   ├── movies.css                        ← Movie-specific styles
│   │   ├── tv-shows.css                      ← TV show styles
│   │   ├── cast.css                          ← Person/cast styles
│   │   └── themes/
│   │       ├── dark.css                      ← Dark theme (default)
│   │       └── light.css                     ← Light theme option
│   ├── js/
│   │   ├── admin.js                          ← Admin scripts
│   │   ├── frontend.js                       ← Frontend scripts
│   │   ├── blocks.js                         ← Block editor scripts
│   │   ├── theme-switcher.js                 ← Dark/light theme toggle
│   │   ├── movies.js                         ← Movie-specific JS
│   │   ├── tv-shows.js                       ← TV show JS
│   │   └── cast.js                           ← Person/cast JS
│   └── images/
│       ├── placeholder.png                   ← Default poster image
│       ├── no-profile.png                    ← Default profile image
│       ├── icons/                            ← SVG icon set
│       └── branding/                         ← IEDB logos and branding
├── templates/
│   ├── single-iedb_movie.php                 ← Single movie template
│   ├── single-iedb_tv_show.php               ← Single TV show template
│   ├── single-iedb_person.php                ← Single person template
│   ├── archive-iedb_movie.php                ← Movies archive
│   ├── archive-iedb_tv_show.php              ← TV shows archive
│   └── archive-iedb_person.php               ← People archive
├── widgets/
│   ├── class-iedb-recent-movies.php          ← Recent movies widget
│   └── class-iedb-popular-shows.php          ← Popular shows widget
├── languages/
│   └── iedb.pot                               ← Translation template
├── package.json                               ← NPM dependencies for blocks
├── webpack.config.js                          ← Webpack config for blocks
└── .babelrc                                   ← Babel config for blocks
```

## Post Types & Database Schema

### Custom Post Types
```php
// Movies
iedb_movie (slug: movies)

// TV Shows  
iedb_tv_show (slug: tv-shows)

// People (Cast & Crew)
iedb_person (slug: cast)
```

### Taxonomies
```php
// Genres (for movies and TV shows)
iedb_genre

// Content Ratings (G, PG, R, etc.)
iedb_rating

// Production Status (released, in production, etc.)
iedb_status
```

### Meta Fields

#### Movies (`iedb_movie`)
```php
_iedb_tmdb_id           // TMDB movie ID
_iedb_imdb_id           // IMDB movie ID
_iedb_release_date      // Release date (Y-m-d)
_iedb_runtime           // Runtime in minutes
_iedb_tmdb_rating       // TMDB rating (0-10)
_iedb_vote_count        // Number of votes
_iedb_popularity        // TMDB popularity score
_iedb_budget            // Production budget
_iedb_revenue           // Box office revenue
_iedb_status            // Production status
_iedb_tagline           // Movie tagline
_iedb_homepage          // Official website
_iedb_adult             // Adult content flag
_iedb_original_language // Original language
_iedb_original_title    // Original title
_iedb_cast              // Cast members (serialized)
_iedb_crew              // Crew members (serialized)
_iedb_gallery           // Image gallery (serialized)
_iedb_videos            // Trailers/videos (serialized)
_iedb_similar           // Similar movies (array of IDs)
_iedb_recommendations   // Recommended movies (array of IDs)
```

#### TV Shows (`iedb_tv_show`)
```php
_iedb_tmdb_id              // TMDB show ID
_iedb_original_name        // Original show name
_iedb_first_air_date       // First air date
_iedb_last_air_date        // Last air date
_iedb_episode_runtime      // Episode runtime array
_iedb_tmdb_rating          // TMDB rating (0-10)
_iedb_vote_count           // Number of votes
_iedb_popularity           // TMDB popularity score
_iedb_number_of_episodes   // Total episodes
_iedb_number_of_seasons    // Total seasons
_iedb_status               // Show status (returning, ended, etc.)
_iedb_type                 // Show type (scripted, reality, etc.)
_iedb_homepage             // Official website
_iedb_in_production        // Currently in production flag
_iedb_original_language    // Original language
_iedb_origin_country       // Countries of origin
_iedb_networks             // Broadcasting networks (serialized)
_iedb_production_companies // Production companies (serialized)
_iedb_seasons              // Season details (serialized)
_iedb_created_by           // Show creators (serialized)
_iedb_cast                 // Cast members (serialized)
_iedb_crew                 // Crew members (serialized)
_iedb_gallery              // Image gallery (serialized)
_iedb_videos               // Trailers/videos (serialized)
```

#### People (`iedb_person`)
```php
_iedb_tmdb_id              // TMDB person ID
_iedb_imdb_id              // IMDB person ID
_iedb_birthday             // Birth date
_iedb_deathday             // Death date (if applicable)
_iedb_place_of_birth       // Birth location
_iedb_known_for_department // Primary profession
_iedb_gender               // Gender (1=female, 2=male, 3=non-binary)
_iedb_popularity           // TMDB popularity score
_iedb_adult                // Adult content performer flag
_iedb_also_known_as        // Alternative names (serialized)
_iedb_homepage             // Official website
_iedb_movie_credits        // Movie appearances (serialized)
_iedb_tv_credits           // TV appearances (serialized)
```

## TMDB API Integration

### API Configuration
- Base URL: `https://api.themoviedb.org/3/`
- Images: `https://image.tmdb.org/t/p/`
- Rate Limit: 40 requests per 10 seconds
- API Key: Required (free from themoviedb.org)

### Required API Methods
```php
class IEDB_TMDB_API {
    // Search methods
    search_movies($query, $page = 1)
    search_tv_shows($query, $page = 1)
    search_people($query, $page = 1)
    
    // Detail methods
    get_movie_details($movie_id)
    get_tv_show_details($tv_id)
    get_person_details($person_id)
    
    // Popular/Trending
    get_popular_movies($page = 1)
    get_popular_tv_shows($page = 1)
    get_trending($media_type, $time_window)
    
    // Utility methods
    get_configuration()
    get_movie_genres()
    get_tv_genres()
    get_image_url($file_path, $size)
    download_image($file_path, $size, $post_id)
    test_connection()
}
```

## Admin Interface Requirements

### Main Menu Structure
```
IEDB (main menu)
├── Dashboard           (overview with statistics)
├── Movies             (edit.php?post_type=iedb_movie)
├── TV Shows           (edit.php?post_type=iedb_tv_show)
├── Cast & Crew        (edit.php?post_type=iedb_person)
├── Import/Sync        (custom page for TMDB import)
└── Settings           (plugin settings)
```

### Dashboard Features
- Content statistics (total movies, shows, people)
- Recent imports
- TMDB API status
- Sync status and controls
- Quick action buttons

### Settings Page
- TMDB API key configuration
- Auto-sync settings (interval, enabled/disabled)
- Import settings (content types, limits)
- Image settings (download locally, sizes)
- Advanced options

### Import/Sync Page
- Search TMDB and import individual items
- Bulk import popular/trending content
- Sync existing content with TMDB
- Import history and logs

## Frontend Requirements

### Single Post Templates
- Movie detail pages with full information
- TV show pages with season/episode details
- Person profile pages with filmography
- Responsive design for all devices
- SEO-optimized markup

### Archive Templates
- Movie listings with filtering
- TV show listings with filtering
- People listings with search
- Pagination and sorting options

### Shortcodes System
```php
// Listing Shortcodes
[iedb_movies limit="12" genre="action" orderby="rating"]
[iedb_tv_shows limit="8" status="returning"]
[iedb_people limit="6" department="acting"]

// Single Display Shortcodes (ScreenRant-style)
[iedb_movie_card id="123"]                    // Full movie card with poster, details
[iedb_tv_card id="456"]                       // Full TV show card
[iedb_person_card id="789"]                   // Person profile card

// Content Components
[iedb_poster id="123" size="large"]           // Movie/show poster
[iedb_rating id="123" source="tmdb"]          // TMDB rating display (8.6/10) - READ ONLY
[iedb_genres id="123"]                        // Genre tags (R, Horror, Thriller)
[iedb_cast movie_id="456" limit="10"]         // Cast list with photos
[iedb_crew movie_id="456" department="directing"] // Crew by department
[iedb_details id="123"]                       // Release date, runtime, director, etc.
[iedb_similar content_id="789" limit="6"]     // Similar content grid
[iedb_trailer id="123"]                       // Embedded trailer player
[iedb_gallery id="123" type="stills"]         // Image gallery

// Interactive Elements (NO rating buttons)
[iedb_watchlist_button id="123"]              // Add to watchlist (if implemented)
[iedb_share_buttons id="123"]                 // Social sharing
[iedb_search form="advanced"]                 // Search form
[iedb_view_details id="123"]                  // "View Details" button to single page
```

### Gutenberg Blocks System
**Location:** `blocks/`

#### Required Blocks
```javascript
// Movie/TV Show Blocks
iedb/movie-card           // Single movie display block
iedb/tv-show-card         // Single TV show display block
iedb/person-card          // Person profile block

// Listing Blocks  
iedb/movies-grid          // Movies grid with filters
iedb/tv-shows-grid        // TV shows grid with filters
iedb/people-grid          // Cast/crew grid

// Component Blocks
iedb/poster               // Poster image block
iedb/cast-list            // Cast members list
iedb/similar-content      // Similar movies/shows
iedb/content-details      // Release date, runtime, etc.
iedb/trailer              // Video trailer embed

// Advanced Blocks
iedb/search-form          // Advanced search
iedb/featured-slider      // Hero slider for featured content
iedb/genre-filter         // Genre filtering interface
```

#### Block Features
- **Live Preview** in editor
- **Responsive controls** (mobile, tablet, desktop)
- **Style variations** (card, list, grid layouts)
- **Color scheme** options
- **Typography** controls
- **Spacing** controls
- **Filter options** (genre, year, rating)
- **Animation** options (fade, slide)

#### Block Categories
```javascript
// Custom block category
wp.blocks.registerBlockType('iedb/movie-card', {
    category: 'iedb-blocks',
    title: 'Movie Card',
    description: 'Display a single movie with poster and details',
    // ... block configuration
});
```

### Widget System
- Recent Movies Widget
- Popular TV Shows Widget
- Featured Person Widget
- Random Content Widget

## Design System & UI/UX Approach

### **Standalone Design System**
IEDB uses a **completely independent design system** that maintains consistent branding and professional appearance regardless of the active WordPress theme.

#### Design Philosophy
- **Entertainment-focused aesthetics** (Netflix, IMDb, ScreenRant inspired)
- **Dark theme by default** with light theme option
- **Image-first design** - posters and backdrops are heroes
- **Card-based layouts** for all content types
- **Professional typography** independent of theme fonts
- **Responsive-first** approach for all devices

#### CSS Architecture
```css
/* CSS Custom Properties for easy theming */
:root {
  /* Brand Colors */
  --iedb-primary: #e50914;        /* Netflix red */
  --iedb-secondary: #0f79af;      /* TMDB blue */
  --iedb-accent: #f5c518;         /* IMDb gold */
  
  /* Dark Theme (default) */
  --iedb-bg-primary: #0d1117;     /* GitHub dark */
  --iedb-bg-secondary: #161b22;   /* Card backgrounds */
  --iedb-bg-tertiary: #21262d;    /* Elevated surfaces */
  
  /* Text Colors */
  --iedb-text-primary: #f0f6fc;   /* Primary text */
  --iedb-text-secondary: #8b949e; /* Secondary text */
  --iedb-text-muted: #6e7681;     /* Muted text */
  
  /* Interactive Elements */
  --iedb-border: #30363d;         /* Borders */
  --iedb-hover: #1f6feb;          /* Hover states */
  --iedb-focus: #388bfd;          /* Focus states */
  
  /* Typography */
  --iedb-font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  --iedb-font-mono: 'SF Mono', Monaco, 'Cascadia Code', monospace;
  
  /* Spacing Scale */
  --iedb-space-xs: 0.25rem;   /* 4px */
  --iedb-space-sm: 0.5rem;    /* 8px */
  --iedb-space-md: 1rem;      /* 16px */
  --iedb-space-lg: 1.5rem;    /* 24px */
  --iedb-space-xl: 2rem;      /* 32px */
  --iedb-space-2xl: 3rem;     /* 48px */
  
  /* Border Radius */
  --iedb-radius-sm: 4px;
  --iedb-radius-md: 8px;
  --iedb-radius-lg: 12px;
  --iedb-radius-xl: 16px;
  
  /* Shadows */
  --iedb-shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
  --iedb-shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
  --iedb-shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1);
  --iedb-shadow-xl: 0 20px 25px rgba(0, 0, 0, 0.15);
}

/* Light Theme Override */
[data-iedb-theme="light"] {
  --iedb-bg-primary: #ffffff;
  --iedb-bg-secondary: #f6f8fa;
  --iedb-bg-tertiary: #f1f3f4;
  --iedb-text-primary: #1f2328;
  --iedb-text-secondary: #656d76;
  --iedb-text-muted: #8c959f;
  --iedb-border: #d1d9e0;
}
```

#### Component Structure
```css
/* Base Component Classes */
.iedb-card { /* Movie/TV/Person cards */ }
.iedb-grid { /* Responsive grid layouts */ }
.iedb-poster { /* Poster image component */ }
.iedb-rating { /* Rating display component */ }
.iedb-badge { /* Genre tags, status badges */ }
.iedb-button { /* Action buttons */ }
.iedb-modal { /* Popup modals */ }
.iedb-carousel { /* Content sliders */ }
.iedb-form { /* Search forms */ }
.iedb-list { /* Cast/crew lists */ }
```

#### Typography Scale
```css
.iedb-heading-1 { font-size: 2.25rem; font-weight: 800; }  /* 36px */
.iedb-heading-2 { font-size: 1.875rem; font-weight: 700; } /* 30px */
.iedb-heading-3 { font-size: 1.5rem; font-weight: 600; }   /* 24px */
.iedb-heading-4 { font-size: 1.25rem; font-weight: 600; }  /* 20px */
.iedb-body-lg { font-size: 1.125rem; line-height: 1.6; }   /* 18px */
.iedb-body { font-size: 1rem; line-height: 1.5; }          /* 16px */
.iedb-body-sm { font-size: 0.875rem; line-height: 1.4; }   /* 14px */
.iedb-caption { font-size: 0.75rem; line-height: 1.3; }    /* 12px */
```

### Search & Filtering
- Advanced search form
- Filter by genre, year, rating, status
- AJAX-powered results
- Search suggestions/autocomplete

### SEO & Schema Markup
- Movie schema markup
- TV show schema markup
- Person schema markup
- Open Graph meta tags
- Twitter Card support

### Performance Features
- Image lazy loading
- TMDB API response caching
- Database query optimization
- CDN support for images

### REST API Endpoints
```php
/wp-json/iedb/v1/movies
/wp-json/iedb/v1/tv-shows
/wp-json/iedb/v1/people
/wp-json/iedb/v1/search
```

## Development Priorities

### Phase 1: Foundation (Build First)
1. Main plugin file with proper structure
2. Custom post types and taxonomies
3. Basic TMDB API integration
4. Admin menu and dashboard
5. Settings page with API configuration

### Phase 2: Core Features (Build Second)
1. Meta boxes for all post types
2. TMDB import functionality  
3. **Action Scheduler integration** for reliable sync jobs
4. Admin interface styling
5. Content management features

### Phase 3: Content Display & Design (Build Third)
1. **Standalone design system** implementation
2. **CSS component library** with entertainment aesthetics
3. **Template override system** (bypasses theme templates)
4. **Complete schema markup system** (overrides Yoast)
5. Shortcodes system for content display

### Phase 4: Advanced Features (Build Fourth)
1. **Gutenberg blocks** with custom styling (essential for modern WordPress)
2. **Dark/light theme toggle** functionality
3. **Automated sync scheduling** with Action Scheduler
4. Advanced search and filtering with custom styling
5. **Responsive image galleries** and carousels

### Phase 4: Enhancement (Build Fourth)
1. Advanced search and filtering
2. REST API endpoints
3. Performance optimizations
4. User watchlist features
5. Social sharing integration

### Phase 5: Enhanced Features (Build Fifth)
1. **Bulk operations system** (import, edit, delete)
2. **Content relationships** and franchise management
3. **Enhanced taxonomies** (studios, networks, awards)
4. **Smart content scheduling** (publish before release dates)
5. **Advanced filtering** (decade, runtime, rating ranges)

### Phase 6: Integrations & Analytics (Build Sixth)
1. **Multi-source ratings** (IMDb, Rotten Tomatoes, Metacritic)
2. **Enhanced trailer system** with YouTube API
3. **Entertainment-specific analytics** and insights
4. **Social media integration** with custom cards
5. **Performance optimizations** and monitoring

### Phase 7: Monetization & PWA (Build Last)
1. **Affiliate link system** (streaming services)
2. **Advertisement placement** areas
3. **Progressive Web App** features
4. **Advanced SEO** (sitemaps, breadcrumbs)
5. **Performance optimizations** and monitoring

## Code Standards

### WordPress Standards
- Follow WordPress PHP coding standards
- Use WordPress hooks and filters properly
- Sanitize all inputs, escape all outputs
- Use nonces for form security
- Implement proper capability checks

### Plugin Structure
- Use singleton pattern for main plugin class
- Implement proper activation/deactivation hooks
- Use WordPress transients for caching
- Follow plugin development best practices

### Security Requirements
- SQL injection prevention
- XSS protection
- CSRF protection with nonces
- Capability-based access control
- Input validation and sanitization

## Testing Requirements
- Manual testing for all features
- Mobile responsiveness testing
- Browser compatibility testing
- Performance testing with large datasets
- Security testing

---

## Testing Requirements
- Manual testing for all features
- Mobile responsiveness testing
- Browser compatibility testing
- Performance testing with large datasets
- Security testing