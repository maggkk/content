---
title: "Document: exitFullscreen() method"
short-title: exitFullscreen()
slug: Web/API/Document/exitFullscreen
page-type: web-api-instance-method
browser-compat: api.Document.exitFullscreen
---

{{ApiRef("Fullscreen API")}}

The {{domxref("Document")}} method
**`exitFullscreen()`** requests that the element on this
document which is currently being presented in fullscreen mode be taken out of
fullscreen mode, restoring the previous state of the screen. This usually
reverses the effects of a previous call to {{domxref("Element.requestFullscreen()")}}.

## Syntax

```js-nolint
exitFullscreen()
```

### Parameters

None.

### Return value

A {{jsxref("Promise")}} which is resolved once the {{Glossary("user agent")}} has
finished exiting fullscreen mode. If an error occurs while attempting to exit
fullscreen mode, the `catch()` handler for the promise is called.

## Examples

This example causes the current document to toggle in and out of a fullscreen
presentation whenever the mouse button is clicked within it.

```js
document.onclick = (event) => {
  if (document.fullscreenElement) {
    document
      .exitFullscreen()
      .then(() => console.log("Document Exited from Full screen mode"))
      .catch((err) => console.error(err));
  } else {
    document.documentElement.requestFullscreen();
  }
};
```

> [!NOTE]
> For a more complete example, see the
> [`Element.requestFullscreen()` examples](/en-US/docs/Web/API/Element/requestFullscreen#examples).

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [Fullscreen API](/en-US/docs/Web/API/Fullscreen_API)
- [Guide to the Fullscreen API](/en-US/docs/Web/API/Fullscreen_API/Guide)
- {{ domxref("Element.requestFullscreen()") }}
- {{ domxref("Document.fullscreenElement") }}
- {{ cssxref(":fullscreen") }} and {{cssxref("::backdrop")}}
- The {{HTMLElement("iframe")}} [`allowfullscreen`](/en-US/docs/Web/HTML/Reference/Elements/iframe#allowfullscreen)
  attribute
