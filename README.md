yii_database_read_write_splitting
=================================

yii 数据库 主从 读写分离
link www.lostphp.com

Yii框架数据库多数据库、主从、读写分离 实现

功能描述：
1.实现主从数据库读写分离 主库：写 从库(可多个)：读
2.主数据库无法连接时 可设置从数据库是否 可写
3.所有从数据库无法连接时 可设置主数据库是否 可读
4.如果从数据库连接失败 可设置N秒内不再连接


main.php配置：components 数组中

'db'=>array(
        'class'=>'application.extensions.DbConnectionMan',//扩展路径
        'connectionString' => 'mysql:host=192.168.1.128;dbname=db_xcpt',//主数据库 写
        'emulatePrepare' => true,
        'username' => 'root',
        'password' => 'root',
        'charset' => 'utf8',
        'tablePrefix' => 'xcpt_', //表前缀
        'enableSlave'=>true,//从数据库启用
  	 'urgencyWrite'=>true,//紧急情况 主数据库无法连接 启用从数据库 写功能
		  'masterRead'=>true,//紧急情况 从数据库无法连接 启用主数据库 读功能
        'slaves'=>array(//从数据库
            array(   //slave1
                'connectionString'=>'mysql:host=localhost;dbname=db_xcpt',
                'emulatePrepare' => true,
                'username'=>'root',
                'password'=>'root',
                'charset' => 'utf8',
                'tablePrefix' => 'xcpt_', //表前缀
            ),
		 array(   //slave2
                'connectionString'=>'mysql:host=localhost;dbname=db_xcpt',
                'emulatePrepare' => true,
                'username'=>'root',
                'password'=>'root',
                'charset' => 'utf8',
                'tablePrefix' => 'xcpt_', //表前缀
            ),
 
        ),
    ),
