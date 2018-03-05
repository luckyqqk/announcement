# announcement
announcement system and saved in redis
 ## 公告系统(公告性邮件)
 * 可用于发布通知,发放全服奖励等功能.
 * 与用户私人邮件不同,公告均为全服唯一,所有玩家共享.
 * 用户私人邮件,我会存在MySql,而公告,我会选择存redis.
 * 该公告系统仅提供公告数据的新增,获取和隐藏(没有开启,因为开启不等于新增,开启不应该给已读的用户再次发送红点,却需要给未读的用户发送红点,做此功能,得不偿失).
 * 公告的数量也不能超过31个,默认30个(没错,是一个int可支持的范围,用来做公告,也绰绰有余了).
 * 至于某个玩家对公告的可读/删除状态,应由逻辑方维护,存于该玩家的自身数据中.
 * 除此之外,逻辑方还需在用户数据中存储公告系统的版本,若版本不同,则可读/删除等状态需重置.
 * 逻辑方可获取全部公告,包括隐藏公告,在提供给用户时,需去除隐藏的公告.
 ### 数据来源:
 * GM手动增加公告.
 ### 设置隐藏:
 * GM可手动将公告隐藏,隐藏后的公告,玩家不可见(由逻辑方保证).
 ### 全部删除:
 * GM可删除所有公告,数据直接销毁.注:若要删除某一条公告,请选择使用隐藏功能.
 ### 数据销毁和版本变更:
 1. GM设置公告隐藏,当全部公告均为隐藏,则数据一并销毁,当前版本变更.(所以,隐藏操作应予以操作者提示)
 2. 全部删除或手动变更版本,数据销毁,版本变更.
 3. 自动销毁,每个版本当时间到达expireSeconds后,版本自动变更.
