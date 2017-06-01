## 实现功能

通过操作系统关闭Typora并打开指定文件。（仅在mac上测试了）

## 注意点

同步方法`execSync`的话没有回调。

## 具体代码

```
const exec = require('child_process').exec;
const getIdCMD = 'ps x | grep Typora';
const url = ''; 指定打开的文件路径
exec(getIdCMD, (error, stdout, stderr) => {
    if (error) {
        console.log(error)
        process.exit()
    }
    var i = stdout.indexOf(' ');
    var pid = stdout.substring(0, i);
    const kils = 'kill ' + pid;
    exec(kils, (error, stdout, stderr) => {
        if (error) {
            console.log(error)
        }
        const openCMD = 'open -a Typora  ' + url;
        exec(openCMD, (error, stdout, stderr) => {
            if (error) {
                console.log(error)
            }
        })
    })
})
```

## 代码来源

[git地址](https://github.com/LiuYueKai/Typora2perfect/blob/master/main-process/selectRoot.js)
