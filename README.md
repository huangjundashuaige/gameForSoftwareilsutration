![这里写图片描述](http://img.blog.csdn.net/20171010155626034?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaHVhbmdqdW5kYXNodWFpZ2U=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
<h1> 海绵宝宝大战痞老板 </h1>
<h2> 用consruct2制作射击游戏</h2>
<p>导引</p>
<ol>
<li>利用consruct2基础组件构建射击游戏的基础部分</li>
<li>利用现有基础构件组合出复杂新颖的游戏特性</li>
<li>对这次项目作出总结</li>

<p>首先这个游戏很明显可以看出是受到了construct2 的tutarial里的example的启发这个我当然承认没什么好说的。但是如果你真的尝试过用这个软件制作游戏就会发现虽然看似这个软件很弱智很易上手，但是这既是优点也是缺点，优点就在于可以很好得满足目标用户群体--也就是学习能力不是特别强的小学生，力图实现能够激发他们想象力，能够将他们对于制作游戏的幻想得以实现，<s><strong>甚至达到诱惑这些小学生走向成为码农的不归路</strong></s>
<hr/>
<p>但是这个软件这么作不好的地方就在于极大程度地限制了那些有一定编程基础但是鸡贼吧懒不想学js,unity的这种人比如说我。就会发现其实将一些看似全面的基础游戏模块封装好给你让你用这些做一个游戏，其实就隐含了这个construct2作者自己对于做游戏的理解，换句话说不管你怎么用这个软件做游戏，你能做出来的东西都只能在这个大框架里面</p>
<hr/>
<p>anyway enoungh for my talkshit.Lets get back to what ive done</p>
<hr/>
##游戏策划
突然有章鱼哥被辐射感染过的蜘蛛咬到了，它发现自己突然有了可以无性繁殖的超能力，但是这样下去海底的资源都会被它消耗殆尽，为了防止世界被破坏，勇敢的海绵宝宝站了出来，它消灭了一个又一个复制体，但是就在这时，被伽马射线照射到的痞老板突然出现.......
##游戏设计
<p>关于如何实现射击游戏可以点击这个网站去tutorial找第一个教程[这是construct的射击游戏模板教程](http://www.scirra.com/construct2 "construct2")在这里我想说的只有不同于这个模板的新元素
<ol>
<li>关于如何捡拾道具和装备</li>
<li>关于如何改变角色形象和属性以及可执行操作，具体而言就是怎么让角色变身进化升级</li>
<li>关于如何确定游戏进程并在此基础上做出boss出现和restart判定</li>

</ol>
先摆出游戏的crc卡片吧
object name | spongebob
---- | ---
Attribute | 图片、位置、方向、速度、生命值
Collaborator | Event&Action
bulletA| 发射
bulletB|正面攻击
squarBro|碰撞减血
BossPi|碰撞减血
小蜗|进化变成超级海绵宝宝

<br>
object name |chaoji海绵宝宝
---- | ---
Attribute | 图片、位置、方向、速度、生命值
Collaborator | Event&Action
bulletA| 强化发射
bulletB|强化正面攻击
squarBro|碰撞减血
BossPi|碰撞减血
<br>
object name |章鱼哥
---- | ---
Attribute | 图片、位置、方向、速度、生命值、随机移动
Collaborator | Event&Action
spongebob| 攻击扣血
supremSpongeBob|攻击扣血
<br>
object name |痞老板
---- | ---
Attribute | 图片、位置、方向、速度、生命值、随机移动
Collaborator | Event&Action
spongebob| 攻击扣血
supremSpongeBob|攻击扣血
<p><strong>1.</strong>首先就是先添加事件还是从判定怪物撞击这一点出发，只不过把怪物换成道具然后再对想增加的属性设置全局变量来实现。</p>![1](http://img.blog.csdn.net/20171010214304183?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaHVhbmdqdW5kYXNodWFpZ2U=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
<p><strong>2.</strong>其次就是升级变身
![2](http://img.blog.csdn.net/20171010214550896?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaHVhbmdqdW5kYXNodWFpZ2U=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)这是最重要的一步，就是添加这个游戏最初事件先将后面将随游戏进程出现的角色隐藏起来，并且先存一个档方面之后restart独挡没必要再刷新一次。![3](http://img.blog.csdn.net/20171010215501871?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaHVhbmdqdW5kYXNodWFpZ2U=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
这里是变身的实现过程，这个创意非常的酷炫我觉得，海绵宝宝骑上了小蜗之后就像悟空和贝吉塔一样使用了合体绝招，变身成了终极无敌海绵宝宝骑士。为了能够在位置上无缝衔接进化前的小海绵宝宝我尝试了直接用原先的角色spawn新的角色出来。</p>![four](http://img.blog.csdn.net/20171010220024783?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaHVhbmdqdW5kYXNodWFpZ2U=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
这里在做出攻击的时候也需要同时考虑变身前后的两个角色
![5](http://img.blog.csdn.net/20171010220119210?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaHVhbmdqdW5kYXNodWFpZ2U=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
<p><strong>3.</strong>接下来就是游戏进程的判定了，首先需要知道construct2这个软件编译代码的逻辑由是无结束判定for loop里面一堆的if 语句（也就是event）构成的，而且对于每一次single循环（也就是every tick）的所花费时间也做了限定是1/60seconds这样来达到每秒60帧的效果，所以在全局变量里面设置一个time并且every tick里面都让time++就可以达到记录时间的效果，再在之后的if语句中对时间进行判断来得到定时召唤boss的效果。</p>![6](http://img.blog.csdn.net/20171010220842624?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaHVhbmdqdW5kYXNodWFpZ2U=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)    还有文本框的实时改变也在every tick里面设置![7](http://img.blog.csdn.net/20171010220919926?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaHVhbmdqdW5kYXNodWFpZ2U=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
<hr/>
以上便是全部的游戏制作的内容了
![8](http://img.blog.csdn.net/20171010221252544?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaHVhbmdqdW5kYXNodWFpZ2U=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
看到表情这么欠的痞老板是不是有冲上去打一顿的冲动
[这是游戏链接快来试试吧](https://huangjundashuaige.github.io/gameForSoftwareilsutration/game/index.html)
还有要补充的一点是因为js安全问题好像不能直接输出index.html来玩还需要上传到云端然后在线玩所以大家还是得需要在construct2里面编译才能玩

<strong>谢谢大家观看欢迎评论交流</strong>
