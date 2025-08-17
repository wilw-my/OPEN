# OPEN
一个简单的编程语言[OPEN v1.0.txt](https://github.com/user-attachments/files/21822216/OPEN.v1.0.txt)
OPEN语言规范 v1.0
===============
支持多平台.exe .app .net .apk .jar（需JDK）支持Windows，MacOS,Linux,Unix,Android,ios,鸿蒙，MIUI,澎湃
动态编程，打包后即可变成静态编程
C++编写的本体且开源
自动管理内存
代码文件采用.op文件
永久免费的MIT协议

一、基本定义
--------
1. 包含关系
   - 若函数A在函数B内部缩进（开头多一个Tab），则A被包含于B（如：say包含于start）。
   
2. 关联关系
   - 通过文件函数（open/add/copy/dll）引入的文件视为关联文件。
   
3. 数据类型
   - float（浮点数）
   - bool（布尔值）
   - word（字符串）
   
4. 命名规则
   - 同一文件内局部变量不得重名
   - 关联文件的全局变量不得重名
   - 关联/同一文件中函数名与变量名不得重名
   - 仅限英文、数字、下划线，且不能以数字开头

二、函数分类
--------
1. 运行函数
   (1) start(bool)
       程序启动时执行
   (2) bye(bool)
       程序关闭时执行（延迟1秒内）
   (3) roll
       每帧运行（依赖渲染帧率）
   (4) ph-toll(float)
       每物理帧运行（默认1/60秒）
   (5) if
       后接条件，若条件满足执行
   (6) unless
       后接条件，若条件未满足执行
   (7) else
       包含在if或unless中，若if未满足或unless满足则执行

2. 特殊函数
   (1) # 
       单行注释，格式为"#注释"
   (2) //
       多行注释，格式为"//多行注释//"

3. 变量函数（不可被包含在运行函数中）
   (1) new
       新建局部变量，格式为：new class name : thing
       （类 名称 默认值）
   (2) newall
       新建全局变量，格式同"new"
   (3) func
       定义函数格式为：func name 
					... 
       调用name时执行其包含函数

4. 系统函数
   (1) system (word)
       查询系统并赋值给自己，支持：Windows/Mac/Linux/Unix/Android/HarmonyOS/HyperOS/iOS/MIUI
   (2) device (word)
       查询设备类型并赋值给自己，支持：computer/phone/pad/TV/watch
   (3) again
       重启程序
   (4) sys-bye
       关闭程序
   (5) internet (bool)
       网络连接情况
   (6) bluetooth (bool)
       蓝牙打开情况

5. 文件函数
   (1) open
       打开文件，格式为：open(路径) 或 open(路径) by(程序路径)
       - by是指利用指定程序打开
       - 不带by则会自动寻找最有用程序打开
   (2) dll
       加载支持库，格式为：dll(路径)
   (3) kill
       删除文件，格式为：kill(路径)
   (4) add
       新建文件，格式为：add(路径)
   (5) copy
       复制文件，格式为：copy(源路径)(目标路径)
       将源路径文件复制到目标路径

   注：
   - 路径为系统路径或res://（本文件所在文件夹）
   - 若路径结尾为文件夹，则操作其下所有文件
   - 路径中"{[变量名]}"表示该变量值
   - 路径不存在则新建（add/copy）

6. 输入函数
   (1) input (word)
       回车式输入监控（仅键盘字符）
   (2) Input (word)
       实时式输入监控（支持鼠标、手柄、switch、键盘）

7. 数学函数
   运算符：
   +  -  *  /  ^  !  %  +/（根号）
   三角函数：
   sin/cos/tan/cot/sec/csc
   比较运算：
   ==  !=  >  <  >=  <=
   （支持链式比较：如 a < b == c）

8. 绘制函数
   (1) colour
       颜色格式：colour(R,G,B,A)
   (2) print
       绘制格式：print(colour(...))(坐标/函数)
   (3) shape
       绘制图形：shape(图形名)(大小)(clolour)(坐标)
       - ring(半径)：圆形
       - three(边1,边2,边3)：三角形
       - par(底,高,倾角)：平行四边形
       - ringing(R,r)：圆环（外径R，内径r）

9. 网络函数
   (1) http
       打开网址，格式：http(网址)
   (2) api
       接入大模型（如DeepSeek/ChatGPT），格式：api(API KEY)
   (3) https
       打开网络图像，格式：https(图片URL)

10. 基本函数
    (1) say
        输出，格式：say("文本") 或 say(变量/函数名)
    (2)for
        循环,格式：for(x)循环X次不带(x)则无限次循环

四、示例代码
--------
# OPEN语言示例：启动输出&网络检测
start 
    say("程序启动")
    if internet(true) 
        say("网络已连接")
        http("https://deepseek.com")


# OPEN语言示例：绘制图形
roll
    colour(255, 0, 0, 255)    # 红色
    shape(ring, 50)            # 半径50px的圆
    
    colour(255, 255, 0, 255)  # 黄色
    shape(three, 70, 70, 70)   # 等边三角形


# OPEN语言示例：AI集成
func askAI(question) 
    new word apiKey: "YOUR_API_KEY"
    response = api(apiKey, question)
    say(response)


start
    askAI("OPEN语言的优势是什么？")


