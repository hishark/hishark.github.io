
抛弃冗余的嵌套布局，来试试清爽的 ConstraintLayout 吧。

<!--more-->


> ConstraintLayout 可以使用扁平控件层次结构（无嵌套控件组）来创建复杂的大型布局。它与 RelativeLayout 相似，其中所有的控件均根据同级控件与父布局之间的关系进行布局，但其灵活性要高于 RelativeLayout，并且更易于与 Android Studio 的布局编辑器配合使用。
>
> ConstraintLayout 的所有功能均可直接通过布局编辑器的可视化工具来使用，因为布局 API 和布局编辑器是专为彼此构建的。 因此，我们完全可以使用 ConstraintLayout 通过拖放的形式（而非修改 XML）来构建布局。


## 1. 如何添加

如果要在项目中使用 `ConstraintLayout` ，需要确保两点：

在模块级别的 `build.gradle` 文件中声明 `maven.google.com` 代码库：

```java
repositories {
	google()
}
```

在模块级别的 `build.gradle` 文件中添加 `ConstraintLayout` 库作为依赖项。（此处版本为 2.0.0）

```java
dependencies {
    implementation "androidx.constraintlayout:constraintlayout:2.0.0"
}
```

## 2. 转换布局

如果想将其他布局转换为 `ConstraintLayout` 约束布局，可以直接在 Component Tree 窗口中，右键该布局，点击 **Convert xxx to ConstraintLayout** 即可。

<img src="https://developer.android.google.cn/training/constraint-layout/images/layout-editor-convert-to-constraint_2x.png?hl=zh-cn" width="400">

## 3. 约束条件

要在 `ConstraintLayout` 中定义某个控件的位置，必须为该控件添加至少一个水平约束条件和一个垂直约束条件。

每个约束条件均定义了控件在竖轴或者横轴上的位置，同时均表示了当前控件与其他控件、父布局或隐形引导线之间的连接或对齐方式。因此每个控件在每个轴上都至少有一个约束条件，但通常情况下会需要更多约束条件。

当我们将控件拖放到布局编辑器中时，即使没有任何约束条件，它也会停留在放置的位置。但是当运行应用后，若一个控件没有任何约束条件，则会在位置 [0,0]（即左上角）处进行绘制。

例如，在下图中，布局在编辑器中看着很完美，没什么问题，但是由于控件 C 上没有垂直约束条件，所以它会显示在屏幕的顶部。

![](https://developer.android.google.cn/training/constraint-layout/images/constraint-fail_2x.png?hl=zh-cn)



下图对控件 C 添加了垂直约束条件，所以控件 C 会乖乖的处于控件 A 的正下方。

![](https://developer.android.google.cn/training/constraint-layout/images/constraint-fail-fixed_2x.png?hl=zh-cn)

> 缺少约束条件并不会导致编译错误，但是布局编辑器会将缺少约束条件作为错误显示在工具栏中。

### 3.1 添加引导线约束

![img](https://developer.android.google.cn/training/constraint-layout/images/guideline-constraint_2x.png?hl=zh-cn)

可以添加垂直或水平的引导线来约束控件，该引导线是隐形的，我们可以根据相对于布局边缘的 dp 单位或百分比在布局中定位引导线。

要创建引导线，请点击工具栏中的 Guidelines，然后点击 Add Vertical Guideline 或 Add Horizontal Guideline。

拖动虚线将其重新定位，然后点击引导线边缘的圆圈以切换测量模式。

### 3.2 添加屏障约束

要创建屏障，按照以下步骤操作：

1. 点击工具栏中的 Guidelines 图标 ，然后点击 Add Vertical Barrier 或 Add Horizontal Barrier。
2. 在 Component Tree 窗口中，选择要放入屏障内的控件，然后将其拖动到屏障组件中。
3. 在 Component Tree 中选择屏障，打开 Attributes 窗口，然后设置 barrierDirection。

<!-- 现在，您可以从另一个控件创建屏障约束。 -->

我们还可以将屏障内的控件约束到屏障。这样就可以确保屏障中的所有控件始终相互对齐，即使我们并不知道哪个控件最长或最高。同时，还可以在屏障内添加引导线，以确保屏障的位置“最小”。


与引导线类似，屏障是一条隐藏的线，我们可以用它来约束控件。屏障不会定义自己的位置。相反，屏障的位置会随着其中所含控件的位置而移动。如果希望将控件限制到一组控件而不是某个特定控件时，屏障约束就非常好用。

例如在下图中，控件 C 被约束在屏障的右侧。该屏障设置为控件 A 和控件 B 的右侧。因此，屏障根据控件 A 或控件 B 的右侧是否为最右侧来移动。

<img src="https://developer.android.google.cn/training/constraint-layout/images/barrier-constraint_2x.png?hl=zh-cn" width="400">

### 3.2 创建约束条件

1. 将控件从 Palette 窗口拖到编辑器中。
   当在 `ConstraintLayout` 中添加控件时，该控件会显示一个边界框，每个角上都有用于调整大小的方形按钮，每条边上都有圆形的约束按钮。

2. 点击控件将其选中。

3. 执行以下任一操作都可成功创建约束条件：
   - 点击约束按钮并将其拖动到可用定位点。 此定位点可以是另一控件的边缘、布局的边缘或者引导线。当拖动约束按钮时，布局编辑器会显示可行的连接定位点和蓝色叠加层。
   - 点击 Attributes 窗口的 Layout 部分中的 Create a connection 按钮。

另外，创建约束条件时需要注意几个规则：

- 每个控件至少有两个约束条件：一个水平约束条件，一个垂直约束条件。
- 只能在共用同一平面的约束按钮与定位点之间创建约束条件。因此，控件的垂直平面（左侧和右侧）只能约束在另一个垂直平面上；而基准线则只能约束到其他基准线上。
- 每个约束按钮只能用于一个约束条件，但可以在同一定位点上创建多个约束条件（从不同控件引出的）。

### 3.3 移除约束条件
可以通过以下任意操作移除约束条件：

1. 点击某个约束条件将其选中，然后按 Delete。
2. 按住 Control（在 macOS 上为 Command），然后点击某个约束定位点。请注意，该约束条件变为红色即表示可以点击将其删除。
3. 在 Attributes 窗口的 Layout 部分中，直接点击某个约束定位点将其删除即可。

## 4. 自动创建约束条件
我们可以将每个控件移动到希望的位置，然后点击 Infer Constraints 自动创建约束条件。

Infer Constraints 会扫描布局，以便为所有控件确定最有效的约束集。它会尽可能将控件约束在当前位置，我们可能需要进行一些调整，以确保布局能够按照预期自适应不同的屏幕尺寸和方向。

Autoconnect to parent 是可以启用的独立功能。启用后，当我们将子控件添加到父控件时，此功能会自动为每个控件创建两个或多个约束条件，但前提是可以将子控件约束到父布局。Autoconnect 不会为布局中的其他控件创建约束条件。

Autoconnect 在默认情况下处于停用状态。点击布局编辑器工具栏中的 Enable Autoconnection to Parent，即可启用该功能。

## 参考

[使用 ConstraintLayout 构建自适应界面 - Android Developers](https://developer.android.google.cn/training/constraint-layout?hl=zh-cn)

