# Technical Documentation

## Project Overview

This document provides technical details about the portfolio website implementation, including architecture decisions, component descriptions, and implementation notes.

## Architecture

### File Structure

```
assignment-1/
├── index.html          # Single-page application entry point
├── css/
│   └── styles.css      # All styles including themes and responsive design
├── js/
│   └── script.js       # Client-side functionality
├── assets/
│   └── images/         # Static assets
└── docs/               # Documentation
```

### Design Decisions

1. **Single Page Application (SPA) Approach**
   - All content on one page with section navigation
   - Smooth scrolling between sections
   - Reduces HTTP requests and improves load time

2. **No External Dependencies**
   - Built with vanilla HTML, CSS, and JavaScript
   - No CSS frameworks (Bootstrap, Tailwind) or JS libraries
   - Ensures fast loading and full control over code

3. **CSS Custom Properties for Theming**
   - Centralized color and spacing values
   - Easy theme switching (light/dark)
   - Maintainable and scalable styling

## Component Documentation

### HTML Structure (`index.html`)

#### Sections

| Section | ID | Description |
|---------|-----|-------------|
| Navigation | `.navbar` | Fixed top navigation with links, theme toggle, and mobile menu |
| Hero | `#home` | Landing section with animated background, typing effect, and CTAs |
| About | `#about` | Personal introduction with profile placeholder and info cards |
| Skills | `#skills` | Technical skills displayed in categorized grid cards |
| Experience | `#experience` | Timeline-style education, experience, and certifications |
| Projects | `#projects` | Portfolio project showcase with 6 projects (1 featured) |
| Contact | `#contact` | Contact information and form with validation |
| Footer | `.footer` | Brand info, quick links, and copyright |

#### Semantic Elements Used

- `<nav>` - Navigation bar
- `<header>` - Hero section
- `<section>` - Content sections
- `<article>` - Project cards
- `<footer>` - Page footer
- `<form>` - Contact form

### CSS Architecture (`css/styles.css`)

#### Custom Properties (CSS Variables)

```css
:root {
    /* Colors */
    --bg-primary: #ffffff;
    --bg-secondary: #f8f9fa;
    --text-primary: #212529;
    --accent-color: #4a90a4;

    /* Spacing */
    --spacing-sm: 1rem;
    --spacing-md: 2rem;
    --spacing-lg: 3rem;

    /* Other */
    --transition-speed: 0.3s;
}
```

#### Dark Theme Implementation

Theme is applied via `data-theme` attribute on `<html>`:

```css
[data-theme="dark"] {
    --bg-primary: #1a1a2e;
    --text-primary: #eaeaea;
    /* ... other overrides */
}
```

#### Responsive Breakpoints

| Breakpoint | Target Devices |
|------------|----------------|
| `> 768px` | Desktop and tablets (landscape) |
| `<= 768px` | Tablets (portrait) and large phones |
| `<= 480px` | Small mobile devices |

#### Layout Systems

1. **Flexbox** - Used for:
   - Navigation alignment
   - Centering content
   - Card content layout
   - Timeline items

2. **CSS Grid** - Used for:
   - Skills card grid (3 categories)
   - Projects card grid (featured card spans 2 columns)
   - Certifications grid
   - Contact section layout
   - Timeline container (2-column on desktop)

#### Animations & Effects

| Animation | Description |
|-----------|-------------|
| `float` | Animated gradient shapes in hero background |
| `pulse` | Hero avatar glow pulsing effect |
| `fadeInUp` | Elements fade in and slide up on load |
| `blink` | Typing cursor blinking animation |
| `scroll` | Scroll indicator animation |
| `slideDown` | Notification slide-in animation |

#### Gradient Colors

Six unique gradients for project cards:
- `gradient-1`: Purple to violet
- `gradient-2`: Pink to red
- `gradient-3`: Blue to cyan
- `gradient-4`: Green to teal
- `gradient-5`: Pink to yellow
- `gradient-6`: Teal to pink

### JavaScript Functionality (`js/script.js`)

#### Functions

| Function | Purpose |
|----------|---------|
| `initThemeToggle()` | Sets up dark/light theme toggle with localStorage persistence |
| `initMobileNav()` | Handles mobile hamburger menu with animations |
| `initContactForm()` | Form validation, submission handling, and loading states |
| `initTypingEffect()` | Creates animated typing effect in hero tagline |
| `initScrollAnimations()` | Triggers fade-in animations when elements enter viewport |
| `initScrollToTop()` | Shows/hides scroll-to-top button based on scroll position |
| `initActiveNavHighlight()` | Updates active nav link based on current section |
| `isValidEmail()` | Validates email format using regex |
| `showNotification()` | Displays success/error notification messages |

#### Theme Toggle Implementation

```javascript
// Check saved preference
const savedTheme = localStorage.getItem('theme') || 'light';
document.documentElement.setAttribute('data-theme', savedTheme);

// Toggle on click
themeToggle.addEventListener('click', function() {
    const currentTheme = document.documentElement.getAttribute('data-theme');
    const newTheme = currentTheme === 'dark' ? 'light' : 'dark';
    document.documentElement.setAttribute('data-theme', newTheme);
    localStorage.setItem('theme', newTheme);
});
```

#### Form Validation

- Required field checking
- Email format validation using regex
- Visual feedback via notifications

## Performance Considerations

### Optimizations Implemented

1. **Minimal HTTP Requests**
   - Single CSS file
   - Single JavaScript file
   - No external fonts or libraries

2. **CSS Efficiency**
   - Using CSS custom properties (parsed once)
   - Efficient selectors
   - Minimal specificity conflicts

3. **JavaScript**
   - Event delegation where appropriate
   - DOM queries cached in variables
   - Deferred script loading (at end of body)

### Loading Strategy

```html
<!-- CSS in head for render-blocking (intentional) -->
<link rel="stylesheet" href="css/styles.css">

<!-- JS at end of body for non-blocking -->
<script src="js/script.js"></script>
```

## Accessibility Features

1. **Semantic HTML**
   - Proper heading hierarchy (h1 > h2 > h3)
   - Landmark elements (nav, main, footer)
   - Form labels associated with inputs

2. **ARIA Attributes**
   - `aria-label` on icon buttons
   - Meaningful link text

3. **Keyboard Navigation**
   - All interactive elements focusable
   - Visible focus states
   - Logical tab order

4. **Color Contrast**
   - Text colors meet WCAG contrast requirements
   - Both light and dark themes accessible

## Browser Compatibility

### Supported Browsers

- Chrome 80+
- Firefox 75+
- Safari 13+
- Edge 80+

### CSS Features Used

| Feature | Support |
|---------|---------|
| CSS Custom Properties | IE11 not supported, all modern browsers |
| CSS Grid | Widely supported |
| Flexbox | Widely supported |
| `scroll-behavior: smooth` | Most modern browsers |

## Testing

### Manual Testing Checklist

- [ ] All navigation links work correctly
- [ ] Theme toggle persists across page refreshes
- [ ] Mobile menu opens and closes properly
- [ ] Form validation shows appropriate messages
- [ ] Responsive design works at all breakpoints
- [ ] All content is readable in both themes
- [ ] Typing effect cycles through all phrases
- [ ] Scroll animations trigger when scrolling
- [ ] Active nav link updates when scrolling sections
- [ ] Scroll-to-top button appears after scrolling down
- [ ] Timeline displays correctly on all screen sizes
- [ ] Project cards hover effects work properly

### Browser Testing

Test in the following browsers:
1. Google Chrome (Desktop & Mobile)
2. Mozilla Firefox
3. Microsoft Edge
4. Safari (if available)

### Responsive Testing

Use browser DevTools to test at:
- 1920px (Large desktop)
- 1366px (Laptop)
- 768px (Tablet)
- 375px (Mobile)

## Future Improvements

Potential enhancements for future versions:

1. **Backend Integration**
   - Connect contact form to email service
   - Add form submission confirmation

2. **Additional Features**
   - Blog section
   - Downloadable resume
   - Project filtering/sorting

3. **Performance**
   - Image optimization
   - Lazy loading for images
   - Service worker for offline support

4. **Accessibility**
   - Skip navigation link
   - Reduced motion preference support
   - Screen reader testing
