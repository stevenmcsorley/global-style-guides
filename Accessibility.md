[**↺**BACK](./README.md)
# Accessibility
Generally speaking, a site is accessible when the site's content is available, and its functionality can be operated, by literally anyone.
  - [Mission](#mission)
  - [Levels](#levels)
  - [Principles](#principles)
  - [General Rules](#general-rules)
  - [Tools](#tools)
  - [Inspiration for this Guideline](#inspiration-for-this-guideline)

## Mission

To achieve WCAG 2.0/2.1 (AA) throughout projects and (AAA) where possible.

## Levels
There are  three levels of accessibility compliance in WCAG, they refect the priority of support.
  - **A:** Essential. If this isn't met, assistive technology may not be able to read, understand, or fully operate the page or view.
  - **AA:** Ideal support. Now required for EU government and public body websites.
  - **AAA:** High-level support. This is typically reserved for sites that serve a specialized audience.

## Principles
- **Perceivable** - information and user interface components must be presentable to users in ways they can recognize.
  - *Text alternative* (A) - for any non-text content so that it can be changed into other forms people need, such as large print, braille, speech, symbols or simpler language
  - ~~Time base media~~
  - *Adaptable* - content that can be presented in different ways (for example simpler layout) without losing information or structure.
    - Info and relationships (A)
    - Meaningful sequence (A)
    - Sensory characteristics (A)
    - Orientation (AA)
    - Identify input purpose (AA)
  - *Distinguishable* - easier for users to see and hear content including separating foreground from background.
    - Use of colour (A)
    - ~~Audio control~~
    - Contrast (minimum) (AA)
    - Resize text (AA)
    - Images of text (AA)
    - Reflow (AA)
    - Non-text contrast (AA)
    - Text spacing (AA)
    - Content on hover or focus (AA)
- **Operable** - user interface components and navigation must be functional.
  - *Keyboard accessible* -  all functionality must be available from a keyboard.
    - Keyboard (A)
    - No keyboard trap (A)
    - Character key shortcuts (A)
  - *Enough time* - provide users enough time to read and use content.
    - Timing adjustable (A)
    - ~~Pause, stop, hide~~
  - ~~Seizures and physical reactions~~
  - *Navigable* - provide ways to help users navigate, find content, and determine where they are.
    - Bypass blocks (A)
    - Page titled (A)
    - Focus order (A)
    - Link purpose (in context) (A)
    - Multiple ways (AA)
    - Headings and labels (AA)
    - Focus visible (AA)
  - *Input modalities* - provide the same functionality to all users who are unable to perform complex gestures, by giving alernatives with basic gestures.
    - Pointer gestures (A)
    - Pointer cancellation (A)
    - Label in name (A)
    - Motion actuation (A)
- **Understandable** - the information and the operation of user interface must be unambiguous.
  - *Readable* - text content must be readable and understandable.
    - Language of page (A)
    - Language of parts (AA)
  - *Predictable* - web pages must appear and operate in predictable ways.
    - On focus (A)
    - On input (A)
    - Consistent navigation (AA)
    - Consistent identification (AA)
  - *Input assistance* - help users avoid and correct mistakes.
    - Error identification (A)
    - Labels or instructions (A)
    - Error suggestion (AA)
    - Error prevention (legal, financial, data) (AA)
- **Robust** - content must be robust enough that it can be interpreted reliably by a wide variety of user agents, including assistive technologies.
  - *Compatible* - maximize compatibility with current and future user agents, including assistive technologies.
    - Parsing (A)
    - Name, role, value (A)
    - Status messages (AA)

## General Rules
- Use plain translated language
> ***Why?*** Less confusion, easier to understand in multiple languages.
- Use semantic HTML
> ***Why?*** Easier to develop with, better on mobile, good for SEO.
- Use clear keyboard navigation and focus
> ***Why?*** Clean UI easy and fast for anyone.
- Use images with alt and text alternatives
> ***Why?*** Everyone in any situation can understand the meaning.
- Use the app with different devices, orientation or zooms
> ***Why?*** Everyone can have a similar and all-inclusive experience.
- Use color to help the UX, not hinder or hide functionality
> ***Why?*** Everyone can have the same functionality.

## Tools
- Browser developer tools
  - Chrome - inspect accessability tab, audit tab
  - Edge - inspect accessability tab, audit tab
  - Firefox - inspect accessability tab, audit tab
  - IE - inspect accessability tab
  - Safari - inspect node tab accessability dropdown, audit tab
- Screen readers
  - [Orca Screen Reader](https://wiki.gnome.org/Projects/Orca) - Linux
  - [VoiceOver](https://www.apple.com/uk/accessibility/mac/vision/) - Mac 
  - [NVDA](https://www.nvaccess.org/), [JAWS](https://www.freedomscientific.com/products/software/jaws/) - Windows
  - [Chrome Vox](http://www.chromevox.com/)
- Web sites
  - [HTML5 Accessibility](https://www.html5accessibility.com/)
  - [Using ARIA](https://w3c.github.io/using-aria/)

## Inspiration for this Guideline
 - [WCAG2.1](https://www.w3.org/TR/WCAG21/)
 - [The A11Y Project](https://a11yproject.com)
 - [Google developers](https://developers.google.com/web/fundamentals/accessibility/)
 - [Wiki](https://en.wikipedia.org/wiki/Web_Content_Accessibility_Guidelines)

[**⇪**TOP](#accessability)