# SASS project
This is a complete, ready to use file structure for a sass project. It does not require compass, can be compiled using any implementation of LibSass.

Inspiration: [KISS principle](https://en.wikipedia.org/wiki/KISS_principle), [DRY principle](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself), [Open/close principle](https://en.wikipedia.org/wiki/Open/closed_principle), [BEM definitions](https://en.bem.info/method/key-concepts/) and [SMACSS](https://smacss.com/).

## Compiler directives
- sass --watch .:. --style=compressed --sourcemap=none
- compass watch --output-style=compressed --no-sourcemap

## Structure
Sections are presented in the order of import order in the main.scss.

### Vendor
- vendor supplied styles,
- imported at start so they can be easily overwritten by custom styling.

### Base
- _No selectors should be defined in these files_
- Settings and helpers/mixins.
- Each file contains explanation of its content.
- reset/normalize if no vendor reset/normalize is used.

### Layout
- _Class prefix: l_
- Layout, doesn't provide any real function, just appearance.
- Always apply to selected class, element (tagname) on the page.
- Never require `!important`.
- Never mixed with javascript.

### Components
- _Class prefix: c_
- Component, defines an object that can be interacted with.
- Each component should be stored in separate folder.
- Often mixed with javascript code.

### Utils
- _Class prefix: has/is_
- Can be used to style otherwise unspecified element (not block, not element).
- Should do one single job, have as few CSS properties as possible.
- Always use `!important` to have a high chance of immutability of applied state.
- Usually applied by javascript to update view after changes.

### Modules
- _Class prefix: m or <module-name>_
- Styles unique for given application module.
- Reusable, modular parts of our design. They are the sidebar sections, the product lists and so on.
- Each module should be stored in separate folder.
- Often mixed with javascript code.

### shame.scss
- Class prefix: __
- Whenever a temporary or bad styling has to be applied, prefix with two underscores.
- Should be fixed or modified as soon as possible.

### debug.scss
- Styles for debugging, import them at the end of main.scss

## Interaction with javascript
Classes used to manipulate DOM with Javascript should almost never be styled, with exception of application wide implementations. To additionaly separate the roles, they should be prefixed with `js-`.

## Themes
Normally, there are no themes defined by the structure, but it can be easily adapted.
1. Rename "main.scss" file to "_ compiled.scss".
2. In this file, comment out declared colors and settings.
3. For each theme, create file new file, that will declare theme colors and settings.
4. At the end of each theme file, @import "_ compiled".

## Do's and don'ts
1. All `@extend`, `@include` rules must be at the top of the class.
2. All `&` rules must be at the bottom of the class.
3. If you repeat some styling, make it component, layout, or util.
4. Avoid per attribute styling unless it's really required.
5. Avoids nesting more than 3 selectors down.
6. Suggested maximum lines per file: 100.
7. Don't `@extend` in your module from other modules, in your component from other components, etc. This will introduce errors when extended module/component changes.
8. At the end of development cycle, review and refactor created code. Files should be small and readable, no more than 3 indents.
9. Do not nest more than 3 deep. Specifity is unbeatable without !important hack and CSS gets hints of DOM structure.
10. Overusing `position:absolute/fix/relative` and `float:left/right` can lead to weird behaviours, and breaks standard flow. Try to minimize usage when possible.
11. Create classes that do what their name suggest. If more properties are added to the class, check if the name still suits the function.
12. Avoid side effects (styling object in context of other object) - these are terrible to fix and understand.
