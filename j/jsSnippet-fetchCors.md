/*
```js
*/

const fetchCors = async(url, targetElem) => {
    const response = await fetch(url);
    const docData = await response.text();
    console.log(docData);
}

const docUrl = 'https://fastly.jsdelivr.net/gh/riversun/JSFrame.js/public/index.html';
fetchCors(docUrl);

/*
```
*/