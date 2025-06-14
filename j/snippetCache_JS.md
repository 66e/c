/*
```js
*/

const generateUnit = (txtIn) => {
    const trgtContainer = document.querySelector("div#containErNT");
    const unit = loadFan( txtIn );
    if (trgtContainer) {
        trgtContainer.appendChild(unit);
    } else {
        jsPanel.create({
        callback: (panel) => {
            panel.content.appendChild(unit);
        },
        theme: 'primary',
    });
    }
}

/*
```
*/