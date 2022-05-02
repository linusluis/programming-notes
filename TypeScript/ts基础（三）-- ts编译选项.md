
## 1、自动编译文件

编译文件时，使用-w指令后，TS编译器会自动监视文件的变化，并在文件发生变化时对文件进行重新编译。  
示例：`tsc xxx.ts -w`

## 2、自动编译整个项目

如果直接使用tsc指令，则可以自动将当前项目下的所有ts文件编译为js文件。  

但是能直接使用tsx命令的前提是，要先在项目根目录下创建一个ts的配置文件tsconfig.json。   

tsconfig.json是一个JSON文件，添加配置文件后，只需tsc命令即可完成对整个项目的编译。

配置选项：
1. include
> - 用来指定那些ts文件需要被编译
> - 默认值：["**/*"]
> - 说明：“**”表示任意目录，“*”表示任意文件
> - 示例：
>```json
> "include":["src/**/*","tests/**/*"]
> ```
> - 上述示例中，所有src目录和tests目录下的文件都会被编译
- exclude
- extends
- files

2. exclude
> - 不需要被编译的文件目录，一般不需要设置
> - 默认值：["node_moudles","brwer_components","jspm_packages"]
> - 示例：
> ```json
> "exclude":["./src/hello/**/*"]
> ```
> 上述示例中,src下hello目录下的文件都不会被编译

3. extends
> - 定义被继承的配置文件
> - 示例：
> ```json
> "extends":"./configs/base"
>```
> - 上述示例中，当前配置文件中会自动包含config目录下base.json中的所有配置信息。

4. files
> - 指定被编译文件的列表，只有需要编译文件少时才会用到
> - 示例：
> ```json
> "files": [
>    "core.ts",
>    "sys.ts",
>    "types.ts",
>    "scanner.ts",
>    "parser.ts",
>    "utilities.ts",
>    "binder.ts",
>    "checker.ts",
>    "tsc.ts"
>  ]
> ```
> - 上述示例中，列表中的文件都会被TS编译器所编译

5. compilerOptions
> - 编译选项是配置文件中非常重要也比较复杂的配置选项
> - 在compilerOptions中包含多个子选项，用来完成对编译的配置
> - 子选项
> 1.  target
>> 用来指定ts被编译为的ES的版本
>> 可选值：ES3（默认）、ES5、ES6/ES2015、ES7/ES2016、ES2017、ES2018、ES2019、ES2020、ESNext
>> 示例：
>>```json
>> "compilerOptions":{
>>      "target":"ES6"   
>> }
>>```
>> 如上设置，我们所编写的ts代码将会被编译为ES6版本的js代码
> 2. lib
>>指定代码运行时所包含的库（宿主环境）
>>可选值：ES5、ES6/ES2015、ES7/ES2016、ES2017、ES2018、ES2019、ES2020、ESNext、DOM、WebWorker、ScriptHost ......
>> 示例：
>>```json
>>"compilerOptions": {
>>    "target": "ES6",
>>    "lib": ["ES6", "DOM"],
>>}
>>```
> 3. module
>>设置编译后代码使用的模块化系统
>>可选值：CommonJS、UMD、AMD、System、ES2020、ESNext、None
>>示例：
>>```json
>>"compilerOptions": {
>>    "module": "CommonJS"
>>}
>>```
> 4. outDir
>>编译后文件的所在目录
>>默认情况下，编译后的js文件会和ts文件位于相同的目录，设置outDir后可以改变编译后文件的位置
>>示例：
>>```json
>>"compilerOptions": {
>>    "outDir": "dist"
>>}
>>```
>>设置后编译后的js文件将会生成到dist目录
>>
>5. rootDir
>>指定代码的根目录，默认情况下编译后文件的目录结构会以最长的公共目录为根目录，通过rootDir可以手动指定根目录
>>示例：
>>```json
>>"compilerOptions": {
>>    "rootDir": "./src"
>>}
>>```
> 6. allowJs
>>是否对js文件编译，默认是false
> 7. checkJs
>>是否对js文件进行检查,默认是false
>>示例：
>>```json
>>"compilerOptions": {
>>    "allowJs": true,
>>    "checkJs": true
>>}
>>```
>8. removeComments
>>是否删除注释
>>默认值：false
> 9. noEmit
>>不对代码进行编译
>>默认值：false
>10. noEmitOnError
>>当有错误时不生成编译后的文件
> 10. sourceMap
>>是否生成sourceMap
>>默认值：false
> 11. 严格检查
>>strict： 启用所有的严格检查，默认值为true，设置后相当于开启了所有的严格检查
>>alwaysStrict：总是以严格模式对代码进行编译
>>noImplicitAny：禁止隐式的any类型
>>noImplicitThis：禁止类型不明确的this
>>strictBindCallApply：严格检查bind、call和apply的参数列表
>>strictFunctionTypes：严格检查函数的类型
>>strictNullChecks：严格的空值检查
>>strictPropertyInitialization：严格检查属性是否初始化
>12. 额外检查
>>noFallthroughCasesInSwitch：检查switch语句包含正确的break
>>noImplicitReturns：检查函数没有隐式的返回值
>>noUnusedLocals：检查未使用的局部变量
>>noUnusedParameters：检查未使用的参数
>13. 高级
>>allowUnreachableCode：检查不可达代码
>> 可选值：true：忽略不可达代码 ；false：不可达代码将引起错误  
>>noEmitOnError：有错误的情况下不进行编译
>>默认值：false

