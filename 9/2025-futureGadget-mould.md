/*
```js
*/

const c = "";
let l = '';
var v = `${c} 小于 ${l}`;

console.log(typeof undeclaredVariable);

document.body.appendChild(p);

if (a > 0) {
    result = "positive";
} else {
    result = "NOT positive";
}

const func2 = (x, y) => {
    return 0;
}

let newDiv = document.createElement("div");
newDiv.textContent = "This text is different!";

window.addEventListener("load", (event) => {
  log.textContent += "load\n";
});

switch (foo) {
  case -1:
    console.log("负 1");
    break;
  case 0: // foo 的值匹配这个条件；执行从这里开始
    console.log(0);
  // 忘记了 break！执行穿透
  case 1: // 'case 0:' 中没有 break 语句，所以这个 case 也会执行
    console.log(1);
    break; // 遇到 break，不会继续到 'case 2:'
  case 2:
    console.log(2);
    break;
  default:
    console.log("default");
}

/*
```
*/