---
description: 需要附属mod LootTweaker
---

在阅读此页面前, 强烈建议先阅读 [LootTable : 导论](/easy/lootTable-introduction.md) 页面, 了解 LootTable 的相关原版概念.

其次, LootTweaker 和 LootTableTweaker **并不冲突, 且互相都有对方没有的功能**, 实操时推荐两者都安装, 再根据自己的实际需求选用.


# 导包
```csharp
import loottweaker.LootTweaker;
```

# 基础实例

## 移除物品
```csharp
// 通过 LootTable 注册名获取猪的 LootTable, 并将其储存到临时变量 pig中, 以供之后调用.
val pig = LootTweaker.getTable("minecraft:entities/pig");

// 通过 pool 注册名 获取猪的 LootTable 的 main 随机池.
val pigMainPool = pig.getPool("main");

// 从猪的 LootTable 的 main 随机池中移除名为 minecraft:porkchop 的 entry.
pigMainPool.removeEntry("minecraft:porkchop");

// 也可以链式调用
LootTweaker.getTable("minecraft:entities/pig")
           .getPool("main")
           .removeEntry("minecraft:porkchop");
```

## 添加物品
```csharp
// 通过 LootTable 注册名获取牛的 LootTable, 并将其储存到临时变量 cow 中, 以供之后调用.
val cow = LootTweaker.getTable("minecraft:entities/cow");

/*在牛的 LootTable 中, 添加一个名为 steve 的 pool, 并将此 pool 储存到临时变量 alex 中, 以供之后调用.
  第一个 string 为 pool 的注册名, 后四个 int 分别为最小被抽取量, 最大被抽取量, 最小额外被抽取量, 最大额外被抽取量.
*/
val alex = cow.addPool("steve", 1, 1, 0, 0);

// 向名为 steve 的 pool 中添加 entry <minecraft:apple>, 权重为 5.
alex.addItemEntry(<minecraft:apple>, 5);

// 在 addItemEntry 后再添加一个 string, 则为对应 entry 的注册名, 如不定义则 LootTweaker 会自动生成一个.
alex.addItemEntry(<minecraft:apple>, 5, "stevelikesapples");

// 也可以链式调用
LootTweaker.getTable("minecraft:entities/cow")
           .addPool("steve", 1, 1, 0, 0)
           .addItemEntry(<minecraft:apple>, 5, "stevelikesapples");
```

[战利品表修改(LootTweaker-进阶)](advanced/loottweaker-advanced.md).