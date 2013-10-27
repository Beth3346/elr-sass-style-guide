# DRM SASS Style Guide

Adapted from: [http://css-tricks.com/css-style-guides/](http://css-tricks.com/css-style-guides/)

### Use Your Regular CSS Formatting Rules / Style Guide

#### Always leave a space between selector and opening brace
#### Always leave a blank line between nested selectors
#### Always leave a blank line after closing braces
#### No double spacing after rules
#### One selector per line, One rule per line
#### Indent all rules once
#### List related properties together
#### Have a plan for class name naming
#### Prefer .classes over #ids in selectors
#### Use semantic class names whenever possible
#### Avoid using presentational class names such as bold or center
#### Always use scss syntax
#### Use dashes instead of underscore or camelCase for all filenames and selectors

#### Create partials for _extends, _variables, and _media-query breakpoints
+ No variables in .scss files that contain rules

#### Use a consistent pattern for ordering rules
+ List @extend(s) First
+ List "Regular" Styles Next

+ List @include(s) Next

	+ This visually separates the @extends and @includes as well as groups the @includes for easier reading
	+ You might also want to make the call on separating user-authored @includes and vendor-provided @includes

+ Nested Selectors Last

	+ Nothing goes after the nested stuff.
	+ The same order as above within the nested selector would apply

#### All Vendor Prefixes Use @mixins

+ Use compass @mixins for this whenever possible

#### Maximum Nesting: Three Levels Deep

+ Chances are, if you're deeper than that, you're writing a crappy selector. Crappy in that it's too reliant on HTML structure (fragile), overly specific (too powerful), and not very reusable (not useful). It's also on the edge of being difficult to understand.

+ Possibly even make use of extend so it has the benefit on the CSS side of re-usability.

#### Do not nest Sass rules if it creates an overly specific selector

+ If a nested block of Sass is longer than that, there is a good chance it doesn't fit on one code editor screen, and starts becoming difficult to understand.

+ The whole point of nesting is convenience and to assist in mental grouping. Don't use it if it hurts that.

#### Global and Section-Specific Sass Files Are just Table of Contents

+ In other words, no styles directly in them. Force yourself to keep all styles organized into component parts.

#### List Vendor/Global Dependencies First, Then Author Dependencies, Then Patterns, Then Parts

+ So the "table of contents" things comes together like:

+ The dependencies like Compass, colors, and mixins generate no compiled CSS at all, they are purely code dependencies. Listing the patterns next means that more specific "parts", which come after, have the power to override patterns without having a specificity war.

#### Break Into As Many Small Files As Makes Sense

+ There is no penalty to splitting into many small files. Do it as much as feels good to the project. I know I find it easier to jump to small specific files and navigate through them than fewer/larger ones.

+ I'd probably do this right in the global.scss, rather than have global @import a _header.scss file which has its own sub-imports. All that sub-importing could get out of hand.

+ Globbing might help if there starts to be too many to list.

#### Partials are named _partial.scss

+ This is a common naming convention that indicates this file isn't meant to be compiled by itself. It likely has dependencies that would make it impossible to compile by itself. 

#### Locally, Compile Expanded with Line Mapping

+ This means dev tools can tell you exactly what file and on what line rules are coming from, even if it is an imported partial.

#### In Deployment, Compile Compressed

+ Live websites should only ever have compressed CSS.

#### Don't Even Commit .css Files

+ This might take some workflow changes, but it's pretty nice if .css files aren't even in your repository. 
+ The compilation happens during deployment. So the only thing you see in the repo are your nicely formatted hand authored Sass files.

#### Be Generous With Comments

+ It is rare to regret leaving a comment in code. It is either helpful or easily ignorable. Comments get stripped when compiling to compressed code, so there is no cost.
+ Use // syntax for all comments

#### Use Variables for All Common Numbers, and Numbers with Meaning

+ If you find yourself using a number other than 0 or 100% over and over, it likely deserves a variable. Since it likely has meaning and controls consistency, being able to tweak it easily may be useful.
+ If a number clearly has strong meaning, that's a use case for variables as well.

#### Use variables for all colors other than black and white

+ Chances are a color isn't one-off, and even if you think it is, once it's in a variable you might see uses for it elsewhere.
+ Variations on that color can often be handled by the Sass color functions like lighten() and darken()
+ This make updating colors easier (change in one place, whole color scheme updates).

#### Nest and Name Your Media Queries

#### Shame Last

+ In your global stylesheet, @import a _shame.scss file last.
+ If you need to make a quick fix, you can do it here. Later when you have proper time, you can move the fix into the proper structure/organization.

#### Final Output Is On You

+ Write Sass such that the final CSS output is just as you would have written it without Sass.