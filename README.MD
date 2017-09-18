# jenkins自动打包平台  
　　使用jenkins构建的自动打包平台脚本。  
　　其中包括android ant/gradle脚本、ios xcodebuild脚本、代码更新git脚本、邮件内容email脚本
***
## jenkins自动打包脚本与插件脚本
### 通用插件:
  + git:  
  　　代替jenkins自有的git插件，实现自定义需求的git插件。  
　　　　目前实现功能有：  
　　　　　　git clone:  
　　　　　　　　clone项目、判断项目是否存在，存在则pull、可自定义clone路径  
　　　　　　git pull:  
　　　　　　　　更新项目，主要用于更新依赖库项目  
　　　　使用方式：  
　　　　　　git clone xxxx.xxxx.com/xxx.git /home/xxx/xxx  
　　　　　　git pull /home/xxx/librarys  
　　　　可以继续扩展功能，只需再case语句中增加action与具体操作即可
  
  + email:  
　　编写email模板的插件，可以自定义任意内容的email模板  
　　　　目前已有模板有：  
　　　　　　git失败时的email模板、jenkins通用模板  
　　　　使用方式：  
　　　　　　email "git"/"jenkins"  
　　　　后续可以继续扩展更多模块

### 打包插件:　　
  + ant:  
　　ant编译eclipse项目插件  
　　　　实现功能：  
　　　　　　ant打包apk、规则化命名apk、生成apk下载url、生成apk下载二维码、调用email发送email  
　　　　使用方式：  
　　　　　　ant ProjectName  
  + gradle:  
　　gradle编译android studio项目插件  
　　　　实现功能：  
　　　　　　gradle打包apk、apk规则化命名、生成apk下载url、生成apk下载二维码、调用email插件发送email  
　　　　使用方式：  
　　　　　　gradle ProjectName  
  + xcodebuild:  
　　ios项目打包插件  
　　　　实现功能：  
　　　　　　xcodebuild打包生成ipa、fir.im cli上传ipa至fir服务器  
　　　　使用方式：  
　　　　　　xcodebuild ProjectName  




## jenkins (自由风格)项目所需配置参数
### android:
	ANDROID_SDK:android sdk版本号，例如：android-19
	BUILD_TYPE:打包模式，如：debug、release
	COMMONIT_BRANCH:项目分支号，例如master
	COMMONIT_LIBRARY_BRANCH:依赖库项目分支号
### ios:
	BUILD_TYPE:打包模式，如：Debug、Release
	SCHEME:项目scheme，项目必须将scheme设置为shared
	COMMONIT_BRANCH:项目分支号，例如master
	COMMONIT_LIBRARY_BRANCH:依赖库项目分支号

## jenkins shell 配置
	git clone xxxx.xxxx.com/xxx.git
	git pull /home/xxx/librarys
	/home/arche/workspace/jenkins/shell/ant(gradle、xcodebuild) ${WORKSPACE}
