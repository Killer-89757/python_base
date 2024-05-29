# Fiddler插件安装及使用

前言：

   下面是一些能够对调试起到帮助的插件，没有用过的小伙伴可以试试

------

一、编程猫调试插件

**1. 插件安装**

下载完插件之后打开插件文件夹，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFvX6vg3keoUXrNb9R6_TEhQdC5z2-838fe6.png)

找到**Fiddler**安装目录下的**Scripts**，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFgIYqFLU1cPOynzEKQr_tYFTCuDA-300cb0.png)

将插件中的所有文件全部复制到该文件夹 （我这里是已经复制过之后的），然后打开**Fiddler**就可以看到调试插件了，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFjijkuymr8QC9HdwvqTsXC3mlh5p-5bde65.png)

**2. 插件使用**

这里以**注入Hook**为例，它里面自带了一个**cookie**的**Hook**，如果不指定网站的话，我们只需要吧上面默认填的网址给去掉，然后点击**开启**就行了，为了能够断住，可以在代码里面加上**debugger**，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFhgOe2zHvvLonD6sK_osv8mFwCFD-ae94ed.png)

之后回到浏览器中打开控制台，然后打开目标网站就会发现断住了，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFsOyl4Dr0AS290Osp02NJWUp8QqY-6a2848.png)

还有数据加解密等功能，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFsRIyGZ7-ji7_V84TOLPswK2rMXw-b69c09.png)

其余的功能大家可以自行尝试下。

## 二、Fiddler抓包一键生成调试代码

项目开源地址：https://github.com/quicktype/quicktype

1. 解压文件，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFlNgoexBkOTkrSmyyDn3ePAIUDUe-04eb0b.png) 2. 将刚才解压的文件放到Fiddler目录下，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFvHP-rRImAkZUoAa6DCXQpF914jz-4bd80a.png)

3. 打开Fiddler，之后打开脚本编辑器如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFoLnHmJddQ-OJQNwKDUjUr_rcsJX-bbe955.png)

将里面的代码复制到一个空白的地方，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFgkI5ibh8DrSRlw9szUlkQ7HyA77-49de10.png)

3. 将以下代码复制到上面的代码中

```JS
public static RulesOption("关闭请求体转代码", "生成代码")
 var m_DisableReuqest: boolean = false;

 public static RulesOption("关闭返回体转代码", "生成代码")
 var m_DisableResponse: boolean = false;
   
 public static ContextAction("C#-httpclient", "生成代码")
 function do1(arrSess: Session[]) {  doStar(arrSess, "csharp","httpclient"); }
 public static ContextAction("C#-restsharp", "生成代码")
 function do2(arrSess: Session[]) { doStar(arrSess, "csharp","restsharp"); }

 public static ContextAction("Java-okhttp", "生成代码")
 function do3(arrSess: Session[]) {  doStar(arrSess, "java","okhttp"); }
 public static ContextAction("Java-asynchttp", "生成代码")
 function do4(arrSess: Session[]) {  doStar(arrSess, "java","asynchttp"); }
 public static ContextAction("Java-nethttp", "生成代码")
 function do5(arrSess: Session[]) {  doStar(arrSess, "java","nethttp"); }
 public static ContextAction("Java-unirest", "生成代码")
 function do6(arrSess: Session[]) {  doStar(arrSess, "java","unirest"); }

 public static ContextAction("Kotlin-okhttp", "生成代码")
 function do7(arrSess: Session[]) {  doStar(arrSess, "kotlin","okhttp"); }
   
 public static ContextAction("JavaScript-xhr", "生成代码")
 function do8(arrSess: Session[]) {  doStar(arrSess, "javascript","xhr"); }
 public static ContextAction("JavaScript-jquery", "生成代码")
 function do9(arrSess: Session[]) {  doStar(arrSess, "javascript","jquery"); }
 public static ContextAction("JavaScript-fetch", "生成代码")
 function do10(arrSess: Session[]) {  doStar(arrSess, "javascript","fetch"); }
 public static ContextAction("JavaScript-axios", "生成代码")
 function do11(arrSess: Session[]) {  doStar(arrSess, "javascript","axios"); }
  
 public static ContextAction("Node-native", "生成代码")
 function do12(arrSess: Session[]) {  doStar(arrSess, "node","native"); }
 public static ContextAction("Node-request", "生成代码")
 function do13(arrSess: Session[]) {  doStar(arrSess, "node","request"); }
 public static ContextAction("Node-fetch", "生成代码")
 function do14(arrSess: Session[]) {  doStar(arrSess, "node","fetch"); }
 public static ContextAction("Node-axios", "生成代码")
 function do15(arrSess: Session[]) {  doStar(arrSess, "node","axios"); }   
 public static ContextAction("Node-unirest", "生成代码")
 function do16(arrSess: Session[]) {  doStar(arrSess, "node","unirest"); } 
 
 public static ContextAction("Python3-http.client", "生成代码")
 function do17(arrSess: Session[]) {  doStar(arrSess, "python","python3"); }
 public static ContextAction("Python-requests", "生成代码")
 function do18(arrSess: Session[]) {  doStar(arrSess, "python","requests"); }
   
 public static ContextAction("ObjectiveC-nsurlsession", "生成代码")
 function do19(arrSess: Session[]) {  doStar(arrSess, "objc","nsurlsession"); }

 public static ContextAction("Ruby-net::http", "生成代码")
 function do20(arrSess: Session[]) {  doStar(arrSess, "ruby","native"); }

 public static ContextAction("Swift-nsurlsession", "生成代码")
 function do21(arrSess: Session[]) {  doStar(arrSess, "swift","nsurlsession"); }
   
 public static ContextAction("powershell-webrequest", "生成代码")
 function do22(arrSess: Session[]) {  doStar(arrSess, "powershell","webrequest"); }
 public static ContextAction("powershell-restmethod", "生成代码")
 function do23(arrSess: Session[]) {  doStar(arrSess, "powershell","restmethod"); }

 public static ContextAction("Shell-curl", "生成代码")
 function do24(arrSess: Session[]) {  doStar(arrSess, "shell","curl"); }
 public static ContextAction("Shell-httpie", "生成代码")
 function do25(arrSess: Session[]) {  doStar(arrSess, "shell","httpie"); }
 public static ContextAction("Shell-wget", "生成代码")
 function do26(arrSess: Session[]) {  doStar(arrSess, "shell","wget"); }
  
 public static ContextAction("Go-NewRequest", "生成代码")
 function do27(arrSess: Session[]) { doStar(arrSess, "go","native"); }
   
 public static ContextAction("Clojure-clj_http", "生成代码")
 function do28(arrSess: Session[]) { doStar(arrSess, "clojure","clj_http"); }

 public static ContextAction("C-Libcurl", "生成代码")
 function do29(arrSess: Session[]) { doStar(arrSess, "c","libcurl"); }
 
 public static ContextAction("PHP-curl", "生成代码")
 function do30(arrSess: Session[]) {  doStar(arrSess, "php","curl"); }
 public static ContextAction("PHP-http1", "生成代码")
 function do31(arrSess: Session[]) {  doStar(arrSess, "php","http1"); }
 public static ContextAction("PHP-http2", "生成代码")
 function do32(arrSess: Session[]) {  doStar(arrSess, "php","http2"); }  
  
 public static function doStar(oSessions: Session[], target: String,client:String) {
     //注意看这里，请下载我给的这2个exe并替换成你电脑中正确的目录
  var httpsnippet = "E:\\workspace\\github\\test\\httpsnippet.exe";
  var quicktype = "E:\\workspace\\github\\test\\quicktype.exe";
  var oExportOptions = FiddlerObject.createDictionary(); 
  var tempPath2 = System.IO.Path.Combine(System.IO.Path.GetTempPath(), "fiddler.har");
  if(System.IO.File.Exists(tempPath2)){
   System.IO.File.Delete(tempPath2); 
  }
  var tempPath = System.IO.Path.Combine(System.IO.Path.GetTempPath(), "fiddler.json");
  if(System.IO.File.Exists(tempPath)){
   System.IO.File.Delete(tempPath); 
  }
  var tempRequestBodyPath = System.IO.Path.Combine(System.IO.Path.GetTempPath(), "fiddler_requestBody.json");
  if(System.IO.File.Exists(tempRequestBodyPath)){
   System.IO.File.Delete(tempRequestBodyPath); 
  }
  var tempResponseBodyPath = System.IO.Path.Combine(System.IO.Path.GetTempPath(), "fiddler_responseBody.json");
  if(System.IO.File.Exists(tempResponseBodyPath)){
   System.IO.File.Delete(tempResponseBodyPath); 
  }
  oExportOptions.Add("Filename", tempPath2); 
  FiddlerApplication.DoExport("HTTPArchive v1.2", oSessions,oExportOptions, null);  
  System.IO.File.Move(tempPath2, tempPath);
  if(!System.IO.File.Exists(tempPath)){
   MessageBox.Show("生成代码失败", "No action");
   return;  
  }
  var rtPath = System.IO.Path.Combine(System.IO.Path.GetTempPath(), "fiddler_rt");
  if(System.IO.Directory.Exists(rtPath))System.IO.Directory.Delete(rtPath,true);
  if(!doProcess(httpsnippet, "\""+tempPath+"\" -t "+target+" -c "+client+" -o " + "\""+rtPath+"\"")){
   MessageBox.Show("生成代码错误", "No action");
   return;  
  }
  var file = System.IO.Directory.GetFiles(rtPath);
  if(file.Length!=1){
   MessageBox.Show("生成代码错误", "No action");
   return; 
  }
  var json = System.IO.File.ReadAllText(file[0]);
  System.IO.File.Delete(file[0]);
  var rtPath1 = System.IO.Path.Combine(System.IO.Path.GetTempPath(), "fiddler_request_body");
  if(System.IO.File.Exists(rtPath1))System.IO.File.Delete(rtPath1);
  if(!m_DisableReuqest && System.IO.File.Exists(tempRequestBodyPath)){
  
   json += getJsonCode(quicktype,tempRequestBodyPath,rtPath,rtPath1,target,"FiddlerRequest");
  }
  rtPath1 = System.IO.Path.Combine(System.IO.Path.GetTempPath(), "fiddler_response_body");
  if(System.IO.File.Exists(rtPath1))System.IO.File.Delete(rtPath1);
  if(!m_DisableResponse && System.IO.File.Exists(tempResponseBodyPath)){
   json += getJsonCode(quicktype,tempResponseBodyPath,rtPath,rtPath1,target, "FiddlerReponse"); 
  } 
  
  Clipboard.SetText(json);
  MessageBox.Show("代码生成成功,已复制到剪贴板"); 
 }
  
 static function getJsonCode(file: String,tempRequestBodyPath:String,rtPath:String,rtPath1:String,target:String,type:String): String {
  var json = "";
  var tmp1 = "";
  if(target == 'csharp'){
   tmp1 = "--quiet --telemetry disable --features just-types --array-type list --no-check-required --namespace \"Fiddlers\" --lang \"" + target + "\" --top-level \""+type+"Model\" \"" + tempRequestBodyPath + "\"" +" -o " + "\""+rtPath1+"\"";
  }
  else if(target == 'kotlin'){
   tmp1 = "--quiet --telemetry disable --framework just-types --lang \"" + target + "\" --top-level \""+type+"Model\" \"" + tempRequestBodyPath + "\"" +" -o " + "\""+rtPath1+"\"";
  }
  else if(target == 'java'){
   tmp1 = "--quiet --telemetry disable --array-type list --just-types --package \"Fiddlers\" --lang \"" + target + "\" --top-level \""+type+"Model\" \"" + tempRequestBodyPath + "\"" +" -o " + "\""+rtPath+"\\test"+"\"";
    
  }
  else {
   tmp1 = "--telemetry disable --just-types  --lang \"" + target + "\" --top-level \""+type+"Models\" \"" + tempRequestBodyPath + "\"" +" -o " + "\""+rtPath1+"\""; 
  }
   
  doProcess(file, tmp1)
  if(System.IO.File.Exists(rtPath1)){
   json += "\r\n//"+type+"-POJO\r\n" + System.IO.File.ReadAllText(rtPath1).Replace("package quicktype","");
  }
   
  if(target == 'java'){
   var javaFiles = System.IO.Directory.GetFiles(rtPath,"*.java"); 
   if(javaFiles.Length>0){
    json += "\r\n//"+type+"-POJO\r\n" ;
    for (var i:int = 0; i<javaFiles.Length; i++)
    {
     json += System.IO.File.ReadAllText(javaFiles[i]).Replace("package Fiddlers;","")
     System.IO.File.Delete(javaFiles[i]);
    }
   }
  }
  return json;
 }
   
 static function doProcess(file: String,paramsList:String): Boolean {
  var process = new System.Diagnostics.Process();
  process.StartInfo.FileName = file;
  process.StartInfo.Arguments = paramsList;
  process.StartInfo.CreateNoWindow = true;
  process.StartInfo.WindowStyle = System.Diagnostics.ProcessWindowStyle.Hidden;
  process.StartInfo.UseShellExecute = false;
  process.StartInfo.Verb = "runas";
  process.StartInfo.RedirectStandardError = true;
  process.StartInfo.RedirectStandardOutput = true;
  process.Start();
  process.WaitForExit();
  process.Dispose(); 
  return true;
 }
```

4. 复制完之后，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFlSiBK_s9Xfk4Ix--ldLCppdNuCN-60f76d.png)

5. 修改代码中的路径，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFhxlW_-iCh5h9X_doe70TbiF2A4I-33b6ca.png)

6. 路径修改完成之后，将代码复制回脚本编辑器中并保存，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFjneA-yCZlVE3SQ18XgOjCzboGUV-be61f3.png)

7. 重新打开Fiddler，然后在抓包请求上右键，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFg0VwjsZldWzCwixXJ-Jsxxc6N2Q-52fc1e.png)

当看到上图这样就说明完成了，这个时候就可以将抓包请求一键抓成对应语言的代码了。