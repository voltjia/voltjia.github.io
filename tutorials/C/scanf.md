# 回声

很好，我们已经讲了黑盒的概念，并且还讲了 C 语言中的一种输出方式（`printf`），但是对于一个盒子来说，光有输出是不行的，我们还要懂得如何输入。所以与 `printf` 相对的，我们有着一个写着 `scanf`（“scan formatted”）的盒子，同样是使用 `<stdio.h>` 里的电源供电。

```C
#include <stdio.h>

int main() {
    char s[128];
    scanf("%s", s);
    printf("%s\n", s);
    return 0;
}
```

如果大家运行了这段代码，在框框里输入一段字符，并且回车，那么你会看到程序会再打印出一行相同的字符，比如如果我输入 `Hello!` 之后回车，那么将会有如下显示。

```
Hello!
Hello!
```

其中第一行是我的输入，第二行则是程序的输出。是不是很像在山谷里大喊了一声，听到了山谷传来的回音。除了 `scanf` 之外，我们看到了一行熟悉又陌生的 `char s[128];`，大家有没有觉得，这非常像我们之前提到的声明变量的形式，有一个名字 `s`，前面还有个 `char`。没错，这就是个变量声明，`char` 是一个新的类型，是英文 character 的缩写，可以存放一个字符，就像之前提到的 `'a'`、`'1'`、`'!'` 之类的。那么问题来了，后面的 `[128]` 是啥意思呢？这里我们就要再引入一个新的概念：数组。想象一个柜子，柜子上按顺序有好几个抽屉，每个抽屉都存储了相同类型的东西，这样一个柜子，就是数组。而 C 语言当中，声明一个数组的方式，就是在名称后面加上方括号，方括号中间放入这个柜子当中有多少个抽屉。换句话说，`char s[128];` 声明了一个带有 `128` 个抽屉的柜子，其中每个抽屉可以用来存储一个 `char`，并且把它命名为了 `s`。

有了柜子 `s`，我们就可以进一步解释 `scanf` 了，它会按照第一个输入（一个格式化的字符串）所表示的格式，读取用户的输入，然后放入后面的指定位置。比如，`scanf("%s", s);`，就是读取一个字符串（`%s` 这个占位符对应的就是字符串，可以记成 s 是英文 string 的首字母），然后把它放进后面的柜子 `s` 里。细心的读者可能会有疑问：上面说 `s` 是个数组，这里怎么能存放字符串呢？很好的问题，因为 C 语言比较精简，本身几乎没有附带什么数据结构，所以一般 C 语言所说的字符串，就是一个字符数组，只不过以 `'\0'` 这样一个特殊的字符结束。对于 `'\0'`，大家可以这么理解，一个柜子可以比较大，但是我们却不一定能使用全部抽屉，那么我们知道一个字符串从第一个抽屉开始，到哪里结束呢？答案就是到 `'\0'` 结束。就像我们正在讲的 `s`，它有 `128` 个抽屉，但是我们刚才用到的只有 `6` 个（因为 `"Hello!"` 里面有 `6` 个字符：`'H'`、`'e'`、`'l'`、`'l'`、`'o'`、`'!'`）。于是，`scanf` 就一个字符一个字符地读取了我们的输入，放到了 `s` 的抽屉里面，在放完之后，最后又放了一个 `'\0'` 来标志字符串终止了。这样，下一行，我们的老朋友 `printf`，看到了 `%s` 以后，就会去后面找字符串，于是发现了 `s` 这个柜子，然后一个抽屉一个抽屉地把字符拿出来打印出来，最后翻到一个抽屉里是 `'\0'` 的时候，它就意识到，哦，到这就该结束了，然后就结束了打印。

```C
#include <stdio.h>

int main() {
    int a;
    scanf("%d", &a);
    printf("%d\n", a);
    return 0;
}
```

同样，如果我们声明一个整形变量（让咱们来慢慢适应编程术语，其实就是装整数的抽屉）`a`，并且把 `scanf` 和 `printf` 当中的占位符替换成 `%d`（还记得我们之前介绍过的，是用来给整形占位的），那么这个程序就会变成，我们输入一个整数，然后程序再打印出这个整数。比如如果我们输入 `128`，那么将会有以下显示。

```
128
128
```

很明显，从“回声”这个标题的意义上讲，使用字符数组能够达到的效果更贴合它的意思，因为 `%d` 版本的程序只能够正确反应整数。但有仔细的读者可能已经发现了，这次的 `scanf` 后面的 `a`，前面带着一个 `&`，这是为什么呢？还记得我们之前讲过，每一个抽屉都有一个确定的位置和名称，尽管抽屉里面的内容会变化，但是抽屉的位置不会变化。而在 C 语言当中，每当我们想要使用某个抽屉里面的东西，我们其实是把里面的东西拿出来，复制一份相同的，然后把副本放到其它盒子的输出上面，而不是抽屉本身。这样的好处是，盒子在修改这个东西的时候，原来的抽屉里面的东西并不会改变，也就增强了程序的稳定性，否则万一改来改去的，说不定就会出啥问题。但是这样的话问题就来了，如果我们就是想让一个盒子修改这个东西怎么办？有一个好办法就是，我们不传递给它这个东西，而是传递给它一个位置，这样我管这个位置到底是原件还是副本还是什么，如果我是这个盒子，我是不是可以拿着这个位置，直接定位到这个抽屉，然后就能进一步修改里面的东西了？没错，这个 `&` 在这里就是取抽屉的位置的意思。所以 `scanf("%d", &a);` 就能够理解成，`scanf` 拿到了一个抽屉的位置，它读取了一个整数，然后找到了这个抽屉，把整数放了进去。

有同学说：那不对啊，那为啥之前的那个 `%s`，就用不着 `&`？要是这么说，如果没有 `&`，我们不就是传递的 `s` 的副本，而不是本身？这是一个很好的问题，也正是我为什么讲了 `%s` 版本的回声程序之后，还要引入一个 `%d` 的，就是为了区分二者。之前说，在 C 语言当中，传递抽屉的时候，其实传递的是副本，需要复制一下。我们能这么做，很大的原因是抽屉比较小。而一个柜子，里面可能有成百上千个抽屉，如果我们还是要复制，那岂不是要费很大的功夫？所以对于一个柜子来说，C 语言默认是传递第一个抽屉的位置，而不再是副本，这样一来，由于柜子当中，抽屉的位置是一个接一个的，我们有了第一个抽屉的位置，就可以找到所有的抽屉了。比如我们想找第 `3` 个抽屉，那就从第一个开始往后数就行了。

```C
#include <stdio.h>

int main() {
    char s[128];
    scanf("%s", &s[0]);
    printf("%s\n", s);
    return 0;
}
```

所以说，`s` 其实就跟 `&s[0]`（现在可以把 `s[i]` 理解成找到柜子 `s` 当中的第 `i + 1` 个抽屉就行，所以 `s[0]` 就是第一个抽屉）几乎一样。你这么写这个程序，效果是一样的。总结起来就是，C 语言里面传递单一变量的时候是传递的副本而非本身，而使用数组的时候，实则使用的是数组的第一个元素的地址。