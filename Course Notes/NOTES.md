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



<h1>Setting HTMX Attributes Dynamically (On The Client)</h1>
In the previous lecture, you learned how to dynamically generate & set HTMX attributes on the server.

You can also do that on the client, with help of client-side JavaScript.

But there's one important thing to note & keep in mind: Unlike on the server, the client-side code will execute after the page was loaded and therefore after HTMX checked for known attributes.

Therefore, whenever you dynamically set or change HTMX attributes with help of client-side JavaScript code, HTMX will ignore those attributes (or, to be precise: It simply won't detect them).

Hence you must make HTMX aware of those attributes. And you can do that manually, by calling `htmx.process(elementWithNewAttributes)` in your JavaScript code (e.g., right after the code that added an HTMX attribute).

Here's an example:

```
<script>
  const button = document.querySelector("button");
  button.setAttribute("hx-get", "/data");
  htmx.process(button);
</script>
```

`htmx` is a globally available variable that's added by HTMX.

Link to official `htmx.process()` documentation: https://htmx.org/api/#process


This is a good follow-up course, especially if you're working with Django:
https://www.udemy.com/course/full-stack-django