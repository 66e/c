/*
```js
*/

const fetchCors = async(url, targetElem) => {
    const response = await fetch(url);
    const docData = await response.text();
    document.write(docData);
}

const docUrl = 'https://66e.github.io/9/imgsLoad5-Progres_html.md';
fetchCors(docUrl);

/*
```
*/