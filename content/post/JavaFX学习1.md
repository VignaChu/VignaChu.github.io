---
title: JavaFX基础学习1
cover: ../../cover/vignaHoldingCup.png
description: 本文介绍了JavaFX的基础用法

date: 2025-10-05T11:00:00+08:00
lastmod: 2025-10-05T11:00:00+08:00

tags:
  - Java
  - JavaFX
  - 桌面应用
  - Study
categories:
  - Study

math: true
mermaid: true

---

## 杂谈

JavaFX作为Swing与awt的现代替代品，是Java平台的UI组件库，它提供了丰富的控件和功能，内置现代化的控件，支持CSS语法，内置视觉效果，并通过GPU进行渲染。

## 导入

可以使用Maven管理工具导入JavaFX依赖，只需修改pom.xml文件，添加以下依赖：

```xml
<dependencies>
        <!-- JavaFX本体 -->
        <dependency>
            <groupId>org.openjfx</groupId>
            <artifactId>javafx-controls</artifactId>
            <version>21.0.1</version>
        </dependency>
        <!--FXML文件扩展-->
        <dependency>
            <groupId>org.openjfx</groupId>
            <artifactId>javafx-fxml</artifactId>
            <version>21.0.1</version>
        </dependency>
    </dependencies>
    <!-- 官方提供的编译插件 -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.openjfx</groupId>
                <artifactId>javafx-maven-plugin</artifactId>
                <version>0.0.8</version>
                <configuration>
                    <mainClass>org.example.App</mainClass>
                    <!-- 你项目的入口类 -->
                </configuration>
            </plugin>
        </plugins>
    </build>
```

## 代码框架

JavaFX的代码框架如下：

```java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.layout.StackPane;
import javafx.stage.Stage;
... // 其他需要的模块

public class App extends Application {
    @Override
    // 重载start方法
    public void start(Stage primaryStage) {
        // 创建布局
        StackPane root = new StackPane();
        // 创建窗口
        Scene scene = new Scene(root, 300, 250);
        primaryStage.setScene(scene);
        // 设置标题
        primaryStage.setTitle("JavaFX Demo");
        // 显示窗口
        primaryStage.show();
    }
    // stage->scene->root
    public static void main(String[] args) {
        launch(args);  //调用Application的启动方法
    }
}

```

当launch()方法被调用后,类会先后调用init()、**start()**、stop()三个方法，init()方法用于初始化一些组件(如数据库连接、线程等)，start()方法用于创建窗口并显示(实现主要功能)，stop()方法用于释放资源。

*注：init()方法被调用时JavaFX组件还未被加载，因此不能在init()方法中创建组件。*

## 窗口(Stage)

Stage是JavaFX的顶层容器，相当于Swing的JFrame，包含了窗口的各种属性。一般应用只有一个主窗口，使用start方法的参数primaryStage来创建主窗口。

1. title:窗口标题，通过`primaryStage.setTitle("标题内容");`来修改;
2. icon:窗口图标，通过`primaryStage.getIcons().add(new Image("url"));`来设置;
3. resizable:窗口是否可调整大小，通过`primaryStage.setResizable(boolean);`来设置;
4. stageStyle:窗口样式，通过`primaryStage.initStyle(窗口样式);`来设置。一共有四种样式：StageStyle.DECORATED(默认样式，什么都有)、StageStyle.UNDECORATED(无装饰样式，全屏叉号之类的都没有)、StageStyle.TRANSPARENT(背景可以透明，其他和默认一致)、StageStyle.UTILITY(只有一个抬头和叉);
5. modality:窗口是否为模式窗口，通过`primaryStage.initModality(属性);`来设置。一共有三种:Modality.NONE(默认，不会阻塞其他窗口),Modality.WINDOW_MODAL(只阻塞父子窗口),Modality.APPLICATION_MODAL(只能操作当前窗口);
6. event:事件，窗口常用的基本只有关闭(用于提示是否关闭)。首先需要取消默认的关闭事件`Platform.setImplicitExit(false)`,之后通过`primaryStage.setOnCloseRequest(event -> { event.consume();//取消关闭窗口的动作 之后要执行的逻辑});`，之后如果要关闭调用`Platform.exit();`

7. 在start方法的最后记得使用`.show()`方法来显示窗口。

## 场景(Scene)

Scene是JavaFX的容器，相当于Swing的JPanel，用于容纳各种组件。一般通过`Scene scene = new Scene(root, 宽, 高);`来创建场景，其中root作为组件图的根节点，通常是是布局组件。

场景可以设置场景内鼠标的光标`setCunsor(new ImageCunsor(new Image("url")));`


## 组件

JavaFX提供了丰富的组件，常用的组件有：

- 布局组件：Pane、BorderPane、GridPane、HBox、VBox、StackPane等。
- 控件：Button、Label、TextField、TextArea、ChoiceBox、List、ComboBox、MenuBar、ToolBar等。
- 图形组件：Canvas、Line、Rectangle、Circle、Arc、Polygon、Polyline、Image等。
- 效果组件：Color、Effect、Shadow、Blend、Transform、Animation、Transition等。
- 媒体组件：MediaView、MediaPlayer、Media、AudioSpectrum、VideoSpectrum等。
- 多媒体组件：WebView等。
- 除此之外还有数据绑定和属性系统、多线程、CSS处理、FXML处理、事件处理、表格与树型控件、图表等。

### 节点类(Node)

Node是所有组件的父类，有很多方法的定义，下面介绍一下其中的一些常用方法：
1. layoutX、layoutY:组件在父容器中的坐标，通过setLayoutX、setLayoutY方法来设置;
2. prefWidth、prefHeight:组件的宽度、高度，通过setPrefWidth、setPrefHeight方法来设置;
3. style:组件的CSS样式，通过setStyle方法来设置;
```java
// 设置背景颜色和边框颜色
node.setStyle("-fx-background-color: #FF0000; -fx-border-color: #000000;");
// 前面加上-fx-后和CSS语法一样，不同样式之间用;空格隔开
```
4. opacity:组件的透明度(0~1)，通过setOpacity方法来设置;
5. visible:组件是否可见，通过setVisible方法来设置;
6. alignment:组件在父容器中的对齐方式，通过setAlignment方法来设置,有若干种对齐方式：`Pos.TOP_LEFT、Pos.TOP_CENTER、Pos.TOP_RIGHT、Pos.CENTER_LEFT、Pos.CENTER、Pos.CENTER_RIGHT、Pos.BOTTOM_LEFT、Pos.BOTTOM_CENTER、Pos.BOTTOM_RIGHT`。
7. rotate:组件的旋转角度，通过setRotate方法来设置;
8. translateX、translateY:组件的平移距离,通过setTranslateX、setTranslateY方法来设置;
9. parent:组件的父容器,通过getParent方法来获取;
10. scene:组件所在的场景,通过getScene方法来获取;
11. children:组件的子节点列表,通过getChildren方法来获取,例如添加子节点可以使用`getChildren().add(child);`来实现，通常也使用addAll()方法来批量添加,内部填数组或若干逗号分隔的元素都可以。

### 容器

容器也是节点的一种，尝尝作为根节点或局部根节点，用于容纳其他组件。
1. VBox：从左上开始一段一段往下排，构造函数参数为double类型的间距；
2. HBox：从左上开始一段一段往右排，构造函数参数为double类型的间距；
3. FlowPane：动态的流式布局，默认水平排布，排满则换行。有多种构造函数
```java
FlowPane flowPane = new FlowPane(Orientation.HORIZONTAL, 10, 10); 
// 第一个参数为排列方向，后两个分别为横纵间距，最后是子节点，每部分参数均可省略
//Orientation.HORIZONTAL 水平排布(默认)
//Orientation.VERTICAL 垂直排布
```
也可以在后面用setOrientation()方法设置方向。
4. TilePane：每个子节点大小相同的布局，参数太多所以我通常都是先创建一个空的再修改其属性。

*注：修改属性的方法命名格式通通为set+属性名。且下面的并非所有属性*

- alignment:对齐方式，和上面说的一致
- hgap/vgap:水平/垂直间距，设置后会影响子节点的间距
- orientation:排布方向，和上面那个容器的一致
- perfColumnCount/prefRowCount:子节点的期望列数/行数，设置后会影响子节点的布局
- prefTileWidth/prefTileHeight:子节点的大小，设置后会影响子节点的布局
- tileAlignment:子节点的对齐方式，即每个格子内子节点处于什么位置

5. **BorderPane**:四个区域，分别为上、下、左、右，类似Swing的BorderLayout。可以设置边框和背景颜色，也可以设置子节点的位置。通过setTop、setBottom、setLeft、setRight方法来为每一部分添加节点。
6. GridPane：网格布局，网格的大小取决于网络网格中显示的组件大小，可以通过`gridPane.add(button1, 0, 0, 1, 1);`添加组件，前几个是起始坐标，后两个为跨度
7. ScrollPane：带滚动条的容器
8. TabPane：感觉还挺实用，但比较特殊，需要仔细讲一下：
    - 首先需要创建外部容器TabPane
    - 之后创建Tab，Tab需要一个标题和一个内容节点。可以在构造函数的时候设置标题，在setContent()方法中设置内容节点。
    - 最后通过TabPane的getTabs()方法获取Tab列表，并将Tab添加到TabPane中。
9.  SplitPane：带分割条的面板，给每个子组件之间放分隔条，可以和上面类似修改方向
10. StackPane：默认所有元素都在中心的布局，可以用于添加背景、遮罩等。

## 杂项

- `getHostServices().showDocument(string url)`:用于打开外部网页与文档，尝尝放在按钮的监听器中。

## 参考资料
- [封面图片](https://safebooru.org/index.php?page=post&s=view&id=3253193)
- [JavaFX 桌面软件 PC 软件开发 基础入门](https://www.bilibili.com/video/BV1Qf4y1F7Zv?vd_source=5909159ad31d9e8d4f1abee249dbcd4b&spm_id_from=333.788.videopod.episodes)
- [JavaFX官网](https://openjfx.cn/)
- [Java最新图形化界面开发技术——JavaFx教程](https://developer.aliyun.com/article/1646638)
- [JavaFX官方文档](https://openjfx.cn/openjfx-docs/)