# shopify-download-files

## Steps

### 1. Go to files page: https://YOUR_STORE_NAME_HERE.myshopify.com/admin/settings/files?limit=250
### 2. Open the browser JS console.
### 3. Copy and paste the following snippet in the console and hit Enter.
```
const simulateClick = function (elem) {
	const evt = new MouseEvent('click', {
		bubbles: true,
		cancelable: true,
		view: window
	});
	const canceled = !elem.dispatchEvent(evt);
};

function fetchPageAssets() {
    const assets = document.querySelectorAll('[class*="Polaris-Thumbnail"] img');
    assets.forEach(i => {
        if (i.src != "" && !i.src.includes('.svg')) {
            files.push('<img src="' + i.src.replace('_60x60', '') + '">')
        }
    })
}

var files = [];

function downloadListFile() {
    const a = document.createElement('a');
    a.id = 'download-file';
    a.href = 'data:application/octet-stream;base64,' + window.btoa(files.join('\n'));
    a.setAttribute('download', 'shopify-files.html');

    document.querySelector('body').appendChild(a);
    simulateClick(document.querySelector('#download-file'));
}

files.push('<html>\n<body>');
fetchPageAssets();
files.push('</body>\n</html>\n');
downloadListFile();
```

### 4. Save the document
### 5. Open the downloaded document on a new browser tab.
### 6. Save the docuemnt (CMD + S) (CONTROL + S), Make sure you select download complete document, not just html.
### 7. Repeat this step for page 2 of the files page, but reload first before step 1.

#### Note: Multiple downloads will end up on multiple folders when you download them, you can manually combine them on your computer.
