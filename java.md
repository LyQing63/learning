## 1.网络编程

### URL
* 协议与域名之间  "://" 
* 路径: "/"
* 参数: "参数名 = 参数值"
---
### Get 请求 - 无参数
***抓取网站用库:*** `okhttp3`
安装方式：在`pom.xml`中添加依赖

```java
 <!-- https://mvnrepository.com/artifact/com.squareup.okhttp3/okhttp -->
<dependency>
 <groupId>com.squareup.okhttp3</groupId>
 <artifactId>okhttp</artifactId>
 <version>4.1.0</version>
</dependency>
```
1. 实例化 ```OkHttpClient```
1. 实例化```Request```对象
1. 构建对象 （调用对象）
1. 执行时会出错，需要```Catch```捕捉
1. 获取返回的字符串内容
---
### API
>API为应用程序接口，一般是指一些预先定义函数，目的是可以为开发人员快速访问某一程
>序，而无需和访问源码，或理解它内部工作的细节。
>即: API可以快速调用某个程序。

代码：
```java
public stastic String getContent(String url){
	OkHttpClient okHttpClient = new OkHttpClient();
	Request request = new Request.builder().url(""对应的网址"").build;
	Call call = okHttpClient.newCall(request);
	try{
		result = call.execute().body.string();
	} catch (Exception e) {
		system.out.println("request" + url + "error");
    	e.printStackTrace();
	}
}
```
>Okhttp3 的源代码
![Okhttp3](https://style.youkeda.com/img/ham/course/j3/j14-2-1-12.png?x-oss-process=image/resize,w_1534/watermark,image_d2F0ZXJtYXNrLnBuZz94LW9zcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSx3XzEwMA==,t_60,g_se,x_10,y_10)

---
### post() 方法
>用于提交数据至服务器进行增加、修改、删除操作
>数据不是放在url中，而是放在表单中提交

* 构建 ```FormBody```表单对象，放置表单数据
```java
Builder builder = new FormBody.Builder();
// 设置数据，第一个参数是数据名，第二个参数是数据值
builder.add("", "");
FormBody formBody = builder.build();
Request request = new Request.Builder().url(url).post(formBody).build();
```
```java
Public stastic postContent(String url,Map<Sting,Stirng> formData)
{
	//okHttpClient 实例
	OkHttpClient okHttpClient = new OkHttpClient();
	//post 方式提交的数据
	Builder builder = new FormBody.Builder();
	//放入表单数据
	for (String key:formData.keyset())
	{
		builder.add(key,formData.get(key));
	}
	//构建 FormBody 对象
	FormBody formBody = builder.build();
	Request request = new Request.Builder().url(url).post(formBody).build();
	Call call = okHttpClient.newCall(request);
	String result = null;
	result = call.execute().body().string();
	return result;
}
```
* POST JSON 数据parse("文件目录;charset=utf-8");
```java
private static final MediaType JSON_TYPE = MediaType.
```
	1. 将数据转换成```JSON```格式的字符串，调用```JSON.toJSONString()```
```java
String param = JSON.toJSONString(forData);
```
	1. 创建```RequestBody```实例，提交的是文件目录与编码格式
```java
RequestBody requestBody = RequestBody.creat(JSON_TYPE,param);
```
	1. 构建``Request```实例对象，调用```.post(requestBody)```表示提交数据
```java
Request request = new Request.Builder().url(url).post(formBody)
```
* Response - 网页
	* 获取状态码
	```call.execute().code()```
	* 利用Response爬取数据(用一次请求)
	```java
	Response response = call.execute();
	int code = response.code();
	result = response.body().string();
	```
* Response - 非文本文件
	非文本文件不能用```response.body().string()```获取
	要用```response.body().bytes();```获取
* Response - JSON
	将```JSON```数据转化为```Map```格式
	```java
	Map contentObj = JSON.parseObject(content,Map.class);
	```
* 防盗链
>必须从上一主页面进入网页
>用```Referer```信息，表示请求来源
* Host
>表示当前请求的域名
>属于```Headers```数据
* 下载文件
	* 写入文本文件
	```java
	File file = new File("foo.text");
	FileWriter fileWritter = new FileWriter(file.getName());
	//写入内容
	fileWritter.write(content);
	
	//关闭
	fileWritter.close();
	```
	* 写入二进制(excel,图片等)文件
	```java
	//文件对象
	File file = new File("china-city-list.xlsx")
	
	//写文件
	FileOutputStream fos = new FileOutputStream(file);
	fos.write(data);
	
	//必须刷新并关闭
	fos.flush();
	fos.close();
	```
	* 解析excel
	```java
	<dependency>
  		<groupId>com.alibaba</groupId>
  		<artifactId>easyexcel</artifactId>
  		<version>3.1.1</version>
	</dependency>
	```
	添加依赖
	***解析路径一定是:sheet -> 行 -> 列***
	
	```java
	// 读取第一个sheet
	List<Map<Integer, String>> sheetDatas = EasyExcel.read(文件名).sheet(0).doReadSync();
	//List 中每一个元素表示一行
	for (Map<Integer, String>rowData :sheetDatas){
		//Map 中用序号代指每一列
		for (Integer index : rowData.keySet()){
		//列值
		Stirng columnValue = rowData.get(index);
		}
	}
	```
	![excel与java](https://style.youkeda.com/img/ham/course/py2/j14-5-3-1.svg )
* cookie
	***cookie的内容要从第一行开始填入***
	cookie 是存放在客户端浏览器的，而且是临时的因此登录后还行在登录状态与服务器通讯就比较麻烦，用session可解决问题
* session
	```java
	  // 用 CookieJar 实现 cookie 的存储，便于登录后请求其它 URL 可以复用
private static final OkHttpClient okHttpClient = new OkHttpClient.Builder()
      .cookieJar(new CookieJar() {
        private final HashMap<String, List<Cookie>> cookieStore = new HashMap<>();

        @Override
        public void saveFromResponse(HttpUrl url, List<Cookie> cookies) {
          cookieStore.put("mtime.com", cookies);
          System.out.println("[saveFromResponse]url.host()=" + url.host());
        }

        @Override
        public List<Cookie> loadForRequest(HttpUrl url) {
          System.out.println("[loadForRequest]url.host()=" + url.host());
          List<Cookie> cookies = cookieStore.get("mtime.com");
          return cookies != null ? cookies : new ArrayList<>();
        }
      })
      .build();
	```
	* 复用
		创建一个方法
* JavaMail
	添加依赖
	```java
<dependency>
 <groupId>javax.mail</groupId>
 <artifactId>mail</artifactId>
 <version>1.4</version>
</dependency>
	```
代码
```java
import java.security.Security;
import java.util.Properties;
import javax.mail.Authenticator;
import javax.mail.Message;
import javax.mail.PasswordAuthentication;
import javax.mail.Session;
import javax.mail.Transport;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeMessage;

public class MailClient {
  public static void main(String[] args) {
    try {
      final String SSL_FACTORY = "javax.net.ssl.SSLSocketFactory";

      //配置邮箱信息
      Properties props = System.getProperties();
      //邮件服务器
      props.setProperty("mail.smtp.host", "smtp.qq.com");
      props.setProperty("mail.smtp.socketFactory.class", SSL_FACTORY);
      props.setProperty("mail.smtp.socketFactory.fallback", "false");
      //邮件服务器端口
      props.setProperty("mail.smtp.port", "465");
      props.setProperty("mail.smtp.socketFactory.port", "465");
      //鉴权信息
      props.setProperty("mail.smtp.auth", "true");
      //建立邮件会话
      Session session = Session.getDefaultInstance(props, new Authenticator() {
        //身份认证
        protected PasswordAuthentication getPasswordAuthentication() {
          //1.账户 授权码
          return new PasswordAuthentication("xxxxxxx@qq.com", "xxxx");
        }
      });
      //建立邮件对象
      MimeMessage message = new MimeMessage(session);
      //设置邮件的发件人
      message.setFrom(new InternetAddress("xxxxxxx@qq.com"));
      //2.设置邮件的收件人
      message.setRecipients(Message.RecipientType.TO, "xxxxxxx@qq.com");
      //设置邮件的主题
      message.setSubject("通过javamail发出！！！");
      //文本部分
      message.setContent("文本邮件测试", "text/html;charset=UTF-8");
      message.saveChanges();
      //发送邮件
      Transport.send(message);
    } catch (Exception e) {
      e.printStackTrace();
    }
  }
}
```


## 2.简单算法
* 选择排序
```java
for (int i=0;i<len-1;i++)//不断缩小无序区
{
	for (int j=i+1;j<len;j++)//遍历无序区中元素
	{
	//从无序区中选出一个小的交换
		if (array[j]<array[i])
		{
			int temp = array[i];
			array[i] = array[j];
			arry[j] = temp;
		}
	}
}
```
* 冒泡排序
```java
for (int i=len-1;i>0;i--)//不断缩小无序区
{
	for (int j=0;j<i;j++)//遍历无序区中元素
	{
	//从无序区中选出一个大的向前冒
		if (array[j]>array[j+1])
		{
			int temp = array[j];
			array[j] = array[j+1];
			arry[j+1] = temp;
		}
	}
}
```
* 插入排序
```java
for (int i=1;i<len-1;i++)//不断缩小无序区
{
	int j = i-1;
	int temp = array[i];
	//从无序区中将目标插入合适位置
	while (j>=0 && array[j]>array[i])
	{
		array[j+1] = array[j];
		j--;
	}
}
```
* 归并排序
```java
  public static int[] mergeSort(int[] array) {
    // 为了方便查看结果，我们将每个数组进行打印
    if (array.length == 1) {
      return array;
    }

    int middle = array.length / 2;
    // 处理 0 到 middle 左侧数组部分
    int[] left = mergeSort(subArray(array, 0, middle));
    // 处理 middle 到 array.length 右侧数组部分
    int[] right = mergeSort(subArray(array, middle, array.length));
    // TODO处理合并问题
    int i = 0,j = 0;
    while (i < left.length && j< right.length){
      if (left[i]<right[j]){
        array[i+j] = left[i];
        i++;
      } else {
        array[i+j] = right[j];
        j++;
      }
    }
    while (i<left.length){
      array[i+j] = left[i];
      i++;
    }
    while (j<right.length){
      array[i+j] = right[j];
      j++;
    }
    return array;
  }

  // 拷贝原数组的部分内容，从 left 到 right
  public static int[] subArray(int[] source, int left, int right) {
    // 创建一个新数组
    int[] result = new int[right - left];
    // 依次赋值进去
    for (int i = left; i < right; i++) {
      result[i - left] = source[i];
    }
    return result;
  }
```
![归并排序](https://style.youkeda.com/img/course/a1/5/4-2.svg)

* 快速排序
```java
// 快速排序
public static void quickSort(int[] array) {
    // 调用快速排序的核心，传入left，right
    quickSortCore(array, 0, array.length - 1);
}

// 快速排序的核心，同样也是递归函数
    // 递归基准条件，left >= right 即表示数组只有1个或者0个元素。
    if (left >= right) {
        return;
    }
    // 根据轴分区
    int pivotIndex = partition(array, left, right);

    // 递归调用左侧和右侧数组分区
    quickSortCore(array, left, pivotIndex - 1);
    quickSortCore(array, pivotIndex + 1, right);
}

// 对数组进行分区，并返回当前轴所在的位置
public static int partition(int[] array, int left, int right) {
	int temp = array[right];
	int temp_p = right;
	while (left < right) {
		while (array[left] <= temp && left < array.length-1) {
		 left++;
		}
		while (array[right] >= temp && right > 0) {
		 right--;
		}
		int index = array[left];
		array[left] = array[right];
		array[right] = index;
	}
	if (array[left] > temp) {
	array[temp_p] = array[left];
	array[left] = temp;
	}
	return left;
}
```
![快速排序](https://img-blog.csdnimg.cn/img_convert/a02c25ee737cd9ef749d859f671b045e.gif)
* 快速选择
```java
public class QuickSort {
  // 快速选择，返回选中的元素
  public static int quickFind(int[] array, int aim) {
    return quickFindCore(array, aim, 0, array.length - 1);
  }

  public static int quickFindCore(int[] array, int aim, int left, int right) {
    if (left >= right) {
      return array[left];
    }
    int pivotIndex = partition(array,left,right);
    if (pivotIndex == aim) {
      return array[pivotIndex];
    } else if (pivotIndex > aim) {
      return quickFindCore(array,aim,left,pivotIndex-1);
    } else {
      return quickFindCore(array,aim,pivotIndex+1,right);
    }
  }
  public static int partition(int[] array, int left, int right) {
    int temp = array[right];
    int temp_p = right;
    while (left < right) {
      while (array[left] <= temp && left < array.length - 1) {
        left++;
      }
      while (array[right] >= temp && right > 0) {
        right--;
      }
      if (left < right) {
        swap(array,left,right);
      }
    }
    if (array[left]>temp) {
      swap(array,left,temp_p);
    }
    return left;
  }
  public static void swap(int[] array,int i,int j) {
    int index = array[i];
    array[i] = array[j];
    array[j] = index;
  }
```
* 动态规划
	* 换零钱
	```java
	public int change(Human human){
        int amount = human.amount;
        var dp = new int[amount+1];
        int[] array = this.smallChanges;
        int len = array.length ;
        for (int i = 1; i < dp.length;i++)
        {
            dp[i] = amount+1;
        }
        for (int i = 1; i<=amount;i++)
        {
            for (int j = 0; j < len;j++)
            {
                if (array[j] <= i)
                {
                    dp[i] = Math.min(dp[i], dp[i - array[j]] + 1);
                }
            }
        }
        return dp[amount] > amount ? -1:dp[amount];
    }
	```
## 3.图云
依赖
```java
<dependency>
  <groupId>com.kennycason</groupId>
  <artifactId>kumo-core</artifactId>
  <version>1.17</version>
</dependency>
<!-- 下面tokenizers是为了中文分词引入 -->
<dependency>
  <groupId>com.kennycason</groupId>
  <artifactId>kumo-tokenizers</artifactId>
  <version>1.17</version>
</dependency>
```
```java
public static void generate(String artistId, List<String> texts) {

    FrequencyAnalyzer frequencyAnalyzer = new FrequencyAnalyzer();
    //设置返回的词数
    frequencyAnalyzer.setWordFrequenciesToReturn(500);
    //设置返回的词语最小出现频次
    frequencyAnalyzer.setMinWordLength(4);

    //引入中文解析器
    frequencyAnalyzer.setWordTokenizer(new ChineseWordTokenizer());
    //输入文章数据，进行分词
    final List<WordFrequency> wordFrequencyList = frequencyAnalyzer.load(texts);
    //设置图片分辨率大小
    Dimension dimension = new Dimension(600, 600);
    //此处的设置采用内置常量即可，生成词云对象
    WordCloud wordCloud = new WordCloud(dimension, CollisionMode.PIXEL_PERFECT);
    //设置边界及字体
    wordCloud.setPadding(2);
    // 设置字体，字体必须支持中文，不能随便改
    wordCloud.setKumoFont(new KumoFont("阿里巴巴普惠体 Light", FontWeight.PLAIN));
    //ColorPalette是调色板，用于设置词云显示的多种颜色，越靠前设置表示词频越高的词语的颜色
    wordCloud.setColorPalette(
        new ColorPalette(new Color(0x4055F1), new Color(0x408DF1), new Color(0x40AAF1),
            new Color(0x40C5F1), new Color(0x40D3F1), new Color(0xFFFFFF)));
    wordCloud.setFontScalar(new SqrtFontScalar(10, 70));
    //设置背景图层为圆形
    wordCloud.setBackground(new CircleBackground(300));
    //生成词云
    wordCloud.build(wordFrequencyList);
    //输出到图片文件，用当前的毫秒数作为文件名
    Long milliSecond = LocalDateTime.now().toInstant(ZoneOffset.of("+8")).toEpochMilli();
    //输出到图片文件
    wordCloud.writeToFile("wordCloud-" + artistId + ".png");
  }

```

## JAVA基础

### 接口
* 一个类可以通过继承接口的方式，来继承接口的抽象方法。
* 接口无法被实例化，但可以被实现。实现一个接口的类，必须实现接口内的所有方法，否则必须声明抽象类。
* 接口类型可以用来声明一个变量，可以成为空指针或被绑定在一个以此接口实现的对象。
#### 特性：
* 接口是隐式抽象的，当声明一个接口的时候，不必使用abstract关键字。
* 接口中每一个方法也是隐式抽象的，声明时同样不需要abstract关键字。
* 接口中的方法都是公有的。
#### 继承
* 一个接口能继承另一个接口。
* 允许多继承
#### 标记接口
***给对象标记，时对象拥有某个或某些特权***

* 最常用的为没有任何方法的接口
* 没有任何属性和方法，它仅仅表明它的类属于一个特定的类型，供其他代码来测试允许做一些事情

### 抽象类
***一个类中没有包含足够信息来描绘一个具体的对象的类为抽象类***

* 不能被实例化，因此必须被继承才能使用（一个类只能继承一个抽象类）
* 用```abstract class```来定义抽象类
#### 抽象方法
* 用```abstract```来定义
* 在父类中声明该方法为抽象方法，具体实现在子类中确认。
* 子类必须重写父类的抽象方法或者声明自身为抽象类
