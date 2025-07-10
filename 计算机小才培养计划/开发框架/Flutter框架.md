# 使用

## 环境搭建
- 安装flutter sdk,并完成环境变量的配置(flutter中包含有dart的sdk)，并配置环境变量设置国内的镜像
		PUB_HOSTED_URL="https://pub.flutter-io.cn"
		FLUTTER_STORAGE_BASE_URL="https://storage.flutter-io.cn"
- 安装android studio，并在这里完成android开发的环境配置（注意在设置里手动勾选上cmdline）
		运行：
		flutter doctor  进行框架搭建程度的检验
		flutter doctor --android-licenses完成证书认证
- 想在vscode和android studio运行dart和flutter，需要安装相应的插件dart和flutter（注意：不需要用到的插件应尽量关闭）


## 安卓模拟
- 数据线连接手机
- 使用android stuio自带的手机模拟进行安卓端的调试

## 常用命令
flutter devices  查看相关的设备
flutter run         运行
flutter run -d windows   指定设备的运行
flutter clean
flutter pub get   下载依赖

## 快捷键
- 没啥用，idea里面自带的有对应的按键
- 保存即等效于热加载
![[Pasted image 20241129190501.png]]


# 结构
- build函数构建要搭建的组件
- 树结构
- 组件，书写自己的方法和属性，并指向子元素child或children 
### ⭐组件库⭐
- getwidget
- flutterlibrary
- fluent_ui

[![2024-06-17-172421.png](https://i.postimg.cc/nVGMRzkt/2024-06-17-172421.png)](https://postimg.cc/MXXWXzNs)

## 状态
### Stateless和Stateful  
### State
前二者的扩展
- 使用快捷键实现alt+enter实现Stateful和Statelsee之间的转化
- ```
```dart
//直接创建
class Choupage extends StatefulWidget {  
  const Choupage({super.key, required this.title});  
  @override  
  State<Choupage> createState() => _ChoupageState();  
}  
  
class _ChoupageState extends State<Choupage>
```

## 标识
### Context
小组件在 Widget 树中位置的**句柄。

### Key
- 组件在整个组件树中的唯一标识
- 常见的创建方式：
		const Myapp({super.key})         
- 和Context是一个东西

## 动态组件
- 可以进行状态的更改
- 不需要直接创建key
- 使用createState方法创建该组件的状态，在别的地方使用setState进行状态的更改
```Dart
class Try2Widget extends StatefulWidget {  
  @override  
  Try1Widgt createState() => Try1Widgt();  
}  
```



# 大组件

## 技巧
 - 左键  查看对应属性的需要的值的类型，大概属性需要调用该类的属性来使用
- flutter dev  组件的使用

## 容器
### 侧重于页面布局，无实际的大小
#### Align
- 可以控制其中元素的排布

#### Padding
- 一个提供给控件的和其他的控件之间的距离

#### Center
它的作用是将其子元素（child）在水平和垂直方向上都居中放置。`Center`小部件会尝试将其子元素放置在其父容器的中心位置。

以下是`Center`的一些关键特性：

1. 水平和垂直居中：`Center`会将其子元素在水平和垂直方向上都居中对齐。
2. **大小限制**：`Center`小部件本身没有固定的大小，它会根据子元素的大小和父容器的大小来确定自己的大小。如果子元素的大小超过了父容器的大小，那么子元素可能会被裁剪。
3. **单一子元素**：`Center`只能有一个子元素。如果你需要居中多个元素，可以考虑使用其他布局小部件，如`Row`或`Column`，并结合`mainAxisAlignment`和`crossAxisAlignment`属性来实现。
4. **不受父容器限制**：如果父容器没有指定大小，`Center`会尝试根据子元素的大小来确定自己的大小，但这可能会导致布局问题，因为Flutter的布局系统需要明确的约束来确定小部件的大小。
##### 示例：

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Center Example'),
        ),
        body: Center(
          child: Container(
            height: 100,
            width: 100,
            color: Colors.blueAccent,
            child: Text('Hello World'),
          ),
        ),
      ),
    );
  }
}
```

在这个例子中，`Center`小部件被用作`Scaffold`的`body`，它包含一个`Container`作为子元素。这个`Container`会在`Scaffold`的中心显示，因为它被`Center`小部件包裹。




### 占空间
#### Container

##### 示例：
```Dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Border Example'),
        ),
        body: Center(
          child: Container(
            height: 100,
            width: 100,
            color: Colors.blueAccent,
            border: Border(
              top: BorderSide(
                color: Colors.black, // 边框颜色
                width: 10, // 边框宽度
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```




#### Column和Row
 - 行和列，控制元素的行列的排布
 - 注意这个配合Expanded使用可以方便的实现页面的布局

#### Expended
- 填充现在的容器的剩下的空间

#### Listview 
- 使用一串的部件
- 可以实现滑动的效果


####  Drawer
- 抽屉
![[Pasted image 20241212172746.png]]


## builder
 - `builder` 把集合中的每个字符串都渲染成组件。
 ```dart
class MyApp extends StatelessWidget {
  final List<ListItem> items;
  const MyApp({super.key, required this.items});
  @override
  Widget build(BuildContext context) {
    const title = 'Mixed List';
    return MaterialApp(
      title: title,
      home: Scaffold(
        appBar: AppBar(
          title: const Text(title),
        ),
        body: ListView.builder(
          itemCount: items.length,
          itemBuilder: (context, index) {
            final item = items[index];
            return ListTile(
              title: item.buildTitle(context),
              subtitle: item.buildSubtitle(context),
            );
          },
        ),
      ),
    );
  }
}
```


## Provider
- 简化组件widget的管理




# 小组件

## Picture
在Flutter中处理图片是一个常见的需求，涉及到显示、加载、缓存、处理等多个方面。以下是一些基本的图片处理操作：

### 1. 显示图片

#### 本地图片

```dart
Image.asset(
  'assets/images/your_image.png',
  width: 100.0, // 指定宽度
  height: 100.0, // 指定高度
  fit: BoxFit.cover, // 填充模式
)
```

#### 网络图片

```dart
Image.network(
  'https://example.com/your-image.jpg',
  width: 100.0,
  height: 100.0,
  fit: BoxFit.cover,
)
```

### 2. 加载和缓存网络图片

对于网络图片，可以使用`CachedNetworkImage`来自动缓存图片，提高加载效率。

```dart
CachedNetworkImage(
  imageUrl: 'https://example.com/your-image.jpg',
  placeholder: (context, url) => CircularProgressIndicator(), // 加载中的占位符
  errorWidget: (context, url, error) => Icon(Icons.error), // 加载失败时的占位符
  width: 100.0,
  height: 100.0,
  fit: BoxFit.cover,
)
```

### 3. 图片缩放和裁剪

使用` BoxFit`来控制图片的缩放和裁剪行为：

- `BoxFit.cover`：保持图片宽高比，完全填充容器。
- `BoxFit.contain`：保持图片宽高比，完全包含在容器内。
- `BoxFit.fill`：不保持图片宽高比，完全填充容器。
- `BoxFit.fitWidth`：保持图片宽高比，宽度完全填充容器。
- `BoxFit.fitHeight`：保持图片宽高比，高度完全填充容器。
- `BoxFit.none`：不保持图片宽高比，也不完全填充容器。

### 4. 图片圆角和裁剪

使用`ClipRRect`或`ClipOval`来实现圆角或圆形图片：

```dart
ClipRRect(
  borderRadius: BorderRadius.circular(10.0),
  child: Image.network(
    'https://example.com/your-image.jpg',
    width: 100.0,
    height: 100.0,
    fit: BoxFit.cover,
  ),
)
```

```dart
ClipOval(
  child: Image.network(
    'https://example.com/your-image.jpg',
    width: 100.0,
    height: 100.0,
    fit: BoxFit.cover,
  ),
)
```

### 5. 图片滤镜

使用`ColorFiltered`来应用滤镜效果：

```dart
ColorFiltered(
  colorFilter: ColorFilter.mode(Colors.black.withOpacity(0.5), BlendMode.multiply),
  child: Image.network(
    'https://example.com/your-image.jpg',
    width: 100.0,
    height: 100.0,
    fit: BoxFit.cover,
  ),
)
```

### 6. 图片混合

使用`Stack`和`Positioned`来实现图片的叠加和混合：

```dart
Stack(
  children: [
    Image.network(
      'https://example.com/your-image.jpg',
      width: 100.0,
      height: 100.0,
      fit: BoxFit.cover,
    ),
    Positioned(
      bottom: 0,
      right: 0,
      child: Image.asset(
        'assets/images/overlay_icon.png',
        width: 30.0,
        height: 30.0,
      ),
    ),
  ],
)
```

这些基本操作可以帮助你在Flutter应用中处理和显示图片。根据你的具体需求，选择合适的方法来实现。





## TodoTile
- 待办事项
![[屏幕截图 2024-12-12 173951.png]]




## Icon
- 控制图标显示
- 可以使用一些其他的库：该链接指向的url:[Phosphor Icons](https://phosphoricons.com/?q=%22setting%22)
		使用：![[Pasted image 20241213125759.png]]
		正常的使用：
		![[Pasted image 20241213125829.png]]
## Tooltip
- 悬浮时出现提示的文字

## Button

在 Flutter 中，按钮是用户界面中非常重要的组成部分。Flutter 提供了多种类型的按钮，每种按钮都有其独特的特性和用途。根据你的应用需求和设计风格，可以选择最适合的按钮类型。以下是 Flutter 中常用的几种按钮及其使用场景和特点。

### 1. **ElevatedButton**

`ElevatedButton` 是一种带有阴影效果的按钮，默认情况下有轻微的提升效果，点击时会有动画反馈。它适合用作主要操作按钮。

#### 示例：

```dart
ElevatedButton(
  onPressed: () {
    // 按钮点击事件
  },
  child: Text('Elevated Button'),
)
```

#### 特点：

- 适用于主要操作。
- 默认有阴影和提升效果。
- 点击时有动画反馈。
- 可以通过 `style` 属性自定义按钮的样式，如颜色、边框、圆角等。

### 2. **TextButton**（文本按钮）

`TextButton` 是一种没有背景颜色的按钮，只有文字和可选的下划线。它适合用作次要操作或辅助操作。

#### 示例：
```dart
TextButton(
  onPressed: () {
    // 按钮点击事件
  },
  child: Text('Text Button'),
)
```

#### 特点：
- 适用于次要操作。
- 没有背景颜色，默认只有文字。
- 点击时有透明度变化的反馈。
- 可以通过 `style` 属性自定义按钮的样式，如文字颜色、下划线等。

### 3. **OutlinedButton**（带边框按钮）
`OutlinedButton` 是一种带有边框的按钮，通常用于次要操作或需要与 `ElevatedButton` 区分的场景。它有一个透明的背景和一个明显的边框。

#### 示例：
```dart
OutlinedButton(
  onPressed: () {
    // 按钮点击事件
  },
  child: Text('Outlined Button'),
)
```

#### 特点：

- 适用于次要操作。
- 带有边框，默认背景透明。
- 点击时有透明度变化的反馈。
- 可以通过 `style` 属性自定义按钮的样式，如边框颜色、宽度、圆角等。

### 4. **IconButton**（图标按钮）

`IconButton` 是一种只包含图标的按钮，适合用于工具栏、菜单等地方。它通常用于执行快速操作或导航。

#### 示例：
```dart
IconButton(
  icon: Icon(Icons.add),
  onPressed: () {
    // 按钮点击事件
  },
)
```

#### 特点：

- 适用于图标操作。
- 只显示图标，不显示文字。
- 点击时有透明度变化的反馈。
- 可以通过 `iconSize` 和 `color` 属性自定义图标大小和颜色。

### 5. **FloatingActionButton**（浮动按钮）

`FloatingActionButton` 是一种圆形的按钮，通常悬浮在屏幕的一侧，用于执行主要操作。它常用于添加新项目、保存等操作。

#### 示例：

dart

深色版本

```
FloatingActionButton(
  onPressed: () {
    // 按钮点击事件
  },
  child: Icon(Icons.add),
)
```

#### 特点：

- 适用于主要操作。
- 圆形按钮，默认有阴影效果。
- 通常放置在屏幕的右下角。
- 可以通过 `mini` 属性创建较小的浮动按钮。
- 可以通过 `backgroundColor` 和 `foregroundColor` 属性自定义按钮的颜色。

### 6. **CustomButton**（自定义按钮）

如果你需要更复杂的按钮样式或行为，可以使用 `GestureDetector` 或 `InkWell` 来创建自定义按钮。这种方式允许你完全控制按钮的外观和交互行为。

#### 示例：

```dart
GestureDetector(
  onTap: () {
    // 按钮点击事件
  },
  child: Container(
    padding: EdgeInsets.all(16.0),
    decoration: BoxDecoration(
      color: Colors.blue,
      borderRadius: BorderRadius.circular(8.0),
    ),
    child: Text(
      'Custom Button',
      style: TextStyle(color: Colors.white),
    ),
  ),
)
```

#### 特点：

- 完全自定义按钮的外观和行为。
- 适用于需要特殊样式或交互效果的场景。
- 可以结合 `Container`、`InkWell` 等小部件来实现复杂的效果。

### 7. **CupertinoButton**（iOS 风格按钮）

`CupertinoButton` 是用于 iOS 风格的应用程序中的按钮，提供类似于 iOS 的按钮样式。它适合用于 iOS 平台的应用，或者需要跨平台一致性的应用程序。

#### 示例：

```dart
CupertinoButton(
  onPressed: () {
    // 按钮点击事件
  },
  child: Text('Cupertino Button'),
)
```

#### 特点：

- 适用于 iOS 风格的应用。
- 提供类似于 iOS 的按钮样式。
- 可以通过 `color` 和 `padding` 属性自定义按钮的样式。

### 8. **DropdownButton**（下拉按钮）

`DropdownButton` 是一个下拉选择按钮，允许用户从多个选项中选择一个值。它适合用于需要选择的操作，如选择语言、主题等。

#### 示例：

```dart
String dropdownValue = 'Option 1';

DropdownButton<String>(
  value: dropdownValue,
  onChanged: (String? newValue) {
    setState(() {
      dropdownValue = newValue!;
    });
  },
  items: <String>['Option 1', 'Option 2', 'Option 3']
      .map<DropdownMenuItem<String>>((String value) {
    return DropdownMenuItem<String>(
      value: value,
      child: Text(value),
    );
  }).toList(),
)
```

#### 特点：

- 适用于选择操作。
- 提供下拉菜单功能。
- 可以通过 `items` 属性自定义选项列表。

### 9. **BackButton**（返回按钮）

`BackButton` 是一个内置的返回按钮，通常用于页面顶部的导航栏中。点击该按钮会触发页面返回操作。

#### 示例：

```dart
BackButton(
  onPressed: () {
    Navigator.pop(context);
  },
)
```

#### 特点：

- 适用于返回操作。
- 内置导航功能。
- 通常用于页面顶部的导航栏。

### 10. **CloseButton**（关闭按钮）

`CloseButton` 是一个内置的关闭按钮，通常用于对话框或弹出窗口中。点击该按钮会关闭当前页面或弹出窗口。

#### 示例：

```dart
CloseButton(
  onPressed: () {
    Navigator.pop(context);
  },
)
```

#### 特点：

- 适用于关闭操作。
- 内置关闭功能。
- 通常用于对话框或弹出窗口。

### 总结

- **ElevatedButton**：适用于主要操作，带有提升效果。
- **TextButton**：适用于次要操作，无背景颜色。
- **OutlinedButton**：适用于次要操作，带有边框。
- **IconButton**：适用于图标操作，通常用于工具栏或菜单。
- **FloatingActionButton**：适用于主要操作，圆形按钮，常用于添加或保存操作。
- **CustomButton**：适用于需要自定义样式的场景。
- **CupertinoButton**：适用于 iOS 风格的应用。
- **DropdownButton**：适用于选择操作，提供下拉菜单功能。
- **BackButton** 和 **CloseButton**：适用于返回和关闭操作，内置导航功能。

### 选择按钮的最佳实践

1. **根据操作的重要性选择按钮类型**：
    
    - 主要操作（如提交、保存）使用 `ElevatedButton`。
    - 次要操作（如取消、编辑）使用 `TextButton` 或 `OutlinedButton`。
    - 图标操作使用 `IconButton`。
    - 浮动操作（如添加新项目）使用 `FloatingActionButton`。
2. **保持一致性**：
    
    - 在整个应用中保持按钮样式的统一性，确保用户能够轻松识别不同类型的按钮。
    - 使用 `ThemeData` 统一管理按钮的样式，确保全局一致性。
3. **考虑平台差异**：
    
    - 如果你开发的是跨平台应用，建议根据平台选择合适的按钮样式。例如，在 iOS 应用中使用 `CupertinoButton`，在 Android 应用中使用 `ElevatedButton`。
4. **提供清晰的反馈**：
    
    - 确保按钮在点击时有明显的视觉反馈（如颜色变化、动画等），以提升用户体验。

# 样式
在 Flutter Web 应用中，如果你遇到加载字体文件（如 Roboto 字体）失败的问题，你可以通过以下几种方法手动配置字体：
## 文字
### 1. 使用本地字体文件

将字体文件添加到你的 Flutter 项目中，并在代码中引用它们。

#### a. 添加字体文件

将字体文件（例如 `.ttf` 或 `.otf`）添加到你的 Flutter 项目中，通常放在 `assets/fonts` 目录中。

#### b. 更新 `pubspec.yaml`

在 `pubspec.yaml` 文件中，添加字体文件的路径：

```yaml
flutter:
  fonts:
    - family: Roboto
      fonts:
        - asset: assets/fonts/Roboto-Regular.ttf
        - asset: assets/fonts/Roboto-Bold.ttf
          weight: 700
```

#### c. 在 Flutter 代码中使用字体

在你的 Flutter 代码中，使用 `Text` 小部件并指定字体。例如：

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Web Font Example',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        textTheme: TextTheme(
          bodyText2: TextStyle(fontFamily: 'Roboto'),
        ),
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Roboto Font Example'),
      ),
      body: Center(
        child: Text(
          'Hello, World!',
          style: TextStyle(fontSize: 24),
        ),
      ),
    );
  }
}
```

### 2. 使用 Google Fonts

如果你仍然希望使用 Google Fonts，但遇到加载问题，可以尝试以下方法：

#### a. 使用 `<link>` 标签

在你的 `web/index.html` 文件中，添加一个 `<link>` 标签来引用 Google Fonts。例如：

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>My Flutter Web App</title>
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
</head>
<body>
  <script src="main.dart.js" type="application/javascript"></script>
</body>
</html>
```

#### b. 在 Flutter 代码中使用字体

在你的 Flutter 代码中，使用 `Text` 小部件并指定字体。例如：

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Web Font Example',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        textTheme: TextTheme(
          bodyText2: TextStyle(fontFamily: 'Roboto'),
        ),
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Roboto Font Example'),
      ),
      body: Center(
        child: Text(
          'Hello, World!',
          style: TextStyle(fontSize: 24),
        ),
      ),
    );
  }
}
```

### 3. 检查网络和跨域问题

确保你的网络连接正常，并且没有跨域问题。如果你在本地开发环境中遇到问题，尝试在不同的网络环境中运行你的应用。

### 4. 检查服务器和代理设置

如果你的应用部署在服务器上，确保服务器配置允许从 Google Fonts 服务器加载资源。你可能需要在服务器上设置适当的 CORS 策略。

通过以上步骤，你应该能够解决加载 Roboto 字体的问题。如果问题仍然存在，请检查具体的错误信息，并根据需要调整配置。希望这些信息能帮助你解决问题！如果还有其他问题，请随时提问。


## 间距
### Padding?


### Margin
- 外边距


### border
- 内边距
- 容器的属性



#### 现成的美观方案：渐变
选择颜色时，可以参考以下几种常见的渐变配色方案：
- **冷色调渐变**：蓝色 -> 紫色 -> 深紫色
- **暖色调渐变**：橙色 -> 红色 -> 粉色
- **自然色调渐变**：绿色 -> 黄色 -> 橙色
- **科技感渐变**：深蓝色 -> 深紫色 -> 黑色
- **柔和渐变**：浅蓝色 -> 浅粉色 -> 白色
##### 示例
- 实现的效果还算可以
```Dart
decoration: BoxDecoration(  
  gradient: LinearGradient(  
    begin: Alignment.topLeft,  
    end: Alignment.bottomRight,  
    colors: [  
      // Colors.deepPurple,  
      // Colors.pinkAccent,  
      Colors.blue.shade100,  
      Colors.pink.shade100,  
      Colors.white  
    ],  
  ),  
  borderRadius: BorderRadius.circular(20.0), // 圆角  
  boxShadow: [  
    BoxShadow(  
      color: Colors.black.withOpacity(0.2),  
      spreadRadius: 5,  
      blurRadius: 7,  
      offset: Offset(0, 3), // 阴影偏移  
    ),  
  ],  
  // color: Colors.lightBlueAccent,  
),
```


## ios样式
```dart
import 'package:flutter/cupertino.dart';//提供ios似的样式风格  
  
void main() {  
  runApp(const CupertinoApp(  
    title: 'Navigation Basics',  
    home: FirstRoute(),  
  ));  
}  
  
class FirstRoute extends StatelessWidget {  
  const FirstRoute({super.key});  
  
  @override  
  Widget build(BuildContext context) {  
    return CupertinoPageScaffold(  
      navigationBar: const CupertinoNavigationBar(  
        middle: Text('First Route'),  
      ),  
      child: Center(  
        child: CupertinoButton(  
          child: const Text('Open route'),  
          onPressed: () {  
            Navigator.push(  
              context,  
              CupertinoPageRoute(builder: (context) => const SecondRoute()),  
            );  
          },  
        ),  
      ),  
    );  
  }  
}  
  
class SecondRoute extends StatelessWidget {  
  const SecondRoute({super.key});  
  
  @override  
  Widget build(BuildContext context) {  
    return CupertinoPageScaffold(  
      navigationBar: const CupertinoNavigationBar(  
        middle: Text('Second Route'),  
      ),  
      child: Center(  
        child: CupertinoButton(  
          onPressed: () {  
            Navigator.pop(context);  
          },  
          child: const Text('Go back!'),  
        ),  
      ),  
    );  
  }  
}
```


# 页面逻辑
## Provider
[Provider](https://so.csdn.net/so/search?q=Provider&spm=1001.2101.3001.7020) 是一个 Flutter 的插件包，旨在简化状态管理和依赖注入。它使用 InheritedWidget 作为底层实现，通过提供一种订阅与更新的机制，能够让应用在状态变化时自动刷新对应的 UI，极大地提升了开发体验。



### 导航
- 手机端的话好像是使用push自动加上返回
- 电脑端其实浏览器有自带的
#### 实现
- 在主页面的Material中加上
```dart
//路由的配置
Map<String, WidgetBuilder> routes = {
  '/': (context) => HomePage(),
  '/newPage': (context) => NewPage(),
};
MaterialApp{
title:"",
home:Mypage(),
routes: routes
}
```

- 跳转
```dart
onTap: (){
//Navigator.pop(context); 
Navigator.pushNamed(context, '/newPageWithArguments', arguments: 'Some arguments');
}
```

- 跳转到指定的页面
使用`Navigator.popUntil()`
如果你需要返回到特定的页面，而不是仅仅返回上一个页面，你可以使用`Navigator.popUntil()`。
```dart
// 返回到根页面
Navigator.popUntil(context, (route) {
  return route.isFirst;
});
```


## 网络请求
```dart
Future<void> _sendRequest() async {  
  String input = _controller.text;  
  if (input.isEmpty) return;  
  
  //构建请求  
  Uri url = Uri.parse('http://localhost:5000/api');  
  Map<String, String> queryParams = {'message': input};  
  String queryString = Uri(queryParameters: queryParams).query;  
  Uri requestUrl = Uri.parse('$url?$queryString');  
  
  //发出请求  
  try {  
    final response = await http.get(requestUrl);  
    if (response.statusCode == 200) {  
      var responseBody = jsonDecode(response.body);  
      setState(() {  
        _response = responseBody['message'] ?? 'No response';  
      });  
    } else {  
      setState(() {  
        _response = 'Failed to fetch data';  
      });  
    }  
  } catch (e) {  
    setState(() {  
      _response = 'Request failed: $e';  
    });  
  }  
}
```

## 特定要求的组件的实现

### 侧栏的实现方式

### 页面的局部刷新
- 使用listview和组件的函数操控Setstate函数调整全局变量进行控制

### 滚动效果的实现
在Flutter中，`Column` 组件本身并不提供滚动功能。`Column` 只是一个垂直布局组件，用于按顺序垂直排列其子组件。如果你的页面内容超出了屏幕的可视范围，你需要使用其他组件来实现滚动效果。

为了给 `Column` 添加滚动效果，你可以将其包裹在 `SingleChildScrollView` 组件中，这样当内容超出屏幕大小时，用户就可以滚动查看所有内容。下面是一个简单的例子：

```dart
SingleChildScrollView(
  child: Column(
    children: <Widget>[
      // 你的子组件列表
      Container(height: 200.0, color: Colors.red),
      Container(height: 200.0, color: Colors.blue),
      // 更多子组件...
    ],
  ),
)
```

在这个例子中，`Column` 中的每个 `Container` 都设置了固定的高度，当这些 `Container` 的总高度超过屏幕高度时，`SingleChildScrollView` 允许用户通过滚动来查看所有的 `Container`。

如果你想要水平滚动，可以使用 `Row` 代替 `Column`，并将 `SingleChildScrollView` 的 `scrollDirection` 属性设置为 `Axis.horizontal`：

```dart
SingleChildScrollView(
  scrollDirection: Axis.horizontal,
  child: Row(
    children: <Widget>[
      // 你的子组件列表
      Container(width: 200.0, height: 100.0, color: Colors.red),
      Container(width: 200.0, height: 100.0, color: Colors.blue),
      // 更多子组件...
    ],
  ),
)
```

这样，用户就可以水平滚动来查看所有的 `Container` 组件。




# 问题
## 图标不能正常的显示
- 清理缓存：
		flutter clean
- 安装依赖：
		flutter pub get


与其使用 `Stack`，应该使用 `Column` 并在其中包含一个 `Expanded` 的 `ListView`，这样可以自然地支持滚动。
## 中文不能正常加载
- 刷新可以解决，可能有别的方法





## 页面资源存储问题的解决





## 对于现在ai使用中出现的问题以及解决方案（try）

### 回复的信息趣味性或者专业性不足

- 专业性
	- 对文献进行检索，并保留文献的查阅记录，可以使用一个侧栏进行

- 趣味性
	- 人群判断



### 主动性
- 通常并不会主动的发起交流
	- 首先ai要对当前信息有一个概况，对用户情况有所了解(信息过滤)
	- 



### 不同的ai可交流的对象只有一个

- 利用不同的api实现多开







# 包

| name             | effect                        |
| ---------------- | ----------------------------- |
| http             | 网络请求                          |
| provider         | 流行的状态管理库，它使得在整个应用中传递数据变得简单而高效 |
| goodlefont       | goodle字体扩展                    |
| phosphor_flutter | icon库                         |



# 单词记忆

| 单词          | 含义     |
| ----------- | ------ |
| alignment   | 对齐方式   |
| sized       | 特定大小的  |
| Directional | 定向的    |
| horizontal  | 水平的    |
| textAlign   | 文本对齐方式 |
|             |        |
|             |        |
