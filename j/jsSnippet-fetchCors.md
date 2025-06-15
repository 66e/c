/*
```js
*/

const parseURL = ($string) => {
    const __urlRegex = /(\b(https?|ftp|file):\/\/[-A-Z0-9+&@#\/%?=~_|!:,.;]*[-A-Z0-9+&@#\/%=~_|])/ig;
    const __imgRegex = /\.(?:jpe?g|gif|png)$/i;
    const pRompt6Exe = /^\#6\/p\/\w+$/i;
    const regTestStr = __urlRegex.test($string);
    if (regTestStr) {
        switch (true) {
            case __imgRegex.test($string):
                return "img";
                break;
            
            default:
                return "a";
        }
    } else if (pRompt6Exe.test($string)) {
        return "pRompt6Exe";
    } else {
        return "p";
    }
}

const arraySparse = [
    "https://www.mojidict.com/search",
    "https://img.acgn.cc/img/2600/2550/10.jpg",
    /* empty */,
    "Kitzuki Kokone",
    "#6/p/s",
];

arraySparse.forEach((element) => {
    const number = parseURL(element);
    console.log(number);
});

/*
```
*/