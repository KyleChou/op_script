功能：能够在发布前对你指定项目指定两个分支之间做对比，即为你此次发布的内容  
原理：通过gerrit api查询两个分支的最新commit id，然后交给git log来处理
解释：为什么不用gerrit api拉出分支对比结果？  
答：不是能力问题！刚开始的确是用的gerrit api直接跑出结果，在大多数场景下也的确是没有问题的。然而，后来发现当两个分支中有一个最新一条是Merge commit信息时，问题就发生了，该条Merge信息不会出现在结果中，查了下gerrit的数据库，也证实了这点，当最后一条信息是Merge信息时，gerrit会把最新的一条仅仅存在本地，以文本的形式存储，古尔抓取不到。ps:当后面再提交时，gerrit会把这条Merge存到数据库中，不是永久丢弃