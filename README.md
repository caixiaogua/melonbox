# melonbox（原melonUI）

### 用于创建基于html5的桌面应用，类似于electron

### melonbox特点：
1. 基于chrome内核，支持所有最新的html5特性。
2. 基于jsgo，丰富的系统api接口，轻松愉快的开发体验。
3. 内建go语言jit，可使用js和go进行混合开发。
4. 代码可编译加密，可放心地打包发布桌面应用。
5. 绿色环保，没有依赖，无需安装，省心省力。

#### 开发方式：
1. 下载melonbox.zip并解压
2. 编辑app.js
3. 执行melonbox.exe启动demo

#### 欢迎加入QQ群：739721147

#### app.js为应用入口文件，开发请参考：
https://github.com/caixiaogua/jsgo

#### 可编译app.js为app.sox
```
jsgocore buildx app.js
```
#### 可打包静态资源文件夹（详细使用说明请参考jsgo6.1更新日志）
```
//例如打包css文件夹，生成css.pkg文件
jsgocore pack css
```
