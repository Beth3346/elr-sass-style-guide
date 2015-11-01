# ELR SASS Style Guide

### Use Your Regular CSS Formatting Rules / Style Guide

Sass should make projects easier to maintain. Keep this in mind while you are writing Sass.
Aim for reusable, flexibile modules.

There are always exceptions to these rules especially when using 3rd party components.

#### Formatting
+ Use dashes instead of underscore or camelCase for all filenames and selectors
+ Always leave a space between selector and opening brace
+ Always leave a blank line between nested selectors
+ Always leave a blank line after closing braces
+ Use a single space after the colon
+ Always end property declarations with a semicolon
+ Put spaces after : in property declarations
+ Put spaces before { in rule declarations
+ No double spacing after rules
+ One selector per line, One rule per line
+ If a selector has one style rule its ok to have it all on one line
+ Indent all rules 4 spaces no tabs ever
+ List related properties together
+ Always use scss syntax
+ Always use shorthand rules
+ Use hex color codes unless transparancy is needed.
+ Avoid trailing spaces
+ All compiled CSS should be compressed
+ Don't just add new styles to the end of the file. Locate and update existing selectors.

#### Number and Units
+ No leading zeros
+ Always omit unit for 0 values
+ Avoid magic numbers https://css-tricks.com/magic-numbers-in-css/
+ Prefer percentages and max/min widths over fixed layouts

#### !important
+ Avoid !important whenever possible
+ Ok for overriding vendor styles in 3rd party components that you have no control over.
+ Also ok for display: none and some application state rules
+ If you are using !important in other parts of your Sass styles you need to refactor immediately

#### Vendor Prefixes
+ Don't use Compass for vendor prefixing. Use autoprefixer instead.
+ Avoid vendor prefixes in Sass files. Use autoprefixer for vendor prefixes.

#### Modules
+ Avoid any vendor styles that your don't understand. No black boxes. If you don't understand it don't use it.
+ If you are constantly overriding styles then refactor.
+ Avoid duplicate rules as much as possible within the same module.
+ Limit side effects.
+ Aim to write code that is encapsulated. Your should be able to remove it without unintended side effects.
+ If you limit side effects dead code will be easy to remove

#### Presentation Styles vs. Layout Styles
+ Presentation-Specific styles are those that only alter the visual design of the element, but don’t change its dimensions or position in a meaningful way. The examples below are presentation-specific.
+ Layout-Specific Styles are those that change the dimensions or positioning of DOM elements. These are mostly layout-specific.
+ Visually separate presentation and layout styles with a line break.
+ All modules should leave layout styles to their container. They should always fill the width of their container.

#### Resets
+ Avoid heavy handed resets.
+ If possible, create a reset that works for you.
+ If you are constantly overriding base styles then remove them from your reset.

#### Frameworks
+ Avoid third-party frameworks if possible.
+ These are usually bloated and styles must be overridden constantly.
+ If you must use a framework ensure that you remove unused styles.
+ If you can build your own framework with mixins that work for you.

#### Helper Classes
+ Helper classes are great for quick prototyping and initial layouts.
+ Remove helper classes and add style rules to selectors later to clean up your markup.
+ Always prefer helper classes to inline styles.

#### Selectors
+ Selectors should always be lowercase
+ Avoid tight coupling with CSS and HTML.
+ Selectors should not rely on a rigid HTML structure.
+ Use dashes to separate words in selectors.
+ IDs
    + Avoid these whenever possible.
    + Use ids as JS selectors but don't use them as CSS selectors
    + The only exception is to style 3rd Party content where you have no control over output.
+ Tag Names
    + Ok for resets and base styles
    + Avoid where possible, use class names instead
    + Fine to use when there’s a ton of elements under the same namespace that need a small tweak
    + Don’t overqualify (a.foo)
+ Class Names
    + Have a plan for class name naming
    + Use semantic class names whenever possible
    + Use longer selectors if they add clairity.
    + No more that 4 words per selector.

#### Put all variables in config file
+ No variable declarations in .scss files that contain rules

#### Use mixins generously
+ If you are repeating the same patterns create a mixin
+ This will make your stylesheets much more predictable and consistent

#### Group related styles into as many separate files/modules as make sense.
+ If a file is more than 100 lines break it up

#### Use a consistent pattern for ordering rules
+ List @extend(s) First
+ List @include(s) Next
+ List "Regular" Styles Next
+ List all media queries with the elements they are modifying
+ Nested Selectors Last
    + Nothing goes after the nested stuff.
    + The same order as above within the nested selector would apply

#### Maximum Nesting: Three Levels Deep
+ Chances are, if you're deeper than that, you're writing a crappy selector. Crappy in that it's too reliant on HTML structure (fragile), overly specific (too powerful), and not very reusable (not useful). It's also on the edge of being difficult to understand.
+ Make selectors as general as possible
+ Avoid nesting all together whenever possible

#### Global and Section-Specific Sass Files Are just Table of Contents
+ In other words, no styles directly in them. Force yourself to keep all styles organized into component parts.

#### List Vendor/Global Dependencies First, Then Author Dependencies, Then Patterns, Then Parts
+ So the "table of contents" things comes together like:
+ The dependencies like Compass, colors, and mixins generate no compiled CSS at all, they are purely code dependencies.
+ Listing the patterns next means that more specific "parts", which come after, have the power to override patterns without having a specificity war.

#### Break Into As Many Small Files As Makes Sense
+ There is no penalty to splitting into many small files. Do it as much as feels good to the project.
+ I know I find it easier to jump to small specific files and navigate through them than fewer/larger ones.

#### Partials
+ Partials are named _partial.scss
+ This is a common naming convention that indicates this file isn't meant to be compiled by itself. It likely has dependencies that would make it impossible to compile by itself.

#### Locally, Compile Expanded with Line Mapping
+ This means dev tools can tell you exactly what file and on what line rules are coming from, even if it is an imported partial.

#### In Deployment, Compile Compressed
+ Live websites should only ever have compressed CSS.

#### Don't Even Commit .css Files
+ This might take some workflow changes, but it's pretty nice if .css files aren't even in your repository.
+ The compilation happens during deployment. So the only thing you see in the repo are your nicely formatted hand authored Sass files.

#### Be Generous With Comments
+ Aim for symantic selectors that don't need comments for clairty
+ It is rare to regret leaving a comment in code. It is either helpful or easily ignorable. Comments get stripped when compiling to compressed code, so there is no cost.
+ Use // syntax for all comments
+ Comment any hacks and quick fixes. Try to refactor these later if possible.

#### Use Variables for All Common Numbers, and Numbers with Meaning
+ If you find yourself using a number other than 0 or 100% over and over, it likely deserves a variable. Since it likely has meaning and controls consistency, being able to tweak it easily may be useful.
+ If a number clearly has strong meaning, that's a use case for variables as well.

#### Use variables for all colors
+ Chances are a color isn't one-off, and even if you think it is, once it's in a variable you might see uses for it elsewhere.
+ Variations on that color can often be handled by the Sass color functions like lighten() and darken()
+ This make updating colors easier (change in one place, whole color scheme updates).
+ Don't use color keywords

#### Media Queries
+ Use ems for breakpoints
+ Don't use use screen
+ Keep these nested in the elements they style.
    + Since styles are modular this makes much more sense than listing them in a separate file.
+ Check all known breakpoints (iPad, iPhone, etc.)
+ Attept to make sites look good at any breakpoint.
    + Don't only design for device specific widths.
    + There is no 'breakpoint'
    + Styling elements this way will help to future proof sites.

#### Shame Last
+ In your global stylesheet, @import a _shame.scss file last.
+ If you need to make a quick fix, you can do it here.
+ Later when you have proper time, you can move the fix into the proper structure/organization.
+ Comment all styles in the shame list and explain why these quick fixes were used.

#### Final Output Is On You
+ Write Sass such that the final CSS output is just as you would have written it without Sass.

#### Use rems instead of px for all sizing except media query breakpoints
+ set a base value for the body element
+ use sass to calculate rems

#### Sources:
+ https://ponyfoo.com/articles/css-the-good-parts
+ https://css-tricks.com/sass-style-guide/