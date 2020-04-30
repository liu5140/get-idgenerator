# idgenerator

这些代码是go语言生成全局id的一种方式，每次使用都会自动加载数据，需要使用直接从内存中获取即可，性能高效


具体用途：
1、生成全局主键
2、生成唯一订单号
3、可用于生成推荐码之类


如何使用：

需要在数据库中简历一张表id_space

CREATE TABLE `id_space` (
  `space_name` varchar(45) NOT NULL DEFAULT '',
  `prefix` varchar(45) NOT NULL DEFAULT '',
  `suffix` varchar(45) NOT NULL DEFAULT '',
  `seed` bigint(20) unsigned NOT NULL,
  `batch_size` bigint(11) unsigned NOT NULL,
  PRIMARY KEY (`space_name`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

---插入数据
INSERT INTO `id_space` (`space_name`,`prefix`,`suffix`,`seed`,`batch_size`) VALUES ('label','label','',8322000,1000); 
INSERT INTO `id_space` (`space_name`,`prefix`,`suffix`,`seed`,`batch_size`) VALUES ('order','order','WD0ZV6AFGSCU9MBKN24HJL578XIOP31QERTY',78436784977604,1000); 
INSERT INTO `id_space` (`space_name`,`prefix`,`suffix`,`seed`,`batch_size`) VALUES ('recommendcode','','0ZV6AWDFGSCU9HJL578X1MBKN24QERTYIOP3',78436784977604,1000); 
INSERT INTO `id_space` (`space_name`,`prefix`,`suffix`,`seed`,`batch_size`) VALUES ('user','user','',8322000,1000); 



使用：
//初始化
gen := idgenerator.Instance()

id := gen.GenerateLongID("order")//获取一个int64为的id 如 78436784984608
// 将ID转换为Code
code := gen.ChaosID(id, gen.Suffix("order"))//获取一串 如：OPRMWL8SP

id := gen.RestoreID(code, gen.Suffix("order")) //通过code 也能转换出上面对应的id 



