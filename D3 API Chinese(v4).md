数组-Arrays (d3-array)
数组处理、排序、搜索等
统计-Statistics
基本统计方法
•	d3.min – 计算数组中最小值
•	d3.max – 计算数组中最大值
•	d3.extent – 计算数组中的最大值和最小值（数组范围）
•	d3.sum – 计算数组中数字总和
•	d3.mean – 计算数组的平均值（算数平均数）
•	d3.median – 计算数组中数字的中值 (the 0.5-quantile)
•	d3.quantile - 计算一个已排序的数字数组的分位数 (d3.quantile(array, n)) –––n∈(0,1)
•	d3.variance - 计算数组中数字的方差
•	d3.deviation - 计算数组中数字的标准差
测试如下：
<script>
var dataset=[2,1,3,5,7,9,3,-8,7,9,4,8,-6,5];
console.log(dataset.sort());[-6, -8, 1, 2, 3, 3, 4, 5, 5, 7, 7, 8, 9, 9]
console.log(d3.min(dataset));-8
console.log(d3.max(dataset));9
console.log(d3.extent(dataset));[-8.9]
console.log(d3.sum(dataset));49
console.log(d3.mean(dataset));3.5
console.log(d3.median(dataset));4.5
console.log(d3.quantile(dataset,0.5));4.5
console.log(d3.quantile(dataset,0.75));7
console.log(d3.variance(dataset));26.269230769230774
console.log(d3.deviation(dataset));5.125351770291554
</script>
median和quantile会自动排序数组，0.5-quantile和median输出值一致，0.75-quantile输出的值为第三个四分位值。方差和标准差与实际计算值也一致。extent会输出一个固定长度为2的数组。
查找-Search
对指定元素进行查找操作的方法。
•	d3.scan – 线性查找某一元素（默认为最小值）并返回索引
•	d3.bisect – 二分法查找排序数组中某一个值，在api文件里等同于
d3.bisectRight，时间复杂度O(logn)
exports.bisect = bisectRight;
exports.bisectRight = bisectRight;
•	d3.bisectRight - 二分法查找排序数组中某一个值（相同的值归为右边）
•	d3.bisectLeft - 二分法查找排序数组中某一个值（相同的值归为左边）
•	d3.bisector - 自定义二分查找方法，比如：d3.bisector(function(d) {return d.date;})就是定义了一个时间查找方法（基于数据类别）
•	bisector.left – 使用自定义方法（相同的值归为右边）
•	bisector.right - 使用自定义方法（相同的值归为左边）
•	d3.ascending – 判断是否升序（两个值）
•	d3.descending – 判断是否降序（两个值）
测试如下：
<script>
var dataset=[2,1,3,5,7,9,3,-8,7,9,4,8,-6,5];
console.log(d3.scan(dataset));7
console.log(d3.bisect(dataset.sort(),5));9
console.log(d3.bisectRight(dataset.sort(),5));9
console.log(d3.bisectLeft(dataset.sort(),5));7
console.log(d3.ascending(1,2));-1
console.log(d3.ascending(2,2));0
console.log(d3.descending(1,2));1
</script>
d3.bisect()和d3.bisectRight()输出完全一致，d3.ascending()和d3.descending()输出为[-1,0,1]中的一个，用来判断两个元素的大小，可以在绘制中为数据排序。
转换-Transformations
转换数组和生成新数组的方法。.
•	d3.cross – 计算两个数组的笛卡尔积(Cartesian product)
•	d3.merge – 合并多个数组为一个数组
•	d3.pairs – 创建一个具有相邻元素对(adjacent pairs)的数组
•	d3.permute - 根据索引数组来重新排序元素数组
•	d3.shuffle – 对数组进行随机排序
•	d3.ticks - 从数值区间生成数组
•	d3.tickIncrement -从数值区间生成值（增量）
•	d3.tickStep - 从数值区间生成值（步长）
•	d3.range - 生成一系列的数值
•	d3.transpose – 转置数组矩阵
•	d3.zip – 将多个数组合并，数组中相同索引位置的元素组成新数组的同索引位置元素
测试如下：
<script>
var da=[0,3]; 
var db=[5,7];
var dc=[2,4,6,8,10];
console.log(d3.cross(da,db)); [[0,5],[0,7],[3,5],[3,7]]
console.log(d3.merge([da,db,dc]));[0,3,5,7,2,4,6,8,10]
console.log(d3.pairs(dc));[[2,4],[4,6],[6,8],[8,10]]
console.log(d3.permute(dc,[2,3,1,0,4]));[6,8,4,2,10]
console.log(d3.shuffle(dc));[2,8,6,10,4](每次生成都不同)
console.log(d3.ticks(1,50,5));[10,20,30,40,50]
console.log(d3.tickIncrement(1,50,10));5
console.log(d3.tickStep(1,50,10));5
console.log(d3.range(5));[0,1,2,3,4]
console.log(d3.transpose([da,db]));[[0,5],[3,7]]
console.log(d3.zip(da,db,[5,9],[6,5]));[[0,5,5,6],[3,7,9,5]]
</script>
Transformations中部分api较常用，例如merge、zip等。具体函数过程请参看d3.v4.js。
直方图-Histograms
Bin discrete samples into continuous, non-overlapping intervals.
•	d3.histogram – 构建一个直方图布局（表示离散的数据分布）
•	histogram - 为给定的样本数组计算直方图
•	histogram.value – 设置值访问器(value accessor)
•	histogram.domain – 设置值域范围
•	histogram.thresholds – 制定划分块(bins)的方式
•	d3.thresholdFreedmanDiaconis - Freedman–Diaconis规则
•	d3.thresholdScott - Scott规则
•	d3.thresholdSturges – Sturges规则
这个链接是一个不定义规则的直方图实例和一个定义了规则的直方图实例，http://blog.csdn.net/u014711869/article/details/77371550使用了上述部分函数。
