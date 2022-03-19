**首先需要感谢** [Achuan](https://github.com/Achuan-2/siyuan-themes-tsundoku-light)**和**[Cliff](https://github.com/Crowds21)
--- 
😀开发时间：**大三**

因为马上要考研了，所以接下来应该不会在更新，很抱歉。市集还有很多好玩，很美的主题，大家都可以尝试一下。
---

## 这个主题整体是倾向于，美观！清新

### 每一个段落都是青，绿，蓝组成，你会发现长篇的笔记，看着会很舒服。

#### 当然也不炫酷。

## 开发背景

这是我在大三的时候偶然接触到的Siyuan笔记，（也就是2021年了），原因也很简单。一直用的typora收费了，就转Siyuan了。结果！Siyuan真好用，后面就想着捣鼓着玩，就自己套用别人的主题，去换了一些颜色，和配置一些好玩的东西。

## 样例展示：

## 第七章：输入/输出系统

### 基本知识点

1. 中断向量是指`​中断服务程序的入口地址`
2. 中断执行`保护现场的操作是` **硬件完成，而不是调用软件执行**
3. 磁盘的地址image.png[^1]（按照`驱动器，盘面，磁道，扇区（大小排序）`，==驱动器，磁道，盘面，扇区==）
4. 磁盘的`传输时间`计算：

    $T = T_s + \frac{1}{2*r} + \frac{Data}{D_r} \\D_r = r * N \\r是磁盘的转速，Data是要读取的数据大小\\D_r 是数据的传输率,N是每条磁道的容量 \\这个公式是读取一个磁道的时间$
5. 磁盘读取`最小单位是扇区`
6. 磁盘格式化的内存大小计算：

    1. $格式化容量 = 面数 * 每面的磁道数 * 每个磁道的扇区数 * 扇区的字节数$
    2. $格式化容量 = 面数 * （外半径 - 内半径）*道密度 * 每个磁道的扇区数 * 扇区数$
    3. 磁盘存储空间计算例题[^2]（**注意**：`道密度指圆上的道的数量(与半径有关)，位密度是一个道包含多少bit` ==注意==：位密度有外，内之分）
7. `DMA`实现中断，也需要借助中断系统，DMA的请求是在机器周期结束的时候，中断请求是在指令结束的时候。


---

`这是一段代码`,**（tarjan 缩点）**

```cpp
#include <bits/stdc++.h>

using namespace std;
const int maxn = 1e5+100;
vector<int> edge[maxn];//无向图
set<int> ans;
int dfn[maxn] , low[maxn] , tot ;

void tarjan(int now , int father)
{
    dfn[now] = low[now] = ++tot;
    int child = 0;
    for(int i = 0 ; i < edge[now].size() ; i ++)
    {
        int to = edge[now][i];
        if(!dfn[to])
        {
            tarjan(to , father);
            low[now] = min(low[now] , low[to]);
            if(low[to] >= dfn[now] && now != father) ans.insert(now);
            if(now == father ) child++;
        }
        low[now] = min(low[now] , dfn[to]);
    }
    if(child >= 2 && now == father) ans.insert(now);
}
int main()
{
    int n, m;
    cin >> n >> m;
    for (int i = 1; i <= m; i ++)
    {
        int from , to;
        cin >> from >> to;
        edge[from].push_back(to);
        edge[to].push_back(from);
    }

    for(int i = 1; i <= n ; i ++)
        if(!dfn[i])
            tarjan(i , i);

    cout << ans.size() << endl;
    for(auto it = ans.begin() ; it!= ans.end() ; it++)
    {
        cout << *it <<" ";
    }
}
```
