# shopify-download-files

## Steps

### 1. Go to files page: https://YOUR_STORE_NAME_HERE.myshopify.com/admin/settings/files?limit=250
### 2. Open the browser JS console.
### 3. Copy and paste the following snippet in the console.
```var simulateClick = function (elem) {
	var evt = new MouseEvent('click', {
		bubbles: true,
		cancelable: true,
		view: window
	});
	var canceled = !elem.dispatchEvent(evt);
};

function fetchPageAssets() {
    var assets = document.querySelectorAll('[class*="Polaris-Thumbnail"] img');
    assets.forEach(i => {
        if (i.src != "" && !i.src.includes('.svg')) {
            files.push('<img src="' + i.src.replace('_60x60', '') + '">')
        }
    })
}

var files = [];

function downloadListFile() {
    var a = document.createElement('a')
    a.id = 'download-file';
    a.href = 'data:application/octet-stream;base64,' + window.btoa(files.join('\n'));
    a.setAttribute('download', 'shopify-files.html');

    console.log(a);
    document.querySelector('body').appendChild(a);
    simulateClick(document.querySelector('#download-file'));

}

files.push('<html>\n<body>')
fetchPageAssets()
files.push('</body>\n</html>\n')
downloadListFile()```

### 4.
