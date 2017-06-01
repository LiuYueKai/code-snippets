## 实现功能

遍历文件夹，并且每个节点创建一个适配ztree的对象，同时只显示md文件。

## 具体代码

```
function readFile(path, pid, filesArr) {
    files = fs.readdirSync(path);
    files.forEach(walk);

    function walk(file) {
        var newPath = path + '/' + file;

        var newNode = {
            pId: pid,
            id: file,
            name: file,
            title: file,
            fileUrl: newPath
        }

        states = fs.statSync(newPath);
        if (states.isDirectory()) {
            readFile(path + '/' + file, file, filesArr);
            filesArr.push(newNode);
        } else {
            var i = file.indexOf('md');
            var l = file.length;
            if (i == (l - 2)) {
                filesArr.push(newNode);
            }
        }
    }
}
```

## 代码来源

[git地址](https://github.com/LiuYueKai/Typora2perfect/blob/master/main-process/selectRoot.js)
