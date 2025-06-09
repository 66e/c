/*
```js
*/

// ==UserScript==
// @name         referHub-053
// @namespace    https://bbs.tampermonkey.net.cn/
// @version      0.1.0
// @description  try to take over the world!
// @author       You
// @match        *://*/*
// ==/UserScript==

(() => {
    'use strict';

const uniqueLauncher = () => {
    const triggerExist = document.querySelector('div#triggerField');
    triggerExist === null ? preprocessPrecast() :
    console.log('already entity');
}

const appendRefer = (urlFile) => {
    const fileExtension = urlFile.match(/\.[^/.]+$/);
    const referElem = createByExtens(urlFile, fileExtension[0]);
    const fileName = urlFile.match(/[^\/=\b]+(?=\.[^\/.]*$)/)[0];
    referElem.id = fileName.replace(/\./g,'_')
    + fileExtension[0].replace(/\./g,'_');
    return referElem;
}

const createByExtens = (urlFile, fileExtens) => {
    switch (fileExtens) {
        case '.js':
            const scriptRefer = document.createElement('script');
            scriptRefer.src = urlFile;
            return scriptRefer;
        case '.css':
            const linkRefer = document.createElement('link');
            linkRefer.href = urlFile;
            linkRefer.setAttribute('rel', 'stylesheet');
            return linkRefer;
        default:
            console.log(fileExtens);
            break;
    }
}

const loadJsP = () => {
    jsPanel.create({content: '<div id="aplayer"></div>'});
}

const func2 = (x, y) => {
  return x + y;
}

const preprocessPrecast = () => {
    const trigger = createTrigger();
    const bar = createBar();
    trigger.addEventListener('mouseover', () => {
        bar.style.display = 'block';
    });
    trigger.appendChild(bar);
    const button = document.createElement('button');
    button.textContent = 'x';
    button.style.width = '16px';
    button.style.height = '16px';
    button.addEventListener('mouseup', () => {
        trigger.remove();
    });
    bar.appendChild(button);

    const referUrl = [
        'https://jspanel.de/jspanel/dist/jspanel.min.css',
        'https://jspanel.de/jspanel/dist/jspanel.min.js',
        'https://unpkg.com/imagesloaded@5/imagesloaded.pkgd.min.js',
        'https://cdnjs.cloudflare.com/ajax/libs/fancyapps-ui/5.0.36/fancybox/fancybox.min.css',
        'https://cdnjs.cloudflare.com/ajax/libs/fancyapps-ui/5.0.36/fancybox/fancybox.umd.min.js'
    ];
    const checkbox = [];
    const referElem = [];
    const boolean = [];

    const referReady = (iterator) => {
		referElem[iterator] = appendRefer(referUrl[iterator]);
		const elemId = referElem[iterator].id;
		window.addEventListener("load", (event) => {
			switch (elemId) {
                case 'jspanel_min_js':
                    loadJsP();
                    break;
                case 'jsframe_js':
                    loadAsyncJ();
                    break;
                case 'APlayer_min_js':
                    loadAsyncA();
                    break;
                default:
                    console.log(elemId);
			}
		});
		document.documentElement.appendChild(referElem[iterator]);
		checkbox[iterator].title = referElem[iterator].id;
		console.log('referReady');
	}

    for (let i = 0; i < referUrl.length; i++) {
        checkbox[i] = createCheckbox();
        const label = document.createElement('label');
        label.textContent = i;
        bar.appendChild(label);
        bar.appendChild(checkbox[i]);
        boolean[i] = localStorage.getItem('checkbox' + i);
        if ( boolean[i] === 'true' ) {
            referReady(i);
        }
        checkbox[i].checked = boolean[i] === 'true';
        checkbox[i].addEventListener("change", () => {
            if (checkbox[i].checked) {
                referReady(i);
            } else {
                referElem[i].remove();
            }
            localStorage.setItem('checkbox' + i, (checkbox[i].checked));
        });
    }
    document.body.appendChild(trigger);
}

const createTrigger = () => {
    const triggerField = document.createElement('div');
    triggerField.style.position = 'fixed';
    triggerField.style.zIndex = 801;
    triggerField.id = 'triggerField';
    triggerField.style.bottom = '0px';
    triggerField.style.right = '0px';
    triggerField.style.width = '16px';
    triggerField.style.height = '16px';
    triggerField.style.backgroundColor = '#ccc';
    triggerField.addEventListener('contextmenu', () => {
        
    });
    return triggerField;
}

const createBar = () => {
    const div = document.createElement('div');
    div.style.position = 'fixed';
    div.style.bottom = '16px';
    div.style.right = '0px';
    div.style.width = '16px';
    div.style.height = '160px';
    div.style.backgroundColor = '#ccc';
    div.style.display = 'none';
    div.addEventListener('mouseleave', () => {
        div.style.display = 'none';
    });
    return div;
}

const createCheckbox = () => {
    const check = document.createElement('input');
    check.type = 'checkbox';
    check.style.margin = '0';
    return check;
}

if (document.body) {
    uniqueLauncher();
} else {
    document.addEventListener("DOMContentLoaded", () => {
        uniqueLauncher();
    });
}

    // Your code here...
})();

/*
```
*/