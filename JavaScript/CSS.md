---
title: CSS
permalink: JavaScript/CSS
category: JavaScript
parent: JavaScript
layout: default
has_children: false
share: true
shortRepo:

- javascript
- default

---

<br/>

<details markdown="block">                      
<summary>                      
Table of contents                      
</summary>                      
{: .text-delta }                      
1. TOC                      
{:toc}                      
</details>

<br/>

---

# Modify CSS

## Style attribute

### Hide Element

```javascript
element.style.display = "block"; // Show
element.style.display = "inline"; // Show
element.style.visibility = "visible"; // Show
element.style.display = "inline-block"; // Show

element.style.display = "none"; // Hide
element.style.visibility = "hidden"; // Hide
element.style.opacity = 0; // Hide

// hide
element.style.zIndex = -1;
```

## [classList](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList)

```javascript
const div = document.createElement("div");
div.className = "foo";

// our starting state: <div class="foo"></div>
console.log(div.outerHTML);

// use the classList API to remove and add classes
div.classList.remove("foo");
div.classList.add("anotherclass");

// <div class="anotherclass"></div>
console.log(div.outerHTML);

// if visible is set remove it, otherwise add it
div.classList.toggle("visible");

// add/remove visible, depending on test conditional, i less than 10
div.classList.toggle("visible", i < 10);

// false
console.log(div.classList.contains("foo"));

// add or remove multiple classes
div.classList.add("foo", "bar", "baz");
div.classList.remove("foo", "bar", "baz");

// add or remove multiple classes using spread syntax
const cls = ["foo", "bar"];
div.classList.add(...cls);
div.classList.remove(...cls);

// replace class "foo" with class "bar"
div.classList.replace("foo", "bar");
```

## [className property](https://developer.mozilla.org/en-US/docs/Web/API/Element/className)

```javascript
const el = document.getElementById("item");
el.className = el.className === "active"
               ? "inactive"
               : "active";

elm.setAttribute("class", elm.getAttribute("class"));
```

<br/>      
# [RGB to HEX](https://css-tricks.com/converting-color-spaces-in-javascript/  )

```javascript
function RGBToHex(rgb) {
    let sep = rgb.indexOf(",") > -1
              ? ","
              : " ";
    rgb = rgb.substr(4).split(")")[0].split(sep);

    // Convert %s to 0–255
    for (let R in rgb) {
        let r = rgb[R];
        if (r.indexOf("%") > -1) rgb[R] = Math.round((r.substr(0, r.length - 1) / 100) * 255);
        /* Example:      
         75% -> 191      
         75/100 = 0.75, * 255 = 191.25 -> 191      
         */
    }
}
```

# Create a Style element / modify css style sheets

## insert into document head

```javascript
generateRulesAll(tableRef.current).then((css) => {
    const styleElement = document.createElement("style");
    styleElement.innerText = css;
    iframeRef?.current.contentWindow.document.head.appendChild(styleElement);
});
```

## Append new stylesheet to current stylesheets

> [CSSStyleSheet](https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleSheet)

> [AdoptedStyleSheets ](https://developer.mozilla.org/en-US/docs/Web/API/Document/adoptedStyleSheets)
>
> > The adoptedStyleSheets property of the Document interface is used for setting an array of constructed stylesheets to be used by the document.
> >
> > > [ShadowRoot AdoptedStyleSheets](https://developer.mozilla.org/en-US/docs/Web/API/ShadowRoot/adoptedStyleSheets)

```javascript
const extraSheet = new CSSStyleSheet();
extraSheet.insertRule("p { color: green; }");

// Combine the existing sheets and new one
document.adoptedStyleSheets = [...document.adoptedStyleSheets, extraSheet];
```