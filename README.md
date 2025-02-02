# melonbox

### 用于创建基于html5的桌面应用，类似于electron，但是体积更小巧，打包应用不到10兆，支持win7系统。

#### melonbox目前有四个版本：
```
melonbox-pro  （内置nodejs支持，开发语言js）
melonbox-max  （内置go语言支持，支持js和go混合代码，开发语言js+go）
melonbox-plus  （支持js代码和静态资源打包，开发语言js+go）
melonbox-lite  （支持dotnet扩展，js可直接调用C#编译的DLL，开发语言js+C#）
```

#### 下载地址：https://github.com/caixiaogua/melonbox/releases

### melonbox-mini说明：
1. net.cs为C#编写的js扩展库，可以自己修改，执行buildcs.bat编译为net.dll
2. index.html中的js可以直接调用net.dll中的类和方法
3. 读写文件可以使用内置的readFile和saveFile函数，也可使用net.dll中的扩展方法
4. 内置sqlite数据库，无需额外依赖便可直接在js中操作sqlite数据库
5. 开发一个桌面应用仅3兆，性能好，效率高，成本低，兼容win7系统
```
//调用dll扩展范例：
//index.html
<script>
// 调用net.dll文件中的方法
xcall('net.Math.Add(44,55)').then(res=>{
    res='通过net.dll扩展类计算的结果: 44+55='+res;
    h2div.innerHTML=res;
});
xcall('net.FS.GetFiles(".")').then(res=>{
    h3div.innerHTML+=res+"<br>";
});
// 操作sqlite数据库
sqlite_init("test.db").then(async db=>{
        let res=await sqlite_query("select * from users");
        h4div.innerHTML="<h3>来自sqlite数据库的数据</h3>";
        h4div.innerHTML+=res.map(x=>JSON.stringify(x)).join("<br>");
});
</script>
```

### melonbox-max说明：
1. 更丰富更强大的api接口函数。
2. 可以在html中执行go语言代码。
3. 具体请参考：https://github.com/caixiaogua/jsgo
```
//调用go语言范例：
//index.html
<script>
jsgo(function(){
  let res=api.goRun(`string(ioutil.ReadFile("package.json"))`); //使用go语言读取文件内容
  return res;
}).then(res=>{
	console.log(res);
	alert(JSON.stringify(res));
});
</script>
```

### melonbox-pro说明：
1. 去除了对.net framework的依赖。
2. 内置nodejs，与nodejs完美融合。
3. 自带mysql和sqlite支持。

```
//index.html
<h4 id="h4div"></h4>
<script>
nodejs(async function(){
    let os=require("os");
    let net=os.networkInterfaces();
    let cpu=os.cpus();
    return {"网卡":net,"处理器":cpu};
}).then(res=>{
    console.log("res", res);
    h4div.innerHTML=JSON.stringify(res);
});
</script>
```
```
//去除窗口标题和最大最小化按钮
xcall(`setWinMode(10)`);
//自动最大化
xcall(`setWinMode(2)`);
//进入全屏
xcall(`setWinMode(3)`);
//设置窗口标题
xcall(`setTitle("标题")`);
//单独禁用最小化按钮
xcall(`setMinBtn(false)`);
//单独禁用最大化按钮
xcall(`setMaxBtn(false)`);
//切换到最小化
xcall(`melonbox.hitMin()`);
//切换到最大化
xcall(`melonbox.hitMax()`);
//关闭窗口
xcall(`melonbox.hitClose()`);
```

### melonbox-lite说明：
1. UI基于微软webview2，稳定可靠，支持最新html5特性。
2. 内置本地文件读写，内置支持mysql和sqlite数据库操作。
3. 如需调用C#编译的DLL，需要.net4.0以上环境，编译命令为“csc.exe /t:library net.cs”
4. 可集成其它后台服务程序，如nodejs，或go开发的后台程序。

### melonbox-plus说明：
1. 基于chrome内核，支持所有最新的html5特性。
2. 基于jsgo，丰富的系统api接口，轻松愉快的开发体验。
3. 内建go语言jit，可使用js和go进行混合开发。
4. 代码可编译加密，可放心地打包发布桌面应用。
5. 绿色环保，没有依赖，无需安装，省心省力。
6. 前后端分离模式，dist目录为前端目录，app.js为后端接口。

#### 欢迎加入QQ群：739721147

#### plus版和max版开发请参考：
https://github.com/caixiaogua/jsgo

#### plus版可编译app.js为app.sox
```
jsgo buildx app.js
```
#### plus版可打包静态资源文件夹（详细使用说明请参考jsgo6.1更新日志）
```
//例如打包static文件夹，生成static.pkg文件
jsgo pack static
```
