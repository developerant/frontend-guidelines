Front End Rules
===============

The rules are here as our guide to all things Front End at Architect, they are created by us and for us*. By following these rules we ensure our code is well-written, well thought out, and easy to maintain.

> Every line of code should appear to be written by a single person, no matter the number of contributors.
[@mdo](https://twitter.com/mdo)

## Rule 1: Use utility classes.
A .block .with-something .with-something-else

## Rule 5: Contribute.
The rules are not here to be written by one and followed by all, they are written by the team for the team. So contribute your ideas and best practices! See [How to Contribute](docs/rules-for-contributing.md).

## Rule 6: Use Spaces instead of tabs.
Always use spaces, never tabs. Ensure everything nested is indented correctly by a single tab in all code including HTML, CSS/Sass and JavaScript.

## Rule 7: Do not use that which is unnecessary.
Code and Page bloat are easily avoidable, and serve both the developer and the audience to avoid. The more external frameworks we include in our JavaScript the longer each page takes to load, and the more code we have to trawl through when something goes wrong. Usually, there is a micro-library that will do the same thing, if VanillaJS won't.

This doesn't mean using micro-libraries over jQuery is always the correct option, but should be at least considered on a project specific basis.

## Rule 8: It is what it is
Naming conventions for selectors should be based on what they are rather than what they look like. Class names like `bluetext`, or `redborder` become redundant if your colour scheme changes. A much better way to name your classes is with the role a certain HTML element is intended for in the document.

## Rule 9: Doctype.
**Always** use the HTML5 Doctype:

	<!DOCTYPE html>

## Rule 10: Attribute order
HTML attributes should come in this particular order for easier reading of code.

- src, for, type, href
- title, alt, name
- id
- class
- data-*
- aria-*, role
- boolean attributes (required, checked, etc.)

To easily understand the markup you're writing, the main attribute of the element should be first, and for images and links, the title/alt attribute should follow immediately. Style and interaction attributes like classes, IDs, and data attributes should be towards the end of the elements, followed by a11y attributes.

	<input type="text" name="..." id="..." class="..." required>

	<img src="..." alt="..." class="...">

	<a href="..." title="..." id="..." class="..."></a>

## Rule 11: * { box-sizing: border-box; }
Border box is not default and required far more for responsive layouts than content-box. To save time worrying about when it's included, border-box everything. Use the compass mixin for backward compatibility up to and including IE8. Won't affect speed or anything - using `*` uses just as much memory as any other css.

See [Paul Irish's article](http://www.paulirish.com/2012/box-sizing-border-box-ftw/) for more information.

## Rule 12: The correct number of JavaScript libraries to know is `n+1`
Most front end developers are familiar with JavaScript and jQuery, but there are now more frameworks than you can shake a stick at! Whether it's Angular, Meteor, Backbone, Ember, Coffeescript, or Node.js there's always something new to learn. The drive of a front end developer should mean there's always more you can learn, whether you have the time or not is another matter, but it's the drive that's important.

## Rule 13: Comments (Sass)
Ensure comments are consistent and beautiful. In SCSS, avoid using `/* */` for single-line/inline comments - use `//` instead.

To break up a section of CSS in a file use the following comment style:

	// ===================================
	// Header
	// ===================================

This is a nice and clear method of introducing a new section in a CSS file and comes with the advantage that it won't be processed into the raw CSS.

## Rule 14: Follow the Outside-In order for style definitions
When defining styles, always follow the Outside-In order. This means:

- Layout Properties (`position`, `float`, `clear`, `display`, `z-index`)
- Box Model Properties (`width`, `height`, `margin`, `padding`)
- Visual Properties (`background`, `border`, `box-shadow`)
- Typography Properties (`color`, `font-family`, `font-size`, `text-align`, `text-transform`)
- Misc Properties (`cursor`, `overflow`)

For more information and an example, this has been slightly modified from an [article by Guy Routledge on WebTuts+](http://webdesign.tutsplus.com/articles/outside-in-ordering-css-properties-by-importance--cms-21685)

## Rule 15: Use whitespace
Good readability is key for good code, so make whitespace your friend. Leave space around all declarations and rules, and keep tabbing consistent throughout your code.

This:

	.element {
		display:block;
		width:100%;

		.child {
			width:50%;
		}
	}

	.another-element {
		[...]
	}

Not:

	.element{
		display:block;
		width:100%;
		.child{
			width:50%;
		}
	}
	.another-element { [...] }

## Rule 16: Multi-line CSS
Make sure CSS rules are always written across multiple lines and not a single line, the only exception being where there is only one rule for an element or a list of similar declarations that should be grouped for easier understanding.

## Rule 17: Nesting - 3 levels deep (4 absolute maximum)
In Sass aim to nest no more than 3 levels deep, with an absolute maximum of 4 levels. Sass makes it easy to nest selectors without much hassle but this results in overly specific selectors and will cause issues later on when trying to overwrite styles.

Note: SCSS-Lint will be set to validate at 4 levels of nesting maximum.

## Rule 18: Naming conventions
All classes should be written in lowercase with hypens used to separate words. Only stray away from this when using a CSS methodology like BEM where underscores are part of the pattern.

## Rule 19: Accessibility first
Always write code with accessibility in mind. Make sure `HTML` is semantic and `CSS` won't cause any issues (see [Rule 20]{#rule-20}). Make sure `aria` roles are used when useful and necessary in `HTML` and

## Rule 20: Avoid `display:none;` where possible
Using `display:none` can be detrimental to accessibility and performance. Hiding content from screenreaders when it should be available or slowing page load times by loading content that will ultimately be hidden from the page. Try other alternatives like positioning off-screen or lazy-loading content if necessary.

## Rule 21: Specificity, don’t use IDs in CSS
ID's are a specificity nightmare so avoid using them in your CSS at all costs, even small specific styles can be applied with a custom class on the element. IDs should be used in HTML for hyperlinks to identify specific content on a page.

## Rule 22: Avoid `!important` at all times
If you have to use `!important` somewhere, the CSS is badly written. Go back and refactor.

## Rule 23: Shame.css
Hacks are ok, for a quick fix. However, put them in a `shame.css` file so we know that they are hacks and need to be refactored.

## Rule 24: Measurements should be applied using the appropriate unit
Font sizes in `rem` (with pixel fallback); the base font size of the site should be left at the default (`16px`) for accessibility. Media Queries in `em`, always; this helps the responsive layout respond when the user adjusts the font size of their browser. Layout in `%`, with padding in `px` for consistency in the design.

## Rule 25: Media query placement
Media queries should appear inline with the element you're applying them to:

	.element {
		width:100%;

		@include breakpoint(medium) {
			width:50%;
		}
	}

This means responsiveness is clear and easy to work with, reduces the amount of duplicate styles, and will be output in the correct order in the compiled CSS.

## Rule 26: Mobile first media queries
Always use min-width media queries so that less CSS is having to be processed on smaller screens. Only use `max-width` queries for mobile specific styles to avoid a lot of overwriting.

The boilerplate has media query mixins the default `breakpoint()` mixin is min-width.

## Rule 27: Don’t hand-write browser-prefixes
Always use either an autoprefixer task or use Compass mixins to output browser prefixes for you, these tools are better handled to deal with outputting what's needed for the browsers we support and will be automatically updated over time.

## Rule 28: Shorthand notation
Always favour shorthand notation.

For instance, use:

	margin:0 20px;
	padding:0 10px 10px;
	background:transparent 0 0 no-repeat;

instead of:

	margin:0 20px 0 20px;
	padding:0 10px 10px 10px;
	background-color:transparent;
	background-position:0 0;
	background-repeat:no-repeat;

## Rule 29: Set up your editor correctly
Always set up your editor to do the formatting work for you where possible.

- Use tabs set to 4 spaces.
- Trim trailing white space on save.
- Set encoding to UTF-8.
- Add new line at end of files.

In Sublime the settings are:

	"tab_size": 4,
	"translate_tabs_to_spaces": false,
	"trim_trailing_white_space_on_save": true,
	"ensure_newline_at_eof_on_save": true,
	"default_encoding": "UTF-8",

## Rule 30: Never omit optional closing tags
Always close tags.

## Rule 31: CSS at the top, JavaScript at the bottom
By default all styles should be included in the `<head>` and all script files should be included before the closing `</body>` tag. Exceptions for Modernizr or fonts is allowed, but jQuery should _always_ be included at the bottom.

_Exceptions of course apply if working with an "above the fold" CSS technique._

## Rule 32: Lint code
Use a task runner to ensure that all code written by us is linted, library code can be excluded from linting. Use both JSHint and SCSS-Lint where possible.

## Rule 33: No spaces after declarations
Makes things easier to read, reduces tram lines.

## Rule 34: Pick a methodology/pattern and stick to it
Following on from [Rule #8](#rule-8) on naming conventions, if you're going to choose a CSS methodology like BEM or OOCSS or the modular JS pattern, make sure you consistent throughout the project. Choose a structure and stick with it throughout and ensure all developers on the project are aware of the methodology being used and remain consistent to it as well.

## Rule 35: Use `$variables` for _all_ colours
Always declare variables for colours, including `black` and `white`. When using a consistent colour palette it makes it much easier to change the site design if even the smallest change has been made.

## Rule 36: Use `$variables` to help keep sizing consistent
Keep a `$spacing` variable - it keeps your site's paddings, margins and gutterings consistent. You can make more variables all relative to your main spacing variable too e.g `$spacing-half: $spacing / 2`. With fonts, this is also a good idea: `$fnt-lrg; $fnt-med; $fnt-small;`. It's easy on big front-end's to end up with random font sizes. Subtle consistency goes a long way.