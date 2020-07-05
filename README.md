# VScode配置ESlint+Prettier，实现Typescript代码保存时，自动校验格式并修复
![markdown](https://raw.githubusercontent.com/DCLangX/howToAutoFixTypescript/master/%E6%95%88%E6%9E%9C%E9%A2%84%E8%A7%88.gif "markdown")
## 1、VScode搜索并安装这两个插件
```
ESlint Prettier
```
安装完成之后，按下`ctrl+shit+p`，输入setting.json，选择`首选项：打开设置（json）`回车
在设置中插入如下配置
```
    // eslint配置项，保存时自动修复
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    },
    // 默认使用prettier格式化支持的文件
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    // 自动设定eslint工作区
    "eslint.workingDirectories": [
        { "mode": "auto" }
    ],
```

## 2、为你的项目安装以下插件
```
yarn add eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin prettier eslint-config-prettier eslint-plugin-prettier --dev
```
或者
```
npm install eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin prettier eslint-config-prettier eslint-plugin-prettier --save-dev
```
## 3、新建eslint配置文件
在项目根目录下新建`.eslintrc.js`文件
写入如下内容
```
module.exports = {
  parser: "@typescript-eslint/parser", // 指定ESLint解析器
  parserOptions: {
    sourceType: "module", // 允许使用导入
  },
  extends: [
    "plugin:@typescript-eslint/recommended", // 使用@ typescript-eslint / eslint-plugin中的推荐规则
    "prettier/@typescript-eslint", // 使用eslint-config-prettier禁用一些与Prettier冲突的ESLint规则
    "plugin:prettier/recommended" // 启用eslint-plugin-prettier和eslint-config-prettier，使编辑器显示错误提示，确保这项是扩展数组中的最后一个配置
  ],
  rules: {
    // 放置ESLint规则的位置。可用于覆盖从扩展配置中指定的规则
    // 例如 "@typescript-eslint/explicit-function-return-type": "off",
  },
};
```

## 4、配置Prettier
这步是可选的，如果pretter的默认配置你觉得用着蛋疼，那么你可以在项目根目录下新建`.prettierrc`修改它的配置，下面列举一些常用设置，全部为默认选项，请按需修改
```
{
  "printWidth": 80, //限制每行字符个数
  "tabWidth": 2, //指定每个缩进级别的空格数
  "useTabs": false, //使用制表符而不是空格缩进
  "semi": true, //在语句末尾打印分号
  "singleQuote": false, //使用单引号而不是双引号
  "trailingComma": "es5", //多行时尽可能打印尾随逗号
  "bracketSpacing": true, //在对象文字中的括号之间打印空格
  "arrowParens": "always", //始终给箭头函数的参数加括号
  "htmlWhitespaceSensitivity": "css", //指定HTML文件的全局空格敏感度
  "endOfLine": "lf" //检测换行符类型，如果出现大量换行符报错，可以修改为auto不检测
}
```
更多配置可参考[Pretter文档](https://prettier.io/docs/en/options.html)

##如果还想配置vue、react文件相关的格式化，可以参考下面的说明
<https://github.com/prettier/eslint-config-prettier>


###参考资料
> [Using ESLint and Prettier in a TypeScript Project](https://www.robertcooper.me/using-eslint-and-prettier-in-a-typescript-project)

### End
