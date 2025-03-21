---
title: Actual value
slug: Web/CSS/CSS_cascade/actual_value
page-type: guide
spec-urls:
  - https://www.w3.org/TR/CSS22/cascade.html#actual-value
  - https://drafts.csswg.org/css-cascade-5/#actual-value
---

{{CSSRef}}

The **actual value** of a [CSS](/en-US/docs/Web/CSS) property is the [used value](/en-US/docs/Web/CSS/CSS_cascade/used_value) of that property after any necessary approximations have been applied. For example, a {{glossary("user agent")}} that can only render borders with a whole-number pixel width may round the thickness of the border to the nearest integer.

## Calculating a property's actual value

The {{glossary("user agent")}} performs four steps to calculate a property's actual (final) value:

1. First, the [specified value](/en-US/docs/Web/CSS/CSS_cascade/specified_value) is determined based on the result of [cascading](/en-US/docs/Web/CSS/CSS_cascade/Cascade), [inheritance](/en-US/docs/Web/CSS/CSS_cascade/Inheritance), or using the [initial value](/en-US/docs/Web/CSS/CSS_cascade/initial_value).
2. Next, the [computed value](/en-US/docs/Web/CSS/CSS_cascade/computed_value) is calculated according to the specification (for example, a `span` with `position: absolute` will have its computed `display` changed to `block`).
3. Then, layout is calculated, resulting in the [used value](/en-US/docs/Web/CSS/CSS_cascade/used_value).
4. Finally, the used value is transformed according to the limitations of the local environment, resulting in the actual value.

## Specifications

{{Specifications}}

## See also

- CSS key concepts:
  - [CSS syntax](/en-US/docs/Web/CSS/CSS_syntax/Syntax)
  - [At-rules](/en-US/docs/Web/CSS/CSS_syntax/At-rule)
  - [Comments](/en-US/docs/Web/CSS/CSS_syntax/Comments)
  - [Specificity](/en-US/docs/Web/CSS/CSS_cascade/Specificity)
  - [Inheritance](/en-US/docs/Web/CSS/CSS_cascade/Inheritance)
  - [Box model](/en-US/docs/Web/CSS/CSS_box_model/Introduction_to_the_CSS_box_model)
  - [Layout modes](/en-US/docs/Glossary/Layout_mode)
  - [Visual formatting model](/en-US/docs/Web/CSS/CSS_display/Visual_formatting_model)
  - [Margin collapsing](/en-US/docs/Web/CSS/CSS_box_model/Mastering_margin_collapsing)
  - Values
    - [Initial values](/en-US/docs/Web/CSS/CSS_cascade/initial_value)
    - [Computed values](/en-US/docs/Web/CSS/CSS_cascade/computed_value)
    - [Used values](/en-US/docs/Web/CSS/CSS_cascade/used_value)
    - [Resolved values](/en-US/docs/Web/CSS/resolved_value)
  - [Value definition syntax](/en-US/docs/Web/CSS/CSS_Values_and_Units/Value_definition_syntax)
  - [Shorthand properties](/en-US/docs/Web/CSS/CSS_cascade/Shorthand_properties)
  - {{glossary("Replaced elements")}}
