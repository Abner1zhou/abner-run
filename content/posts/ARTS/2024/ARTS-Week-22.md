+++
title = 'ARTS Week 22, 2024'
date = 2024-06-02
draft = false
categories = ["ARTS"]
tags = ["Docker", "Frontend"]
+++
## 1.Algorithm

[575. 分糖果](https://leetcode.cn/problems/distribute-candies/)

### 集合set

设糖果数量为 n，由于妹妹只能分到一半的糖果，所以答案不会超过 n/2，同时设这些糖果一共有 m 种，答案也不会超过 m。

```Python
class Solution:
    def distributeCandies(self, candyType: List[int]) -> int:
        n = len(candyType)
        m = len(set(candyType))
        if n / 2 < types:
            return int(n / 2)
        else:
            return int(m)
```

### 暴力法

生成代表糖果的给定 `nums`数组的所有排列，并确定所生成数组前半部分中唯一元素的数目。
*ps: 假设无法直接使用的 SET 的情况下使用*

### 优化的暴力法

女孩能得到的唯一糖果的最大数量可以是n/2，如果独特的糖果数量低于n/2的话，为了使女孩能得到的独特的糖果数量最大化，我们会将所有独特的糖果分配给女孩。因此，在这种情况下，女孩得到的独特糖果数量等于给定`candies`数组中的独特糖果总数。

### 排序

```java
public class Solution {
    public int distributeCandies(int[] candies) {
        Arrays.sort(candies);
        int count = 1;
        for (int i = 1; i < candies.length && count < candies.length / 2; i++)
            if (candies[i] > candies[i - 1])
                count++;
        return count;
    }
}
```

## 2.Review

[You should stop writing Dockerfiles today — Do this instead](https://medium.com/kpmg-uk-engineering/you-should-stop-writing-dockerfiles-today-do-this-instead-3cd8a44cb8b0)

使用[**docker init**](https://docs.docker.com/engine/reference/commandline/init/)来初始化Dockerfile, Compose File等。目前已经支持*Go, Python, Java, Node.js, Rust, ASP.NET以及PHP*

使用标准的化的模板，可以遵循最佳实践，避免出现安全问题、性能问题等。

## 3.Tip

[Tailwind CSS](https://tailwindcss.com/)

CSS框架，快速、实时的生产CSS文件

## 4.Share

### 人生之败，非傲即惰。然，勤则百弊皆除

勤分六种

身勤，路虽远，行则必至；事虽难，做则必成

眼勤，遇一人，必详细观察；看一文，必反复审阅

手勤，易丟之物，随手拾之；易忘之事，随笔记之

口勤，他人之常，多夸多赞；自己之短，多学多问

心勤，精诚所至，金石为开；若思所至，诸事皆通

脑勤，谋定而后动，知止而有得；万事皆有法，道正事则通

勤能补拙，全勤才是真正的勤

### 曾国藩的 “六戒五勤”

> https://haoleeson.github.io/2017/11/12/GuofanZeng-six-rings/

### 六戒

- 第一戒：久利之事勿为，众争之地勿往
- 第二戒：勿以小恶弃人大美，勿以小怨忘人大恩
- 第三戒：说人之短乃护己之短，夸己之长乃忌人之长
- 第四戒：利可共而不可独，谋可寡而不可众
- 第五戒：天下古今之庸人，皆以一惰字致败；天下古今之才人，皆以一傲字致败
- 第六戒：凡办大事，以识为主，以才为辅；凡成大事，人谋居半，天意居半

### 五勤

- 一曰身勤：险远之路，身往验之；艰苦之境，身亲尝之。
- 二曰眼勤：遇一人，必详细察看；接一文，必反复审阅。
- 三曰手勤：易弃之物，随手收拾；易忘之事，随笔记载。
- 四曰口勤：待同僚，则互相规劝；待下属，则再三训导。
- 五曰心勤：精诚所至，金石亦开；苦思所积，鬼神迹通。
