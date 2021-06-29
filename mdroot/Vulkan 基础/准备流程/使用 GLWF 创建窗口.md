## 使用 GFLW 创建窗口

这里使用GLFW（Graphics Library Framework）初始化一个窗口。GLFW 具体是做什么的可以直接去维基看（https://zh.wikipedia.org/zh-hans/GLFW，其实说的也很简练，最好直接去官网看doc）。

一个使用 GLFW 完整驱动的大致流程如下：

```c++
glfwInit();
glfwWindowHint(EnumValue，ActualValue) // *
window = glfwCreateWindow(WIDTH, HEIGHT, "Vulkan", nullptr, nullptr);

void mainLoop() {
    while (!glfwWindowShouldClose(window)) {
        glfwPollEvents(); // Window resize, mouse move event, etc.
    }
}

glfwDestroyWindow(window);
glfwTerminate();
```

这里直接通过方法名称就可以大致知道到底是干嘛的了。在第二行我们使用 `glfwWindowHint()` 方法向 GLFW 库传递创建窗口的选项。由于这个库兼容 C，所以初始化参数就很暴力美学，即通过多次调用传递参数给 GLFW。

常用的 `WIndiwHint` 组合如下：

```c++
glfwWindowHint(GLFW_RESIZABLE, GLFW_FALSE); // 不允许调整窗体大小，因为调整大小涉及到整个流水线变动，这里先不考虑那么复杂的
glfwWindowHint(GLFW_CLIENT_API, GLFW_NO_API); // 不是 OpenGL，不创建上下文！
```

当然全部的 Hint 可以前往 https://www.glfw.org/docs/latest/window.html 的 xxx related hints 章节来找到，也可以直接查看 `glfw3.h` 文件，里面的注释详细疯了，好评。

最最最完整的 GLFW 教程当然在官网的 Tutorial 里面了：https://www.glfw.org/docs/latest/vulkan_guide.html