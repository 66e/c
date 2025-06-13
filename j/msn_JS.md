/*
```js
/**/

const retrieveMsn = () => {
    const cpArticle = document.querySelector("cp-article");
    const cpAtcImgS = cpArticle.querySelectorAll("cp-article-image");
    const arr = [];
    const lngt = cpAtcImgS.length;
    for (let i = 0; i < lngt; i++) {
        const img = cpAtcImgS[i].shadowRoot.querySelector(
            "div.article-image-container img.article-image");
        arr.push(img.src);
    }
    return arr;
}

setTimeout(() => {
    console.log(retrieveMsn());
}, 300);

/*
```
/**/