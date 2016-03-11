# Responsive Suffixes
An approach for creating selectors that target small, medium or large screens.

Based on the article of "[BEMIT: Taking the BEM Naming Convention a Step Further](http://csswizardry.com/2015/08/bemit-taking-the-bem-naming-convention-a-step-further/)".

* `@large`: Suffix applied to your targeted "larger" viewports.
* `@medium`: Suffix applied to your targeted "medium" viewports.
* `@small`: Suffix applied to your targeted "small" viewports.
* `@medium-large`: Suffix applied to your targeted viewports that occur from "medium to large" viewports.
* `@small-medium`: Suffix applied to your targeted viewports that occur from "small to medium" viewports.


* > [Demo on CodePen](http://codepen.io/kevinmack18/pen/BjgwER/?editors=1100)

## MIXINS
Mixin to apply suffixes to selectors. Passing in options will provide different outputs, has up to 6 values that need to be passed:

* `$small`: `$suffixcate_suffix-small` (Defined variable for project's "small breakpoint") - Used as the option to target the "large breakpoint" to add `@small` suffix.
* `$medium`: `$suffixcate_suffix-medium` (Defined variable for project's "medium breakpoint") - Used as the option to target the "large breakpoint" to add `@medium` suffix.
* `$large`: `$suffixcate_suffix-large` (Defined variable for project's "large breakpoint") - Used as the option to target the "large breakpoint" to add `@large` suffix.
* `$bp`: Default value: `$suffixcate_bp` (Defined variable for project's "main breakpoint").
* `$base`: Default value: `true` - Used as the option to include initial CSS properties in the selector or just target the generatored suffixed versions
* `$all`: Default value: `false` - Used as the option to output all variations of suffixed: `@small`, `@medium`, `@small-medium`, `@medium-large`, `@large`


```sass
	@include suffixcate($small: $suffixcate_suffix-small, $medium: $suffixcate_suffix-medium, $large: $suffixcate_suffix-large, $bp: $suffixcate_bp, $base: true, $all: false);
```

#### Example 1: Basic
**Sass:**
```sass
.selector-name { // apply to any selector
	@include suffixcate{
		color: red;
	};
}
```
**Compiled CSS:**
```css
.selector-name {
  color: red;
}
@media screen and (min-width: 460px) {
  .selector-name\@large {
    color: red;
  }
}
@media screen and (max-width: 460px) {
  .selector-name\@small {
    color: red;
  }
}
```

#### Example 2: Exclude Base
**Sass:**
```sass
.selector-name($base: false) { // apply to any selector
	@include suffixcate{
		color: red;
	};
}
```
**Compiled CSS:**
```css
@media screen and (min-width: 460px) {
  .selector-name\@large {
    color: red;
  }
}
@media screen and (min-width: 460px) and (max-width: 768px) {
  .selector-name\@medium {
    color: red;
  }
}
@media screen and (max-width: 460px) {
  .selector-name\@small {
    color: red;
  }
}
```

#### Example 3: Include "medium" suffix
**Sass:**
```sass
.selector-name { // apply to any selector
	@include suffixcate($bp: $suffixcate_bp-all){
		color: red;
	};
}
```
**Compiled CSS:**
```css
.selector-name {
  color: red;
}
@media screen and (min-width: 768px) {
  .selector-name\@medium-large {
    color: red;
  }
}
@media screen and (min-width: 460px) and (max-width: 768px) {
  .selector-name\@medium {
    color: red;
  }
}
@media screen and (max-width: 460px) {
  .selector-name\@small-medium {
    color: red;
  }
}
```

#### Example 4: Include all suffixes
**Sass:**
```sass
.selector-name { // apply to any selector
	@include suffixcate($bp: $suffixcate_bp-all, $all: true){
		color: red;
	};
}
```
**Compiled CSS:**
```css
.selector-name {
  color: red;
}
@media screen and (min-width: 460px) {
  .selector-name\@large {
    color: red;
  }
}
@media screen and (min-width: 768px) {
  .selector-name\@medium-large {
    color: red;
  }
}
@media screen and (min-width: 460px) and (max-width: 768px) {
  .selector-name\@medium {
    color: red;
  }
}
@media screen and (max-width: 460px) {
  .selector-name\@small-medium {
    color: red;
  }
}
@media screen and (max-width: 460px) {
  .selector-name\@small {
    color: red;
  }
}
```


### `suffixcateSmall()`
Short-hand mixin to apply just small suffixes to selector.

* `$bp`: The breakpoint of for the selector to have suffix added.
* `$base`: Default value: `true` - Used as the option to include initial CSS properties in the selector or just target the generatored small suffixed version.


```sass
	@include suffixcate($small: $suffixcate_suffix-small, $medium: $suffixcate_suffix-medium, $large: $suffixcate_suffix-large, $bp: $suffixcate_bp, $base: true, $all: false);
```

#### Example 1: Basic
**Sass:**
```sass
.selector-name { // apply to any selector
	@include suffixcateSmall {
		color: red;
	};
}
```
**Compiled CSS:**
```css
.selector-name {
  color: red;
}
@media screen and (max-width: 460px) {
  .selector-name\@small {
    color: red;
  }
}
```

#### Example 1: Unique breakpoint
**Sass:**
```sass
.selector-name { // apply to any selector
	@include suffixcateSmall($bp: 400px) {
		color: red;
	};
}
```
**Compiled CSS:**
```css
.selector-name {
  color: red;
}
@media screen and (max-width: 400px) {
  .selector-name\@small {
    color: red;
  }
}
```


### `suffixcateMedium()`
Short-hand mixin to apply just medium suffixes to selector.

* `$bp`: The breakpoint of for the selector to have suffix added. Is required to be two values: "main breakpint" and "medium breakpoint.
* `$base`: Default value: `true` - Used as the option to include initial CSS properties in the selector or just target the generatored medium suffixed version.
* `$all`: Default value: `false` - Used as the option to output variations of medium suffix: `@medium`, `@small-medium`, `@medium-large`

```sass
	@include suffixcateMedium();
```


### `suffixcateLarge()`
Short-hand mixin to apply just medium suffixes to selector.

* $bp: The breakpoint of for the selector to have suffix added. Is required to be two values: "main breakpint" and "medium breakpoint.
* $base: Default value: `true` - Used as the option to include initial CSS properties in the selector or just target the generatored large suffixed version.

```sass
	@include suffixcateLarge();
```


### `suffixcateExtend()`
Utilize Sass `@extend` directive to share properties of other selectors with the suffixes.

* `$selector`: A list of selectors you want to extend.

```sass
	@include suffixcateExtend($selector: {value});
```

#### Example: Basic
**Sass:**
```sass
.demo-1 {
	@include suffixcateLarge {
		color: #FFF;
		background: #000;
	}
}

.selector-extended-demo {
	@include suffixcateExtend($selector: ".demo-1");
}
```
**Compiled CSS:**
```css
.demo-1, .selector-extended-demo {
  color: #FFF;
  background: #000;
}
@media screen and (min-width: 460px) {
  .demo-1\@large, .selector-extended-demo\@large {
    color: #FFF;
    background: #000;
  }
}
```

