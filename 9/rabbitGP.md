/*
```js
*/

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

const jspanel_OL = () => {
    jsPanel.create({content: '<div id="jspContainer"></div>'});
}

const imagesloaded_OL = () => {
    processElem();
}

const processElem = () => {
    const urlS = [
    "https://7ed.net/bing/api?rand=true&size=1024x768", 
    "https://picsum.photos/v2/list", 
    "https://api.7ed.net/bing/api", 
    "https://picsum.photos/536/354"
    ];
    const objS = [];

    const fragment = new DocumentFragment();

urlS.forEach((url) => {
    objS.push({ src: url });

    const li = document.createElement("li");
    li.style.backgroundColor = "#000";
    li.style.backgroundImage = "url('https://s3-us-west-2.amazonaws.com/s.cdpn.io/82/loading.gif')";
    li.style.backgroundPosition = "center center";
    li.style.backgroundRepeat = "no-repeat";
    li.style.borderRadius="4px";
    li.style.display = "block";
    li.style.float = "left";
    li.style.height = "70px";
    li.style.margin="2px 2px 2px 2px";

    const img = new Image(100, 200);
    img.src = url;
    img.style.borderRadius="4px";
    img.style.opacity = 0;
    img.style.maxHeight = "70px";
    img.style.transition = "opacity 0.4s";
    img.addEventListener("click", (e) => {
        const crrntPrnt = e.currentTarget.parentNode;
        const galIdx = [].indexOf.call(crrntPrnt.parentNode.childNodes, crrntPrnt);
        new Fancybox(
            // Array containing gallery items
            objS,
            // Gallery options
            {
                startIndex: galIdx,
            }
        );
    });
    li.appendChild(img);
    fragment.appendChild(li);
});

const imgLoad = imagesLoaded( fragment );
imgLoad.on( 'always', ( instance ) => {
  console.log( imgLoad.images.length + ' in total' );
});
imgLoad.on( 'done', ( instance ) => {
  console.log('DONE  - all images have been successfully loaded');
});
imgLoad.on( 'fail', ( instance ) => {
  console.log('FAIL - all images loaded, at least one is broken');
});
imgLoad.on( 'progress', ( instance, image ) => {
    if ( image.isLoaded ) {
        image.img.style.opacity = 1;
    } else {
        image.img.parentNode.style.backgroundColor = "#000";
        image.img.parentNode.style.backgroundImage = "url('https://s3-us-west-2.amazonaws.com/s.cdpn.io/82/broken.png')";
    }
    const result = image.isLoaded ? 'loaded' : 'broken';
    console.log( '[' + result + '] ' + image.img.src );
});

const jspContainer = document.querySelector("div#jspContainer");
jspContainer.appendChild(fragment);
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
		referElem[iterator].addEventListener("load", () => {
			switch (elemId) {
			case 'jspanel_min_js':
				jspanel_OL();
				break;
            case 'imagesloaded_pkgd_min_js':
				imagesloaded_OL();
				break;
			default:
			}
		});
		document.documentElement.appendChild(referElem[iterator]);
		checkbox[iterator].title = referElem[iterator].id;
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
		console.log('contextmenu');
    });
    return triggerField;
}

const createBar = () => {
    const div = document.createElement('div');
    div.style.position = 'fixed';
    div.style.bottom = '16px';
    div.style.right = '0px';
    div.style.width = '16px';
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