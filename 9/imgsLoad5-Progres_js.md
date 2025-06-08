/*
```js
*/

const fetchCors = async(url, targetElem) => {
    const response = await fetch(url);
    const docData = await response.text();
    document.write(docData);
}

const docUrl = 'imgsLoad5-Progres_html.md';
fetchCors(docUrl);

/*
```
*/