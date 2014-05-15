# 如何将C++绑定至Javascript

## 简介

Cocos2d JS API接口与cocos2d-x、cocos2d-iphone及cocos2d-html5相同。Cocos2d-html5是通过浏览器在移动设备上运行，cocos2d-iphone和cocos2d-x内的JSB可以大幅提升引擎性能。所有图形、渲染及物理库代码都会在本地运行，只有游戏逻辑会在Java脚本中运行。

将游戏代码移植到脚本语言不仅仅是基于跨平台角度，还有很多其他的优势。因为代码是未编译的，所有在运行时期可以替换，从而加快测试周期。

## 为什么选择Javascript？

Javascript脚本优点如下：

- 更快开发速度

支持JSB绑定的项目：

- cocos2d-x



基本上所有cocos2d、Chipmunk库或CocosBuilder Reader API接口几乎都会以本地速度运行。但是应该注意以下情况：


### 如何工作

绑定生成器（Bindings-generator）是一个Java脚本绑定生成器，会生成自动绑定spidermonkey目标Java脚本的C/C++代码。


1. 下载绑定生成器，本机路径/Users/iven/Dev/bindings-generator

	```
	xcodebuild -license
	```




	```
	sudo port -v selfupdate
	```

	当更新完成之后，使用MacPort在命令行中安装python依赖（dependencies）

	```









- 根据自己的环境个性化设置“test/userconf.ini”和“test/user.cfg”文件。

	[DEFAULT]

	./test.sh

	Errors in parsing headers:







- 修改“autogentestbindings.cpp”中的注册函数如下：

	```
	void register_all_autogentestbindings(JSContext* cx, JSObject* obj) {
	```
	注意：如果你将“ts”添加到“test.ini”文件中的“target_namespace”变量里，便会自动生成代码。无需修改。
	
	```
	 target_namespace =ts
	```
		
- 在“AppDelegate”中注册

	包含头文件“autogentestbindings.hpp”然后注册回调函数：

	```
	sc->addRegisterCallback(register_all_autogentestbindings); 
	```

- 在“hello.js”文件适当地方增加以下代码。本机将“init f”函数放在第一个场景。

	```
	var myClass=new ts.SimpleNativeClass();
	```
	

绑定生成器存在以下两个限制

- 自变量数字参数无法工作，所以需要手动编写包装器
- 代表类无法工作，所以需要手动绑定，详见下一部分。










#include "cocos2d.h" 


bool JSB::JSBinding::init(){




#include "jsapi.h" 

然后注意“JSB_AUTO.cpp”的实现。

```
#include "jsapi.h" 


```

现在已经完成了大部分工作，但是我们需要在“SpiderMonkey”进行注册。
ScriptingCore* sc = ScriptingCore::getInstance();



JSBool JSB_cocos2dx_retain(JSContext* cx, uint32_t argc, jsval *vp){


JS_DefineFunction(cx, jsb_prototype, "retain", JSB_cocos2dx_retain, 0, JSPROP_READONLY | JSPROP_PERMANENT);



var testJSB = new JSB.JSBinding();


js_proxy_t* p = jsb_get_native_proxy(this);




var testJSB = new JSB.JSBinding();




