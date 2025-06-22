# comnt - template content using block-annotated comments

A small, simple, human-friendly way to manage template regions using 
**standard comment syntax** — no weird symbols, no broken files, no preprocessing 
to view your code in a browser.

Source templates remain fully functional working HTML and JavaScript code that can be 
opened, viewed, and tested directly in browsers. 

One huge practical benefit: you can inject actual JavaScript-ready values from Python—
not just strings or you can refer to javascript functions defined elsewhere. 
That means you don’t need to wrap your data in quotes and then call 
`JSON.parse(...)` on the frontend, like you often do with Jinja2.

With Jinja2 we need:
```js
const user = JSON.parse('{{ user_data | tojson | safe }}');
or even sometimes:
const user = JSON.parse(JSON.stringify( '{{ user_data | tojson | safe }}'));
```
With comnt:
```js
const data = /*[user_data*/ {'name' : 'Alice' }
/*user_data]*/;
```

## Two supported tag-comment styles:
 HTML:
```html
<p>
<!--[user_info-->
User Placeholder
<!--user_info]-->
</p>
```
Javascript/css:
```javascript
/*[tag_name*/
const arr_to_change = [0,1]
/*tag_name]*/
```

These files stay 100% valid — editable and previewable in browser.

* **Designer and developer see exactly the same**.
* No regex – pure string methods
* Frontend-friendly – what devs and designers see is what they get
* Easy on the eyes – clean [tag_name] blocks


## Philosophy
Logic-less templates in general is clear separation of design and data.<br>
Inspired by CSS-Tricks: Class Up! Templates, Not Content — the idea is to isolate dynamic logic in comments, keeping your markup clean and maintainable
https://css-tricks.com/class-up-templates-not-content/

### Example use
```py
import comnt
template = """
  <!--[title-->
    Title to be replaced
  <!--title]-->
"""
output = render(template, {"title": "A new title"})
print(output)
```

MIT licence.
