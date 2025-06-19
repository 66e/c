/*
```js
*/

const createMould = ({
    addEventListener,
    appendChild,
    className,
    href,
    id,
    localName,
    textContent,
    src,
}) => {
    const tag = document.createElement(localName);
    tag.addEventListener(addEventListener||"load", () => {
        console.log(typeof 0);
    });
    tag.className = className;
    tag.href = href;
    tag.id = id;
    tag.textContent = textContent;
    tag.src = src;
    document.body.appendChild(tag);
    return tag;
}

const el = createMould({
    addEventListener : 'addEventListener',
    appendChild : 'body',
    className : 'className',
    href : 'href',
    id : 'id',
    localName : 'div',
    textContent : 'textContent',
    src : 'src',
});
document.body.appendChild(el);

/*
```
*/