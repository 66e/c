/*
```js
*/

const parseURL = ($string, param) => {
    const __urlR = "((https?|ftp|file):\/\/|(www|ftp)\.)[-A-Z0-9+&@#\/%?=~_|$!:,.;]*[A-Z0-9+&@#\/%=~_|$]";
    const __imgR = "\.(?:img|jpe?g|gif|png)";
    const urlRegex = new RegExp(__urlR, "i");
    const imgRegex = new RegExp(__imgR, "i");
    const imgWURegex = new RegExp(__urlR + __imgR, "i");
    const pRompt6Exe = /^\#6\/p\/\w+$/i;
    const regTestStr = urlRegex.test($string);
    if (regTestStr) {
        switch (true) {
            case imgRegex.test($string):
                if (param) {
                    const trimmed = $string.match(imgWURegex)[0];
                    return trimmed;
                }
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
    "https://img-s.msn.cn/tenant/amp/entityid/AA1GL9Gi.img?w=534&h=300&m=6",
    "#6/p/s",
];

arraySparse.forEach((element) => {
    const number = parseURL(element);
    console.log(number);
});

/*
```
*/