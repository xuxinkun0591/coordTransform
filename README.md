平时把空间数据保存在oracle数据库, 用oracle spatial技术里的SDO_GEOMETRY字段保存点线面数据,想找个百度-高德-WGS这三种坐标相互转换的代码, 发现竟然没有ORACLE PLSQL 版本的, 大多是javascirpt和java版本的. javascript处理效率低,不适合处理大量数据的坐标转换; java读取数据源不太方便; 用plsql效率高且调用方便,于是自己动手写一个.</br>
该存储过程(包)实现oracle spatial 中 sdo_geometry类型的空间数据经纬度坐标转换, 包括百度-高德-WGS三种坐标, 输入和输出坐标系均为EPSG:4326.</br>
用法: 包coord包含多个函数, 最终用到的只有6个函数-- wgs2bd(wgs转百度)/wgs2gd(wgs转高德)/gd2bd(高德转百度),以及反过来的三个(bd2wgs/gd2wgs/bd2gd),输入变量为原sdo_geometry, 输出变量为转换后的sdo_geometry. 如高德经纬度点(119,20),对应geom=SDO_GEOMETRY(2001,4326,SDO_POINT_TYPE(119,20,NULL),NULL,NULL),需要转换为WGS坐标, 直接用包中的函数coord.gd2wgs(geom),即可得到转换后的坐标(118.9956523, 20.002079).</br>
</br>
代码示例: </br>
SELECT SDO_GEOMETRY(2001,4326,SDO_POINT_TYPE(119,20,NULL),NULL,NULL) ori_point
coord.gd2wgs(SDO_GEOMETRY(2001,4326,SDO_POINT_TYPE(119,20,NULL),NULL,NULL)) trans_point
from dual; </br>
</br>
----------OUTPUT------------  </br>
SDO_GEOMETRY(2001, 4326, MDSYS.SDO_POINT_TYPE(118.9956523, 20.002079, NULL), NULL, NULL)

</br></br>
By xuxinkun
