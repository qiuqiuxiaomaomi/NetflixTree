# NetflixTree
Netflix技术研究


<pre>
Netflix技术哪些大胆的创新

      1）大规模生产级微服务的架构实践

         Netflix大概是大规模生产级微服务做得最杰出的。
</pre>

<pre>
Netflix开发团队提出了几条设计和实现微服务架构的最佳实践：

      1）每个微服务的数据单独存储。
         不同微服务不要使用同一个后台数据存储。让开发团队选择适合每个微服务的数据库。或许,不
         同团队使用同样的数据结构来存储会减少工作量,但当其中某个团队想要更改数据结构的时候,
         其他服务不得不跟着改变。

         数据的拆分会使得数据管理异常复杂,是因为单独的存储系统不容易同步,易于出现不一致的情
         况,外键也会发生意外的改变。你需要一个后台运行的主数据管理的工具来发现和修复不一致
         的情况。比如,你需要检查每个存储订阅者ID的数据库来确保所有的ID都是同一个。这个工具可
         以自己写或者直接买。很多商用的关系型数据库都提供此类核对,它常常过于耦合,不能支持很
         好的伸缩性。

      2）使用类似程度的成熟度来维护代码
         微服务中所有代码都保持同样的类似程度的成熟度和稳定度。也就是说,你想要重写或给一个
         运行良好的已部署好的微服务添加一些代码的话,最好的方式常常是对于新的或要改动的代码,
         新建一个微服务,现有的微服务丢着不管就行。 [编辑注:这种架构常常称之为immutable 
         infrastructure principle.] 这样的话,你可以迭代式的部署和测试新代码,直至没有
         bug,性能足够好,现有的微服务不会出现故障或性能下降。一旦新的微服务和原始的服务一样
         稳定,如果确实需要进行功能合并的话,你可以将其合并在一起,或者处于性能的考虑合并它
         们。然而,就Cockcroft的经验来讲,常常是你发现你的服务太大而要进行拆分。

      3）每个微服务都单独进行编译构建
         每个微服务都单独进行编译构建,这样你就从代码库里某个版本中抽取单独的组件。这样,你可
         以拿到多个类似文件的微服务,但却是不同的版本的。这样如果要对codebase进行清理会比较
         麻烦,但对于在新建微服务时添加新文件时的便利性的话,是值得的。The asymmetry is
         intentional: 你想要引入新的微服务、文件或者功能,很容易又不会存在风险。
        
      5）部署到容器中

      6）将服务器看做是无状态的
         将那些特别是部署了客户端代码的服务器视作是可替换的一组之中的一个。这些服务器的功能
         都是一样的,你无须关心某一个。只需要关心要实现你的目标是否数量足够,你可以使用自动伸
         缩来按需调整数目。如果其中一个服务器宕机了,可以由其他一个替换。避免了那些单个服务器
         完成特殊功能的系统中存在的雪崩现象 
</pre>