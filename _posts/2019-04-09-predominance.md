---
layout: post
title: 回合制中的先手优势如何平衡
date:   2019-04-09
categories: 数值
tag: 设计
---

* content
{:toc}


序章			
====================================
在所有的回合制游戏当中，先后手的优劣势必然是存在的，比如说五子棋中的先手必胜，当然也并不是所有游戏都是先手优势。在此我们以先手优势的游戏为例，寻找一下平衡先后手优劣的手段。    

# 减小先后手之间的差异  
**减少初始资源**  
以炉石传说为例，先手的手牌数比后手的少一张，并且后手会多一张可使用一次的“硬币”，可以这样改变先后手初始资源以对冲先手的优势。但是这样的缺点就是这些初始资源的差异，并不能通过量化的计算来精确获得，只能凭借感觉或者反复调试来获取。  
**获胜条件的差异**  
减少初始资源是在初始差异化，而获胜条件的不同则是在末端。比如`围棋`，使用的就是贴目的方法。后手方在计算目数时会比先手方额外获得几个。这样先手方必须占据棋盘上更多的位置才能获胜。同样的，获胜条件的差异也是无法量化计算来精确获得的。  
**增加反制玩法**  
在先手具有优势的情况下，我们增加一下后手的优势，让其平衡，让先后手都不存在谁明显更具优势。比如说dota2的比赛模式的英雄选择环节，甚至更简单的天梯选择环节：  
甲1-乙2-甲2-乙2-甲2-乙1。这样，甲方先选一人，随后就是乙方选择两人，如此就很难区分到底是哪一方占据优势，并且不仅仅是选英雄的先后顺序上具有反制玩法，同时，先选的英雄可能被后选的敌方英雄所针对克制，这也是削弱先手优势的手段。  
  
# 让游戏变得不在乎先后手  
**增加游戏的随机性**  
大家都开玩笑说炉石传说是个运气游戏，再好的运营都挡不住神抽狗的逆袭，更何况是区区先手优势，随机性并不会破坏游戏胜负的对称性，只会削减回合制游戏中最优解的选择所带来的一边倒的情况。随机性使游戏充满了变数，使后手玩家相信先手优势并不可怕，也使每局游戏玩家都有期待。当然，随机性过了，那就真的是个运气游戏和策略无关了，过分的随机性会让玩家失去自主感，让游戏的成败变为听天由命的焦虑过程。  
**增加游戏长度**  
试想一下，同样的一款回合制rpg游戏，你砍我我砍你的那种，如果双方都是两刀砍死，先后手重不重要，那如果战斗回合数拉长到100回合（真要这么长大概会被喷死），那么先后手还重要么。  
同样的，其他游戏如果大家觉得先手优势，那么我们将游戏拉长，轮流先手，同样可以忽略掉先手优势，毕竟大家都有差不多的机会占据先手，就足够公平了。  
**增加游戏深度**  
先手优势的大小自然取决于玩家能做到多少，所谓的先手优势一般是建立在完美操作的基础上，也就是假设玩家可以做出所预想的最优解，那么如果增加游戏深度，或者说，在这个游戏中，即便存在最优解，人类也无法达到完美操作的情况。比如在足球这类体育项目中，先手控球当然具备优势，可是没有人可以完美操控自己的身体，那么先手控球的优势就对胜利的天平产生不了太大的影响。更何况足球在游戏长度也做出了相应的措施：后半场会由另一方开球。同样在一些回合制RPG中，可以设计出很多后发制人的技能，玩家可以开发一套慢速阵容，以后手打先手，也是不同的游戏乐趣。  
  
# 让先手成为一个玩法  
**先手是需要投入外部资源的**  
其实这个在几乎所有的回合制RPG当中都是这样的，先手即使速度属性，绝大部分回合制RPG里，速度在玩家属性成长当中扮演很重要的一环。毕竟，先出手就可能先对对方造成减员，打的对方少进攻一次，或者先手控制对方，让对方无法反击。但是在培养速度属性上是需要投入外部资源的，部分玩家投入的多，自然获得先手的机会会大的多。但是同时速度属性相较于其他属性，在回合制游戏中是显得极其重要的，如果先手优势非常明显，那么会造成玩家过分追求速度属性，而忽略其他属性的成长，这对追求多元成长的RPG来说是不利，所以很多游戏也在这方面做出了一下相应的措施，速度自然重要，但也要有个度，不能说我们都投入了大量的资源在速度上，但是就因为你的速度比我高一点，就每次都是你先手，那么我作为一个同样投入了大量资源的人体验感会极差，这也就是梦幻西游中乱敏规则所出现来解决的问题。  
# 总结  
回合制游戏的先后手平衡有着许多种不同的思路来帮助解决，最重要的还是知道我们的目的是什么：我们是希望这个游戏是个绝对公平的博弈游戏，还是我们仅仅只是不希望先后手优势会破坏到玩家的游戏体验。其实上述的方法并不一定能抹平游戏先后手的优势影响，甚至在过度使用还会破坏玩家的游戏体验，最重要的是合理的使用来达成目的，而游戏设计最终的目的，不是做平衡而是做体验，不论是否存在先后手优势，只要玩家体验好，那么这就是个好游戏。