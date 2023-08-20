# 你好，世界！

```C
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
```

以上就是一段经典的 C 语言入门代码，如果你完全没有接触过编程，那么这样一段代码可能会让你很懵圈，不过不要紧，接下来就让我们的黑盒思维派上用场。你不需要知道什么是 `#include`，什么是 `main`，什么是 `printf`，你不需要知道在哪里要写括号、花括号、分号，你也不需要知道什么是编译器。但是如果你把以上代码复制粘贴到某个在线编译器中，并且点击运行，你应该能够从某个框框里看到“Hello, World!”被显示了出来，这就是这段代码的作用：当你编译运行它后，它会打印（你现在可以把打印理解成从某个框框中显示一些东西）出“Hello, World!”。如果把这段代码想象成一个黑盒，那么它没有什么输入，有“Hello, World!”这样一个输出。

## 打开黑盒说亮话

接下来就让我们拆开这个大黑盒，一步一步地理解这段代码，一点一点地把这个大黑盒分解成若干个小黑盒，从而变成一个灰盒。请跟着我一起想象：第一个小黑盒上面写着 `main`，你可以把一些特定的盒子按照一定顺序放进去，这些个特定的盒子就会按照摆放的顺序被依次触发，但是它还有一个特点，就是上面一般要放上一个具有对应类型（在这里是 `int`，可以暂时理解为整数）的 `return` 盒子，才能够正常结束；第二个小黑盒上面写着 `printf`，它可以把放在它上面的字符串，按照一定的格式打印出来；第三个小黑盒上面写着 `return`，如果 `main` 遇到了它，就会直接返回它上面的信息（可以暂时理解成是和打印不同的另一种输出），而不再触发后续的盒子；第四个盒子上面写着 `#include`，它里面装着一些其它盒子（其中就有 `printf`） 的电源，如果没有这个盒子，那些盒子就很可能会失效（除非有其它相对应的电源）。总结起来就是，我们想要打印出“Hello, World!”，于是想到了盒子 `printf`，并且把“Hello, World!”放了上去，为了触发它，我们再把 `printf` 放进了 `main` 里面，但是这个时候的 `printf` 没有电，我们需要把电源从 `<stdio.h>` 里面拿出来，所以使用了 `#include`，最后，想让 `main` 正常结束，我们在 `main` 的末端放置了一个上面有 `0` 的 `return`（暂时就记住一般 `main` 返回 `0` 代表正常结束）。

可以看出，对于初学者来说，即便是一小段最为简单的代码，也要分解成许多个黑盒去理解，不过不要紧，在最初接触某个领域时，这再正常不过了，我们不要急于求成，想着去弄明白所有的细节（比如为什么 `0` 代表正常结束，什么算非正常结束等等），我们只要多看看代码，多写写代码，哪怕是加减乘除比个大小都行，主要是熟悉一下 C 语言的形状。慢慢地，相信各位读者就会自然而然地对某些细节产生印象。