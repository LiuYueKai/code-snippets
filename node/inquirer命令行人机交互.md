## 实现功能

人机交互根据用户选择进行不同操作

## 注意点

type的几种类型：
* list：单选
* checkbox: 复选
* input: 输入
更多类型及参数说明参照[官方说明](https://github.com/sboudrias/Inquirer.js)
## 具体代码

```
const inquirer = require('inquirer');

request({
    url: 'https://api.github.com/users/easy-templates/repos',
    headers: {
        'User-Agent': 'easy templates'
    }
}, function(err, res, body) {
    if (err) console.log(err);
    var requestBody = JSON.parse(body);
    if (Array.isArray(requestBody)) {
        requestBody.forEach(function(repo, index) {
            repoNameData.push(`${repo.name} - ${repo.description}`);
        });
        // 人机交互
        inquirer.prompt([{
            type: 'list',
            name: 'selectRepo',
            message: 'Please select :',
            choices: repoNameData
        }]).then(function(answers) {
            var selectName = answers.selectRepo.split(' - ')[0];
            console.log('选择的模板为' + selectName);
        });
    }
});
```

## 代码来源

[git地址](https://github.com/LiuYueKai/easy-template/blob/master/lib/init.js)
