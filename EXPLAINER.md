# Proposal
Directory download functionality could be added using existing primitives with relatively little additional API surface area.

# `webkitRelativePath`
`File.webkitRelativePath` is supported by most major browsers and enables a flattened view of directory structure. Currently, though, this path can only be populated when the user uploads a directory. Adding a `path` property to the `File` constructor would allow sites to create their own directory structure without introducing any new primitives to the web platform.

# `DirectoryEntry`
`DirectoryEntry` recently has been supported by all major browsers. This primitive already enables construction of a tree-view directory structure.

# `Navigator.saveDirectory()`
The primary missing piece is a way to save the constructed directory objects. Calling `Navigator.saveDirectory()` would behave the same way as saving a file does in browsers today. A "Save as..." dialog could be opened, the directory could be automatically saved to Downloads, the user could rename the directory, etc.

`Navigator.saveDirectory()` could accept a list of `File` objects, a `DirectoryEntry`, or both.

# Example code
__Using webkitRelativePath__
```javascript
file1 = new File([contents1], 'myFile.txt');
file2 = new File([contents2], 'pic.jpg', { path: 'images' });
navigator.saveDirectory([file1, file2], 'dirName');
```

__Using `DirectoryEntry`__
```javascript
let myDir = fs.root.getDirectory('dirName', {create:true}, dir => {
    dir.getDirectory('images', {create:true}, subDir => {
        subDir.getFile('pic.jpg', {create:true}, file => {
            myDir.getFile('myFile.txt', {create:true} otherFile => {
                navigator.saveDirectory(myDir, 'dirName');
            });
        });
    });
});
```
