<h1>hx-trigger: Advanced Settings</h1>

`hx-trigger` is an HTMX attribute you often don't need to add - because the default triggers (e.g., `submit` for `<form>`s, `click` for most other elements) often are exactly what you want.

But it's worth noting that you can actually not just use hx-trigger to change the event that triggers a request. Instead, you can also configure how often the event triggers the request, that some other element should trigger the request or that some "indirect" event (e.g., the element being scrolled into view) should trigger the request.

For example, you can ensure that only the first click on a button loads data by adding the once modifier to hx-trigger:

```
<button hx-get="/data" hx-trigger="click once">
    Load Data
</button>
```
You could also add a delay until the request is sent:

```
<button hx-get="/data" hx-trigger="click delay:1s">
    Load Data
</button>
```
Or you could change the element that triggers the request:

```
<button>Load Data</button>
<div hx-get="/data" hx-trigger="click from:previous button">
    Nothing there :(
</div>
```
As mentioned, you can also trigger the request once the element is scrolled into the viewport:
```
<div hx-get="/data" hx-trigger="revealed">
    Nothing there :(
</div>
```
You find a complete list of all the modifiers & variations in the official docs: https://htmx.org/docs/#triggers

And, of course, you'll also see hx-trigger (with more advanced configuration) in action later in the course.