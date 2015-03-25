# Frontend Guidelines

Use [.editorconfig](http://editorconfig.org/) for consistent formatting styles across file formats.

## HTML and CSS

### Styleguide

Adhere to the matching [SuitCSS HTML and CSS styleguide](https://github.com/suitcss/suit/blob/master/doc/STYLE.md) and the [Google HTML/CSS Style Guide](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml).

* Use lowercase words and hyphens for IDs and data attributes. e.g. `<div data-attribute-name="name-of-thing" id="name-of-thing"></div>`

### Architecture

Follow the [SuitCSS design principles](https://github.com/suitcss/suit/blob/master/doc/design-principles.md) and use the [SuitCSS naming conventions](https://github.com/suitcss/suit/blob/master/doc/naming-conventions.md).

Additionally, prefix animation names with the component name, use lower-case words and use hyphens to separate words i.e. `@keyframes component-name-animation-name` e.g. `@keyframes preloader-pulse`.

Use SuitCSS [components](https://github.com/suitcss/suit/blob/master/doc/components.md), [utilities](https://github.com/suitcss/utils) and [base styles](https://github.com/suitcss/base).

### Preprocessor, polyfiller and postprocessor

Use [Stylus](https://github.com/LearnBoost/stylus) as a preprocessor to inline CSS files and provide nesting that supports [media query bubbling](http://learnboost.github.io/stylus/docs/media.html) (which is outside the [CSS Nesting Module](http://tabatkins.github.io/specs/css-nesting/) specification).

Use nesting for only the following and within the order specified (also, add an empty line before the nest):
* Feature tests e.g. `.no-js & {}`.
* Pseudo elements e.g. `&::after {}`.
* Pseudo classes e.g. `&:hover {}`.
* States e.g. on the block/element `&.is-stateName {}` and on a parent e.g. `.is-pageLoading & {}`.
* Support e.g. `@support (hyphens) {}`.
* Media queries e.g. `@media (--medium) {}`.
* Sandboxing/encapsulating descendants within component modifiers e.g. `ComponentName--modifierName { ComponentName-descendantName {} }`.

Use [PostCSS](https://github.com/postcss/postcss) as a polyfiller for the following CSS specifications:

* [CSS Custom Media Queries](http://dev.w3.org/csswg/mediaqueries/#custom-mq).
* [CSS Custom Properties for Cascading Variables Module](http://dev.w3.org/csswg/css-variables/).
* [CSS Values and Units Module (calc notation)](http://www.w3.org/TR/css3-values/#calc-notation).

Use [Autoprefixer](https://github.com/postcss/autoprefixer) as a postprocessor to handle vendor prefixes (via PostCSS.

#### Example of tools in use

```css
/**
 * ComponentName
 *
 * Description of component
 */

@keyframes component-name-animation-name {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}

.ComponentName {
  display: flex;

  /* feature test */
  .no-js & {
    display: block;
  }

  /* pseudo element */
  &::after {
    content 'x';
  }

  /* pseudo class */
  &:hover {
    animation: component-name-animation-name 1.5s ease-out 0s infinite;
    color: var(--color-red);
  }

  /* state on block/element */
  &.is-active {
    color: var(--color-green);
  }

  /* state on some parent */
  .is-pageLoading & {
    color: var(--color-yellow);
  }

  /* support */
  @support (hyphens) {
    hyphens: auto;
    text-align: justify;
  }

  /* media query */
  @media (--medium) {
    color: var(--color-purple);

    /* repeat as above */
    .no-js & {
      display: inline;
    }

    &::after {
      content 'y';
    }

    &:hover {
      width: calc(2 * var(--size-gutter))
    }

    &.is-active {
      color: var(--color-yellow);
    }

    .is-pageLoading & {
      color: var(--color-red);
    }
  }
}

/* unnested element of base component */
.ComponentName-descendantName {
  color: blue;

  /* repeat as above */
  .no-js & {
    display: block;
  }
}

/**
 * modifierName
 *
 * Description of modifier e.g. to illustrate
 * sandboxing/encapsulating component modifiers
 */

.ComponentName--modifierName {

  .ComponentName-descendantName {
    color: var(--color-yellow);

    /* repeat as above */
    .no-js & {
      display: block;
    }
  }
}
```

### Naming of descendants

Keep the naming of descendants consistent across components:

* Use `inner` rather than `wrapper` if an extra element is needed.
* Use `title`, `subTitle` and `body` (rather than `heading` and `content`) to delineate the main content.
* Use `content` to wrap content only when the component also contains presentational mark-up.
* Use `summary` and `details` for revealed content.
* Use `items` for collections.
* Use `item` for elements within a collection.
* Use `media` for images and video.
* Use `<sub component name>` to wrap sub components.

#### Example

```html
<section class="ComponentName">
  <div class="ComponentName-inner">
    <div class="ComponentName-content">
      <div class="ComponentName-summary">
        <div class="ComponentName-audioPlayer" data-region="audio-player"></div>
          <h1 class="ComponentName-title">Title text</h1>
          <img alt="{{alt}}" class="ComponentName-media" src="{{src}}">
        </div>
        <div class="ComponentName-details">
          <p class="ComponentName-body">{{body}}</p>
          <div class="ComponentName-button">
            <button class="Button Button--primary">Button link</button>
          </div>
        </div>
      </div>
      <ul class="ComponentName-items">
        <li class="ComponentName-item"><a href="ComponentName-itemInner">{{link}}</a></li>
        <li class="ComponentName-item"><a href="ComponentName-itemInner">{{link}}</a></li>
      </ul>
    </div>
  </div>
</section>
```

## JavaScript

### Styleguide

Adhere to the [Google JavaScript Style Guide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml).
