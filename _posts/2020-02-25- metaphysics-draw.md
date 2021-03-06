---
layout: post
title: 并不【玄学】的抽卡
date:   2020-02-25
categories: 数值
tag: 设计
---

* content
{:toc}


序章			
====================================
抽卡自然是一个随机事件，但是如果将一切都丢给概率，将玩家丢给运气，这种做法会导致玩家的付费体验不好，那么，我们就需要加入一些额外的功能来完善抽卡系统。  

# 纯随机抽卡模式  
首先是最基础的纯随机抽卡模式，比如说我们一个抽卡池中有2种S级卡，4种A级卡，10种B级卡。我们对所有卡的抽取概率作一个分配：  
>S1=1%  
>S2=1%  
>A1=2%  
>A2=2%  
>A3=2%  
>A4=2%  
>B1=9%  
>......  
>B10=9%  
  
这样，我们得到了一个基础的抽卡概率池。  
但是在这里，我个人比较建议将概率池改为权重池使用，因为这样我们不需要保证所有值加起来等于100，只需要保证每个值的概率符合设计即可。而且在后续添加新的元素进入卡池会更为方便。那么，权重值的设定方式就是：  
>S1=1  
>S2=1  
>A1=2  
>A2=2  
>A3=2  
>A4=2  
>B1=9  
>......  
>B10=9  
  
这样，我们得出的级别卡组分配概率就是：  
>S卡=2%  
>A卡=8%  
>B卡=90%  
  
权重值的配置方式，新增一个新卡进入自然更为方便，但是，加入一个新卡不改变其他卡的权重时，会导致所有卡的中奖概率改变。这是一个新的问题。  
如果我们希望新增一个B卡，但是不对抽到S、A、B级别卡的概率不造成影响的话怎么样设计最为方便后续拓展。  
这样，我们可以设计一个双层权重值的抽卡方式：  
第一层是级别卡组的权重分配：  
>S卡=2   
>A卡=8  
>B卡=90  
  
然后，在每个级别的卡组内再进行权重分配，比如S卡：  
>S1=1  
>S2=1  
  
那么这个时候我们要新增一个S3卡：  
>S1=1  
>S2=1  
>S3=1  
  
这样简单的增加一项在S卡组权重中，便不会影响其他级别卡组的抽取概率，当然，如果希望新卡的抽取概率要高一些也可以直接调整其权重值。  
这种双层权重配置的方式会在后续拓展维护中比较方便，查证数据的时候也会更为清晰。  
  
# 保底机制  
还是以上面所列举的抽卡池模拟，2%的几率出S级卡，但是在实际模拟中，每个玩家进行50次抽卡，依然有36.4%的玩家是没有抽到S卡的。这是纯随机没有办法避免的一个问题，有人运气爆表一发入魂，自然也有脸黑的没法，一直不出货。  
那么，为了避免这一些玩家在消耗了大量的金钱或者时间后，都一直无法抽取到稀有卡的情况，或者说更重要的是为了避免这些脸黑的玩家在经历这种极差的体验后放弃游戏而流失，我们需要加入一个脸黑玩家的保护机制。  
这个保护机制最常见的做法就是`保底机制`，这种机制可以在明面上告知玩家，也可以做在暗处。比如我们2%出S卡，但是额外加入一个条件，玩家连续49次抽取中没有出现S卡，那么在第50次抽取时必出S卡。当然这个次数可以自由设定，而这个连续多少次没有抽取到S卡的计数器则积累在玩家身上，一旦玩家抽取到了S级卡便立马将计数器清零。  
当然也有其他类似的做法。比如由保底机制衍生一下：我们每次未抽取到S卡，都会累计一个计数器，这个计数器不仅仅是达到了某个数字后让玩家下一次必出S卡，而增加了一个额外的功能，这个计数器越大，玩家抽取S卡的概率就越高。也就是玩家连续未抽中S卡的次数越多，那么他抽取S卡的概率就越高。  
如果加入了保底机制，不论是哪一种，自然会对最终的玩家抽取S卡所需次数的期望造成影响，如果我们还希望这个期望值和之前纯随机时保持一致，那么就需要调整抽卡的权重分配。  
  
# 额外的条件  
有些游戏中会有很多免费获取的充值货币，而这种货币可用于抽卡。或者说直接能从日常活动中免费获取抽卡次数。那么我们是否是希望这部分免费获取抽卡机会的玩家和充值获取抽卡机会的玩家所感受的抽卡体验是一致的呢？  
当然，我们设计两套抽卡权重配置，针对免费抽卡和付费抽卡做出区分，这自然是最简单的做法。付费的抽卡体验更好，抽出极品的概率更大，这种做法自然可以。但如果如果我们不希望出现如此大的差异，比如我们严格控制了这种充值货币的产出。我们喜欢两者间有一定的差异，但是体验差异并不大应该怎么设计呢？  
就拿上面的保底机制来说，我们可以在保底计数器上做些小小的文章，比如说我们免费和付费抽卡概率一致，全是2%的看运气。然后每次没抽中都累积1点计数器，当计数器到50时触发保底机制。但是我希望付费抽卡玩家的体验还要更好一些。那么可以让付费抽卡时，未抽中S卡所给计数器累积的点数为2。也就是说，如果这个玩家全是免费抽卡，那么保底机制对他来说是50次内必出一次。而对于全程充值抽卡的玩家来说，这个体验要好的多，每25次内就必出一次。所有玩家通用一套保底设计，只是免费和付费抽卡的过程累积计数器的速度不同。  
  
# 首抽  
目前很多游戏都会在玩家的新手阶段赠送一些抽卡次数，如果这些抽卡次数给予玩家的是一堆垃圾，一些运气好的玩家抽到了S卡，那么玩家在新手阶段的体验会相差巨大。肯定会不可避免的导致大量玩家在首抽一堆垃圾后弃坑。  
还记得我之前提到的`锚定理论`吗。如果首抽的设计做的足够好，就能给玩家一种我能抽到好东西的感觉，才能促使玩家对抽卡产生比较强烈的期待。  
那么这样的话，我们可以给每个玩家的首轮抽取做一个额外的抽卡设计。比如说我们游戏在新手阶段中会赠送玩家10次抽卡机会。那么就设计前10次抽卡必出一个S卡。而后的抽卡则按照正常的权重组进行。这个首抽给予玩家的就是一个我能轻松抽到S卡的“锚”。但是，这个设计的同时会带来一个问题，就是会有大量的玩家，或者卖新号的工作室，不停的注册账号拿首抽，就赌这首抽给的S卡出极品。因为所有的卡牌游戏中，即使是最高等级的S卡，也是有强弱之分的，也是有一般的S卡和极其稀有很难抽到的极品S卡。那么为了避免玩家“白嫖”我们的拿来创造营收的极品S卡，做法很简单，在首抽卡池中不加入极品卡，只加入我们希望玩家免费获得的一些S卡。  
  
# 营造玄学的体验  
抽卡这种看运气的概率问题，玄学可以说是经久不衰。但是有些游戏抽卡系统可以引起广泛的讨论，而有些游戏则不然。那么是为什么？  
在我看来，这是抽卡系统的沉浸感所致。一个好的抽卡系统是能营造这种氛围，引导玩家去往玄学抽卡的方向走，增强抽卡的代入感。  
那么怎么样才算是好的能让玩家有代入感的抽卡系统呢？  
首先：**卡池的内容足够丰富，稀有物品掉落率足够的低**  
其次：**玩家有自己操作的空间**  
如果卡池概率不是那么的低，大量玩家可以轻易抽到稀有物品的话，那么还会有多少玩家去研究怎么样才能抽取到所想要的稀有物品呢？概率足够低才会有`幸存者偏差`发挥的空间。  
而自己操作的空间自然不是简单的点击一下抽卡，或者十连抽这种操作。我们来看一下知名玄学（阴阳师）的抽卡系统是怎么样的。  
阴阳师的抽卡，是需要玩家在抽卡符上画画之后，才会进行抽卡展示结果。而这个画的过程就是阴阳师抽卡系统的灵魂所在。画的什么完全是玩家自由发挥，画的什么和结果有必然联系么？不管真的有没有，只要玩家认为有，那么就有了玄学。  
所以，在设计抽卡系统的时候，就需要给玩家玄学的机会，一个简单的点击后展示结果自然是没法玄学的。哪怕像炉石传说的开包系统都有玄学的空间，用怎样的轨迹将卡包拖到中间，使用什么卡背来进行开包，开包出现5张卡后，按照怎样的顺序来翻开这些卡牌。如果炉石的开包系统是简单的点一下，就展示5张卡牌结果还能营造这些玄学话题么？抽卡本身是个很单纯的玩法，它的气质、氛围、存在感全靠花式，而花式与游戏环境越契合，用户沉浸感越高，越愿意传播玄学。