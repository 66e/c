/*/*
```js
*/

const fetchCors = async(url, targetElem) => {
    const response = await fetch(url);
    const docData = await response.text();
    const txtSon = decomposTxt(docData);
    console.log(txtSon);
}

const decomposTxt = (txt) => {
    const paraSFromDoc = arrSpliter(txt, '\n###');
    const arr = [];
    for (const elem of paraSFromDoc) {
        const line = arrSpliter(elem, '\n');
        arr.push(line);
    }
    return arr;
}

const arrSpliter = (input, spliter) => {
  const arrOut = input.trim().split(spliter);
    return arrOut;
}

const imageFragment = () => {
  const items = ["item1", "item2", "item3"];
  const fragment = new DocumentFragment();
  
  items.forEach((item) => {
    const myImage = new Image(100, 200);
    myImage.src = items;
    fragment.appendChild(myImage);
});

  const imgLoad = imagesLoaded(fragment);
imgLoad.on( 'always', function() {
  console.log( imgLoad.images.length + ' images loaded' );
  // detect which image is broken
  for ( let i = 0, len = imgLoad.images.length; i < len; i++ ) {
    const image = imgLoad.images[i];
    const result = image.isLoaded ? 'loaded' : 'broken';
    console.log( 'image is ' + result + ' for ' + image.img.src );
  }
});
}

const docUrl = 'https://66e.github.io/j/prideAndP.md';
fetchCors(docUrl);

/*/*
```
*/