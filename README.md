# xvcode (x-validation code)


**项目作用：**
主要用于生成web动态验证码图片。主要应用场景为web 页面上需要用户输入验证码才能进行操作的地方。
**开发原因：**
目前网络广为流传的代码所生成的验证码图片太简单，并易于破解。所以我们自己开发了一个简单的验证码生成包，增加了背景的干扰性。
**features：**
> - 提供1中png格式的图片生成器，3种gif格式图片生成器。
> - 随机码由生成器自身生成。
> - 可一定程度自定义背景干扰图形参数

**感谢：**
该项目用于生成gif图片的代码使用了 [gifencoder][1] 项目

*图片示例*

PngVCGenerator:
![Png](docs/img/1.png)

GifVCGenerator:
![Gif1](docs/img/1.gif)

GifVCGenerator2:
![Gif1](docs/img/2.gif)

GifVCGenerator3:
![Gif1](docs/img/3.gif)

[1]: https://github.com/cloader/gifencoder

## getting started

### java 项目中使用


######加入依赖包（maven）

在pom.xml中加入私有仓库地址：
```
<repository>
	<id>snapshots</id>
	<url>http://120.26.91.179:8081/nexus/content/repositories/snapshots/</url>
	<releases>
		<enabled>false</enabled>
	</releases>
	<snapshots>
		<enabled>true</enabled>
	</snapshots>
</repository>
```
在pom.xml依赖中增加：
```
<dependency>
	<groupId>com.xinguang</groupId>
	<artifactId>xvcode</artifactId>
	<version>1.0-SNAPSHOT</version>
</dependency>
```
#######代码示例
```
package test

import java.io.FileOutputStream;
import java.io.IOException;
import com.xinguang.xvcode.generator.Generator;
import com.xinguang.xvcode.generator.Gif2VCGenerator;
import com.xinguang.xvcode.generator.Gif3VCGenerator;
import com.xinguang.xvcode.generator.GifVCGenerator;
import com.xinguang.xvcode.generator.PngVCGenerator;

class Test {
//生成验证码图片到本地磁盘
public void main(String args[]) throws IOException　{
		String path = ".";//图片存储路径
		Integer height = 40;//image 高度。
		Integer width = 200;//image 宽度。
		Integer count = 5;	//
		Generator generator = new PngVCGenerator(width, height, count);
        generator.write2out(new FileOutputStream(path + "/1.png")).close();
        generator = new GifVCGenerator(width, height, count);//   gif
        generator.write2out(new FileOutputStream(path + "/1.gif")).close();
        generator = new Gif2VCGenerator(width, height, count);//   gif
        generator.write2out(new FileOutputStream(path + "/2.gif")).close();
        generator = new Gif3VCGenerator(width, height, count);//   gif
        generator.write2out(new FileOutputStream(path + "/3.gif")).close();
}
}
```
如果要将验证码图片以流的方式穿到前端，可以直接使用*generator.write2out()*方法


### 命令行使用

可以使用jar包直接生成本地图片。命令：
```
java -jar xvcode-1.0-SNAPSHOT-cl
```
支持参数如下：
``` 
usage:
	-p	dir path for the image, default generate in current dir
	-h	image height, default 200
	-w	image width, default 40
	-cl	validation code length, default 5
	
```
例如：
```
java -jar xvcode-1.0-SNAPSHOT-cl -p test/ -h 300 -w 60 -cl 7
```