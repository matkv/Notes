# Enabling extensions in VS Code OSS

Add this to `usr/lib/product.json`:

```
"extensionsGallery": {
    "serviceUrl": "https://marketplace.visualstudio.com/_apis/public/gallery",
    "cacheUrl": "https://vscode.blob.core.windows.net/gallery/index",
    "itemUrl": "https://marketplace.visualstudio.com/items"
}
```

After doing this, all usual extensions should show up when you search for them.