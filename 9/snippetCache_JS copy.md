/*
```js
*/

const createMould = ({
    className,
    click,
    href,
    id,
    localName,
    textContent,
    src,
}) => {
    const tag = document.createElement(localName);
    switch (true) {
        case click !== undefined:
            tag.addEventListener(click || "click", () => {
                console.log(0);
            });
        case className !== undefined:
            tag.className = className;
        case href !== undefined:
            tag.href = href;
        case id !== undefined:
            tag.id = id;
        case textContent !== undefined:
            tag.textContent = textContent;
        case src !== undefined:
            tag.src = src;
    }
return tag;
}

const el = createMould({
    className : 'className',
    click : 'click',
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