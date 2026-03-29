---
name: design-guide
description: Modern UI design system and guidelines for building clean, professional interfaces. Use when creating or modifying any UI components, web pages, React components, HTML/CSS, or visual interfaces. Ensures consistent, modern design with proper spacing, typography, colors, and interaction patterns.
---

# Design Guide

Comprehensive guidelines for creating modern, professional UIs with clean aesthetics and excellent user experience.

## Core Design Principles

**Clean & Minimal**
- Embrace white space—give elements room to breathe
- Remove unnecessary elements and decorations
- Keep layouts uncluttered with clear visual hierarchy

**Neutral Color Palette**
- Base: Grays (#F8F9FA, #E9ECEF, #DEE2E6) and off-whites (#FAFAFA, #FFFFFF)
- ONE accent color used sparingly for CTAs and highlights
- Avoid generic purple/blue gradients
- Use natural, muted tones when color is needed

**Consistent Spacing**
- Use 8px grid system: 8, 16, 24, 32, 48, 64px
- Apply consistently to padding, margins, gaps
- Larger spacing (48px+) between major sections
- Tighter spacing (8-16px) for related elements

**Typography**
- Clear hierarchy with distinct sizes
- Minimum 16px for body text (14px acceptable for secondary text)
- Maximum 2 font families per interface
- Line height: 1.5 for body text, 1.2 for headings
- Use font weight variations (400, 500, 600, 700) for hierarchy

**Subtle Shadows**
- Light, natural shadows: `box-shadow: 0 1px 3px rgba(0,0,0,0.1)`
- Slightly deeper for elevated elements: `0 4px 6px rgba(0,0,0,0.07)`
- Avoid heavy, dark shadows

**Rounded Corners**
- Not everything needs to be rounded
- Standard radius: 6-8px for buttons, cards
- Larger radius (12-16px) for prominent elements
- Use 0 radius for tables, data displays, and formal interfaces

**Interactive States**
- Hover: Subtle brightness or shadow change
- Active: Slight scale reduction or darker shade
- Disabled: 50% opacity with cursor: not-allowed
- Focus: Clear outline or ring (2px, accent color)

**Mobile-First**
- Design for smallest screen first
- Stack elements vertically on mobile
- Ensure touch targets are 44x44px minimum
- Test at 375px width minimum

## Component Patterns

### Buttons

```css
/* Primary Button */
.btn-primary {
  padding: 12px 24px;
  background: #2563EB; /* Accent color */
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  font-weight: 500;
  box-shadow: 0 1px 3px rgba(0,0,0,0.1);
  cursor: pointer;
  transition: all 0.2s;
}

.btn-primary:hover {
  background: #1D4ED8;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}

/* Secondary Button */
.btn-secondary {
  padding: 12px 24px;
  background: white;
  color: #374151;
  border: 1px solid #D1D5DB;
  border-radius: 8px;
  font-size: 16px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-secondary:hover {
  background: #F9FAFB;
  border-color: #9CA3AF;
}
```

### Cards

```css
.card {
  background: white;
  border-radius: 12px;
  padding: 24px;
  box-shadow: 0 1px 3px rgba(0,0,0,0.1);
  transition: box-shadow 0.2s;
}

.card:hover {
  box-shadow: 0 4px 12px rgba(0,0,0,0.08);
}
```

### Forms

```css
.input {
  width: 100%;
  padding: 12px 16px;
  font-size: 16px;
  background: white;
  border: 1px solid #D1D5DB;
  border-radius: 8px;
  transition: border-color 0.2s;
}

.input:focus {
  outline: none;
  border-color: #2563EB;
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
}

.label {
  display: block;
  margin-bottom: 8px;
  font-size: 14px;
  font-weight: 500;
  color: #374151;
}
```

### Layout

```css
/* Container with proper max-width */
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
}

/* Section spacing */
.section {
  padding: 64px 0;
}

/* Grid with consistent gaps */
.grid {
  display: grid;
  gap: 24px;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
}
```

## Color System

**Gray Scale (Primary)**
- `#FFFFFF` - Pure white (backgrounds)
- `#FAFAFA` - Off-white (alternate backgrounds)
- `#F3F4F6` - Very light gray (hover states)
- `#E5E7EB` - Light gray (borders, dividers)
- `#D1D5DB` - Medium gray (borders)
- `#9CA3AF` - Gray (secondary text)
- `#6B7280` - Dark gray (body text)
- `#374151` - Darker gray (headings)
- `#1F2937` - Very dark gray (primary text)

**Accent Color Examples** (pick ONE)
- Blue: `#2563EB` (professional, trustworthy)
- Green: `#059669` (success, growth)
- Indigo: `#4F46E5` (modern, tech)
- Orange: `#EA580C` (energetic, friendly)

## Typography Scale

- **Heading 1**: 48px / 3rem, weight 700
- **Heading 2**: 36px / 2.25rem, weight 600
- **Heading 3**: 28px / 1.75rem, weight 600
- **Heading 4**: 24px / 1.5rem, weight 600
- **Body Large**: 18px / 1.125rem, weight 400
- **Body**: 16px / 1rem, weight 400
- **Body Small**: 14px / 0.875rem, weight 400
- **Caption**: 12px / 0.75rem, weight 400

## Common Mistakes to Avoid

1. **Over-styling**: Don't add gradients, multiple shadows, or excessive effects
2. **Inconsistent spacing**: Stick to the 8px grid system
3. **Too many colors**: Use ONE accent color plus grays
4. **Small text**: Never go below 14px for readable content
5. **Heavy shadows**: Keep shadows subtle and natural
6. **Rounded everything**: Not all elements need border-radius
7. **Missing hover states**: Always provide visual feedback
8. **Cluttered layouts**: Embrace white space

## Responsive Breakpoints

```css
/* Mobile first approach */
.element {
  /* Mobile styles (default) */
}

@media (min-width: 640px) {
  /* Tablet styles */
}

@media (min-width: 1024px) {
  /* Desktop styles */
}

@media (min-width: 1280px) {
  /* Large desktop styles */
}
```

## Accessibility

- Color contrast ratio: 4.5:1 minimum for text
- Touch targets: 44x44px minimum on mobile
- Focus indicators: Clear 2px outline on interactive elements
- Alt text: Always provide for images
- Semantic HTML: Use proper heading hierarchy

## Implementation Checklist

Before finalizing any UI:
- [ ] Uses 8px spacing grid consistently
- [ ] Maximum 2 fonts
- [ ] ONE accent color used sparingly
- [ ] Body text is 16px minimum
- [ ] Buttons have clear hover states
- [ ] Shadows are subtle
- [ ] Layout has adequate white space
- [ ] Mobile-responsive (test at 375px)
- [ ] Color contrast meets 4.5:1 ratio
- [ ] Interactive elements have focus states
