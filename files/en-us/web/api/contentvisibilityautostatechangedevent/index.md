---
title: ContentVisibilityAutoStateChangedEvent
slug: Web/API/ContentVisibilityAutoStateChangedEvent
page-type: web-api-interface
tags:
  - Interface
  - Reference
browser-compat: api.ContentVisibilityAutoStateChangedEvent
---

{{APIRef("CSS Containment")}}

The **`ContentVisibilityAutoStateChangedEvent`** interface of the [CSS Containment Module Level 2](https://www.w3.org/TR/css-contain-2/#content-visibility-auto-state-changed) is the event object for the {{domxref("element/contentvisibilityautostatechanged_event", "contentvisibilityautostatechanged")}} event, which fires on any element with {{cssxref("content-visibility", "content-visibility: auto")}} set on it when it starts or stops being [relevant to the user](/en-US/docs/Web/CSS/CSS_Containment#relevant_to_the_user) and [skipping its contents](/en-US/docs/Web/CSS/CSS_Containment#skips_its_contents).

While the element is not relevant (between the start and end events), the user agent skips an element's rendering, including layout and painting.
This can significantly improve page rendering speed.
The {{domxref("element/contentvisibilityautostatechanged_event", "contentvisibilityautostatechanged")}} event provides a way for an app's code to also start or stop rendering processes (e.g. drawing on a {{htmlelement("canvas")}}) when they are not needed, thereby conserving processing power.

Note that even when hidden from view, element contents will remain semantically relevant (e.g. to assistive technology users), so this signal should not be used to skip significant semantic DOM updates.

{{InheritanceDiagram}}

## Constructor

- {{domxref("ContentVisibilityAutoStateChangedEvent.ContentVisibilityAutoStateChangedEvent", "ContentVisibilityAutoStateChangedEvent()")}} {{Experimental_Inline}}
  - : Creates a new `ContentVisibilityAutoStateChangedEvent` object instance.

## Instance properties

_Inherits properties from its parent, {{DOMxRef("Event")}}._

- {{domxref("ContentVisibilityAutoStateChangedEvent.skipped", "skipped")}} {{ReadOnlyInline}} {{Experimental_Inline}}
  - : Returns `true` if the user agent is skipping the element's rendering, or `false` otherwise.

## Examples

```js
const canvasElem = document.querySelector('canvas');

canvasElem.addEventListener('contentvisibilityautostatechanged', stateChanged);
canvasElem.style.contentVisibility = "auto";

function stateChanged(event) {
  if (event.skipped) {
    stopCanvasUpdates(canvasElem);
  } else {
    startCanvasUpdates(canvasElem);
  }
}

// Call this when the canvas updates need to start.
function startCanvasUpdates(canvas) {
  // …
}

// Call this when the canvas updates need to stop.
function stopCanvasUpdates(canvas) {
  // …
}
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- The {{domxref("element/contentvisibilityautostatechanged_event", "contentvisibilityautostatechanged")}} event
- [CSS Containment](/en-US/docs/Web/CSS/CSS_Containment)
- The {{cssxref("content-visibility")}} property
- The {{cssxref("contain")}} property
