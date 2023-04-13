
# Sass Basics



## Q. What is Sass?

The **Sass** ( which stands for 'Syntactically awesome style sheets ) is an extension of CSS that enables you to use things like variables, nested rules, inline imports and more. It also helps to keep things organised and allows you to create style sheets faster.

Sass works by writing your styles in .scss (or .sass) files, which will then get compiled into a regular CSS file. The newly compiled CSS file is what gets loaded to your browser to style your web application. This allows the browser to properly apply the styles to your web page.

![](https://hub.verj.io/ebase/doc/Using_SCSS_Files_files/image002.png)




## Q. List out the differences between LESS and Sass?

|LESS                                 |Sass                         |
|-------------------------------------|-----------------------------|
|LESS compiler is coded in Javascript |Sass compiler is coded in Dart
|Variable names are prefaced with the @symbol |Variable name are prefaced with $ symbol
|LESS does not inherit multiple selectors with one set of properties | Sass inherits multiple selectors with one set of properties |
|LESS does not work with "unknown" units neither it returns syntax error notification for incompatible units or maths related syntax error|	Sass allows you to work with "unknown" units also returns a syntax error notification for incompatible units|



## Q. Why Sass is considered better than LESS?

* Saas allows you to write reusable methods and use logic statements, e., loops, and conditionals
* Saas user can access Compass library and use some awesome features like dynamic sprite map generation, legacy browser hacks * and cross-browser support for CSS3 features
* Compass also allows you to add an external framework like Blueprint, Foundation or Bootstrap on top
* In LESS, you can write a basic logic statement using a "guarded mixin", which is equivalent to Sass if statements
* In LESS, you can loop through numeric values using recursive functions while Sass allows you to iterate any kind of data
* In Sass, you can write your own handy functions



## Q. What are Sass, Less, and Stylus?

They are CSS preprocessors. They are an abstraction layer on top of CSS. They are a special syntax/language that compile down into CSS. They make managing CSS easier, with things like variables and mixins to handle vendor prefixes (among other things). They make doing best practices easier, like concatenating and compressing CSS.



## Q. What is file splitting and why should you use it?

File splitting helps organize your CSS into multiple files, decreasing page load time and making things easier to manage. How you decide to split them up is up to you, but it can be useful to separate files by component. For example, we can have all button styles in a file called `_buttons.scss` or all your header-specific styles in a file called `_header.scss`, main file, say _app.scss, and we can import those files by writing @import 'buttons';



## # 2. SASS VARIABLES



## Q. How variables work in sass?

Variables are useful for things like colors, fonts, font sizes, and certain dimensions, as you can be sure always using the same ones. Variables in SCSS start with `$` sign

**SCSS Style:**

```scss
$font-stack:    Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

**CSS Style:**

```css
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}
```

When the Sass is processed, it takes the variables we define for the `$font-stack` and `$primary-color` and outputs normal CSS with our variable values placed in the CSS. This can be extremely powerful when working with brand colors and keeping them consistent throughout the site.




## Q. What is variable interpolation in Sass?

Interpolation allows us to interpolate sass expressions into a simple Sass or CSS code. Means, you can define selector name, property name, CSS at-rules, quoted or unquoted strings etc, as a variable.

**Syntax:**

```scss
#{$variable_name}
```

**SCSS Style:**

```scss
@mixin corner-icon($name) {
  /* using interpolation */
  .icon-#{$name} {
    background-image: url("/icons/#{$name}.svg");
  }
}

/* calling the above mixin */
@include corner-icon("mail");
```

**CSS Style:**

```css
.icon-mail {
  background-image: url("/icons/mail.svg");
}
```

Here, the value of the **$name** variable is added wherever we used **#{$name}** in our stylesheet.



## # 3. SASS NESTING



## Q. How does nesting work in Sass?

Basic nesting refers to the ability to have a declaration inside of a declaration.

**SCSS Style:**

```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

**CSS Style:**

```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
nav li {
  display: inline-block;
}
nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```



## # 4. SASS PARTIALS



## Q. What is Sass Partials?

By default, Sass transpiles all the **.scss** files directly. However, when you want to import a file, you do not need the file to be transpiled directly. If you start the filename with an underscore, Sass will not transpile it. Files named this way are called partials in Sass.

**Example:**

The following example shows a partial Sass file named "_colors.scss".

```css
/**
 * "_colors.scss
 */
$myPink: #EE82EE;
$myBlue: #4169E1;
$myGreen: #8FBC8F;
```

Now, if you import the partial file, omit the underscore. Sass understands that it should import the file "_colors.scss":

```css
/**
 * Sass Partials
 */
@import "colors";

body {
  font-family: Helvetica, sans-serif;
  font-size: 18px;
  color: $myBlue;
}
```



## # 5. SASS @IMPORT



## Q. What is the use of the @import function in Sass?

The Sass **@import** function helps us to import multiple Sass or CSS stylesheets together such that they can be used together. Importing a Sass file using the @import rule allows access to mixins, variables, and functions to the other file in which the other file is imported.

**Example:**

```scss
/**
 * common/_button.scss
 */
button {
  padding: .25em;
  line-height: 0;
}
```

```scss
/**
 * common/_lists.scss
 */
ul, ol {
  text-align: left;

  & & {
    padding: {
      bottom: 0;
      left: 0;
    }
  }
}
```

```scss
/**
 * style.scss
 */
@import 'common/button', 'common/lists';
```


## # 6. SASS @MIXIN



## Q. Explain use of @mixin in Sass?

A mixin lets you make groups of CSS declarations that you want to reuse throughout your site

```scss
@mixin border-radius($radius) {
  -webkit-border-radius: $radius;
     -moz-border-radius: $radius;
      -ms-border-radius: $radius;
          border-radius: $radius;
}
```

```scss
.box { @include border-radius(10px); }
```



## Q. What is the meaning of DRY-ing out a mixin?

**DRY-ing** out a mixin means splitting it into **static** and **dynamic** parts. The dynamic mixin is the one the user is going to call, and the static mixin is only going to contain the pieces that would otherwise get duplicated.

**Example:**

```scss
@mixin button($color) {
		@include button-static;

	background-color: $color;
	border-color: mix(black, $color, 25%);
  
	&:hover {
		background-color: mix(black, $color, 15%);
		border-color: mix(black, $color, 40%);
	}
}

@mixin button-static {
	border: 1px solid;
	border-radius: 5px;
	padding: .25em .5em;
	
	&:hover {
		cursor: pointer;
	}
}
```





## Q. Explain the use @extend in Sass?

**@extend** directive provides a simple way to allow a selector to inherit/extend the styles of another one.

```scss
.message {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.success {
  @extend .message;
  border-color: green;
}

.error {
  @extend .message;
  border-color: red;
}
```



## # Q. How Sass support Inheritance?

Using `@extend` lets you share a set of CSS properties from one selector to another.  

**SCSS Style:**

```scss
/* This CSS will print because %message-shared is extended. */
%message-shared {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

// This CSS won't print because %equal-heights is never extended.
%equal-heights {
  display: flex;
  flex-wrap: wrap;
}

.message {
  @extend %message-shared;
}

.success {
  @extend %message-shared;
  border-color: green;
}

.error {
  @extend %message-shared;
  border-color: red;
}

.warning {
  @extend %message-shared;
  border-color: yellow;
}
```

**CSS Style:**

```css
/* This CSS will print because %message-shared is extended. */
.message, .success, .error, .warning {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.success {
  border-color: green;
}

.error {
  border-color: red;
}

.warning {
  border-color: yellow;
}
```





















## # 11. SASS NUMERIC



## Q. Explain Number data in Sass?

```scss
p {
   font-size: 3em * 1.5;
}
```



## Q. What are number operations in SASS?

Sass allows for mathematical operations such as addition, subtraction, multiplication and division. They automatically convert between compatible units.

**SCSS Style:**

```scss
/**
 * style.scss
 */
$size: 25px;

h2 {
   font-size: $size + 5;
}

h3 {
   font-size: $size / 5;
}

.para1 {
   font-size: $size * 1.5;
}

.para2 {
   font-size: $size - 10;
}
```

**CSS Style:**

```css
h2 {
   font-size: 30px;
}

h3 {
   font-size: 5px;
}

.para1 {
   font-size: 37.5px;
}

.para2 {
  font-size: 15px;
}
```


## # 12. SASS LIST



## Q. How to use list in Sass?

```scss
// Separated by commas.
$number-list: 10, 23, 10; 

// Separated by spaces.
$number-list2: 10px 20px 30px; 

// Nested list.
$number-list3: 10, 20 30, 10; 

// Nested list same as $number-list3.
$number-list4: 10, (20 30), 10; 
```





## Q. What is the use of Sass Maps functions?

Sass provides the data type called map which represents one or more pairs of key values. The map, which returns a map, provides a new map and does not modify the initial map.

**Example:**

```scss
/**
 * map.get()
 */
$font-weights: ("regular": 400, "medium": 500, "bold": 700);

@debug map.get($font-weights, "medium"); // 500
@debug map.get($font-weights, "extra-bold"); // null
```



## # 14. SASS SELECTOR



## Q. When can you use the %placeholders in Sass?

Placeholder is special kind of selector which is used for writing own Sass library. Its work is very similar to mixin without arguments. Placeholder selector starts with a **%** sign. Placeholder selectors are excluded in the compilation of the Sass file

**Syntax:**

```scss
@extend %( name_of_selector );
```

**SCSS Style:**

```scss
%button-format {
    padding: 10px 20px;
    border-radius: 15px;
    color: black;
}

.toolbar-button {
    @extend %button-format;
    background-color: lightpink;

    &:hover {
        background-color: rgb(155, 106, 114);
    }
}

.status-bar-button {
    @extend %button-format;
    background-color: lightblue;

    &:hover {
        background-color: blue;
    }
}
```

**CSS Style:**

```css
.status-bar-button, .toolbar-button {
    padding: 10px 20px;
    border-radius: 15px;
    color: black;
}

.toolbar-button {
  background-color: lightpink;
}
.toolbar-button:hover {
  background-color: #9b6a72;
}

.status-bar-button {
  background-color: lightblue;
}
.status-bar-button:hover {
  background-color: blue;
}
```


## Q. What is the use of &combinator?

A combinator is something that explains the relationship between the selectors. A CSS selector can contain more than one simple selector. Between the simple selectors, we can include a combinator.

There are four different combinators in CSS:

* Descendant selector (space)
* Child selector (>)
* Adjacent sibling selector (+)
* General sibling selector (~)

**Example 01:** Without the combined child selector

```scss
card {
  outer {
    inner {
    	color: red;
    }
  }
}
```

**Example 02:** Using **>** selector

```scss
card {
 > outer {
   > inner {
     color: red;
   }
 }
}
```



## Q. Which symbol is used to refer parent selector in Sass?

The sass avoids the rewrite code using the nesting method. To refer the parent selector and inside of parent selector **&** symbol is required. This symbol used for hover, focus and active status in style tag.

```scss
.alert {
  // The parent selector can be used to add pseudo-classes to the outer
  // selector.
  &:hover {
    font-weight: bold;
  }
```



## # 15. SASS COLOR



## Q. What are the types of colors support Sass?

```scss
// RGB (Red, Green, Blue):
$primary: rgb(214,121,45);

// RGBA (Red, Green, Blue, Alpha):
$color: rgba(210, 122, 54, 0.5)

// HSL ( Hue, Saturation, Lightness):
$color: hsl(0, 0%, 100%);

// HSLA (Hue, Saturation, Lightness, Alpha):
$color: hsla(100, 60%, 60%, 0.7)
```



## # 16. SASS MISCELLANEOUS



## Q. How many output styles are there in Sass?

By default, Sass outputs the CSS in a nested style, which is a style that reflects the document structure. Sass allows to choose between four styles: nested, expanded, compact, and compressed.

**:nested**

Nested style is the default Sass style because it reflects the structure of the CSS styles in which each property has its own line, but the indentation is based on how deeply it\'s nested.

```cmd
sass --watch style.scss:style.css --style nested
```

```scss
main {
  padding: 12px 24px;
  margin-bottom: 24px; }
 
article {
  background-color: #00ff00;
  color: red;
  border: 1px solid blue; }
  article p {
    font-size: 18px;
    font-style: italic;
    margin-bottom: 12px; }
```

**:expanded**

In expanded style properties are indented within the rules, but the rules aren\'t indendented in any special way like in :nested output style.

```cmd
sass --watch style.scss:style.css --style expanded
```

```scss
main {
  padding: 12px 24px;
  margin-bottom: 24px;
}
 
article {
  background-color: #00ff00;
  color: red;
  border: 1px solid blue;
}
article p {
  font-size: 18px;
  font-style: italic;
  margin-bottom: 12px;
}
```

**:compact**

In compact style each rule takes up only one line with every property defined on that line. It takes up less space than :nested and :expanded.

```cmd
sass --watch style.scss:style.css --style compact
```

```scss
main { padding: 12px 24px; margin-bottom: 24px; }
 
article { background-color: #00ff00; color: red; border: 1px solid blue; }
article p { font-size: 18px; font-style: italic; margin-bottom: 12px; }
```

**:compressed**

Compressed styles takes up the minimum amount of space possible. There is no whitespace except space that is necessary to separate selectors and the newline on the end of the document. 

```cmd
sass --watch style.scss:style.css --style compressed
```

```scss
main{padding:12px 24px;margin-bottom:24px}article{background-color:#00ff00;color:red;border:1px solid blue}article p{font-size:18px;font-style:italic;margin-bottom:12px}
```

