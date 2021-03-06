# -echarts-mapv-
基于echarts与mapv的可视化航行辅助系统
基于echarts与mapv的可视化航行辅助系统

做的过程中需参考一定的文献，如《南海舰船数据可视化分析系统设计与实现》，一定要重点关注北京大学 袁晓如教授的课题组，他们目前在交通轨迹数据可视化这块应该是全国做的做好的，你们可以模仿！
然后你们作品其中的一个亮点是，你们有明确的行业背景和应用价值，所以不管做什么，落脚点一定要是 海事安全，所有可视化的结果是为 海事安全 服务的，否则的话，做这个工作就意义不大。海事安全可以是面向海事监管部门，也可以是船东，或者正在航行中的船舶本身。

项目名称：基于echarts与mapv的可视化航行辅助系统
分组：信息可视化（大类）——数据可视化（小类）

该分组的要求：数据可视化是指基于编程工具/开源软件（如Python，JavaScript， Processing，E-chart，D3.js等）或数据分析工具（如Matlab，Tableau等）等实 现的数据可视化。

我们使用的开源库：echarts和mapv

研究内容主要如下：

基础功能模块：
1）鼠标缩放、卫星／普通地图切换、鹰眼、比例尺（论文中直接copy的，你们好好思考下）
2）直接统计该片水域的船舶数量，船舶航速的统计分布，船长的统计分布，船宽的统计分析等。


时间轴功能模块：
可以设置一个时间段，然后在这个时间段内，船舶沿着船舶轨迹（也就是AIS数据）进行动态展示，这里还可以包括航向，然后船舶后面可以加一点点虚影（如果有难度就算了，），虚影越亮表示船舶速度越高；如果虚影不好做，直接给动态航行的船舶一个颜色，颜色越亮表示船舶速度越高，颜色越浅，表示船舶速度越低。

搜索功能模块：
这里你们可以自己思考，我提示一点：由于船舶轨迹数据的标识码是用MMSI（类似于我们的身份证）进行标记的，只要输入MMSI（或者在不知道MMSI的情况下用鼠标点击哪条轨迹，对应轨迹的信息就显示出来），显示出来的信息包括，静态信息（比如船长船宽之类的），然后直接显示出对应船舶轨迹的三维轨迹可视化信息（后面模块有介绍，相当于是相互对照关系）。

热力图模块（热力图反映了船舶密度，船舶密度大的地方很显然船舶碰撞风险高，这对于海事监管非常有意义）：
如果实现热力图其实是有很多开源模块的，这里我们要做的是时空热力图，难度也不大。因为在同一片水域，不同局部区域在不同时间内所对应的船舶密度也是不同的，所以这里需要做一个动态的热力图，我们可以将一天24小时划分成24个时间段，比如：0:00-0:59；1:00-1:59.。。。。23:00-23:59，这样动态展示很酷了！如果数据足够，可以展示完第一天，紧接着展示第二天；如果数据不够，可以将第一天和第二天（或其他天）的数据进行叠加，然后只画24个可视化的图即可。
 
这是一个很简单的静态的，我们需要一个动态的。

轨迹可视化模块（便于对船舶轨迹进行异常行为分析，因为轨迹上有速度信息）：
 
这是一个三维轨迹可视化案例，下面是底图，轨迹的颜色显示的是船舶的航行速度，箭头表示方向；
 
船舶轨迹进行聚类后，可直接对属于不同类别的轨迹进行可视化，这里的可视化不用那么复杂，只用不同颜色表达即可，这样可以反映在这片水域内，船舶航行的不同趋势，对于海事监管非常有意义。你还可以在聚类基础上，对属于不同类别轨迹的船舶速度进行可视化（这里用热力图即可，后续我们调整这里的内容），船舶速度直接计算平均速度即可，首先对水域进行网格划分，然后对船舶轨迹进行插值，每个网格在一段时间内会有多艘船舶通过，对这多艘船舶的速度进行平均即可。

轨迹计算模块：
由于你们时间很紧，如果时间足够可以来做，如果时间不够，后期再做。数据可视化在我们水上交通领域属于空白领域，希望你们能够坚持做下去，如果你们想发文章的话，后面可以指导你们发文章，这里扎扎实实做，相信可以做出好成果。如果想发文章或参加各种比赛，一定要多催我哈！这样我们可以提高效率

这块功能比较高级（这三个模块我们课题组研究生都在做，你们计算机的动手能力强有自己的优点，希望你们能够一块做下去，后面可以发属于你们自己的文章或参加比赛，但一定要多交流）：
1）	船舶轨迹预测：便于掌握未来船舶航行的态势，对于风险判断、或某片水域未来船舶的数量（可用热力图展示）非常有意义；
2）	交通风险计算：这个交通风险其实和热力图是相关的。在热力图中，密度大的地方风险高，密度低的地方风险低，当这个只是一种直观的感受，这个风险到底多大呢？就需要用near-miss等方向进行计算；由于同一片水域中不同局部区域在不同时刻对应的船舶轨迹数量是不同的，那么这个风险也是时空变化的，所以和时空热力图一样，这里的交通风险也可以用时空可视化的模式进行表达；
3）	交通风险预测：既然船舶轨迹可以预测，交通风险又和船舶轨迹有关，因此交通风险预测也是可行的。这块我们目前有很多方向，后期我们可以重点做交通风险预测及其可视化，属于世界级的课题，但其实难度不大，我们有自己好的想法就没那么难。

后面内容可暂时不管：


我们的内容主要是：
1.	为帮助要经过该水域的人了解当前水域中的船舶情况，我们利用AIS数据将船舶轨迹做成可视化的动图，便于直观了解这片水域当前的情况
2.	为帮助船舶驾驶人员提前规避风险，提供预测轨迹的功能，会将预测的轨迹显示在当前轨迹之后
3.	为帮助船员方便的了解该地区的天气情况，我们提供了天气数据的可视化，展现该地区当前以及未来几天的天气情况、出现不良天气的概率等（天气数据基本上是拿不到的，可以暂时不考虑）
4.	为帮助行业相关人员分析该水域中的航行特点以及水域中不同区域的繁忙程度，我们将过去一段时间内的轨迹数据做成热力图
5.	为帮助行业相关人员分析该水域的流量特点，我们提供了关于船舶数量的统计，可以按不同的时间跨度展示，如：将每个月内每天船舶数量的变化做成折线图；将每月通航的船舶总数做成柱状图；按船舶航行的时间段（清晨、上午、中午、下午、傍晚、深夜）划分成做成饼图



思路：
1.	历史数据的可视化：
（1）统计研究水域内的船舶交通流情况：（分析交通流演变规律）
对研究水域划定区域，统计不同时间段的船舶交通流（凌晨，上午，中午，下午，晚上），而且可以进行细化统计，分不同船型及不同尺寸分类讨论（比如船舶类型可分为：货船、渔船、油船、客船、其他类型船舶，尺寸：如果研究水域为海洋区域可分为：L<=60，60<L<=100，100<L<=120，120<L<=170，170<L<=285，L>285；如果研究水域为内河可分为：L<=60，60<L<=80，80<L<=100，100<L<=120，120<L<=140，L>140）
（2）研究水域内历史轨迹以及航速的可视化：（分析是否有异常行为船舶，以及碰撞风险分析，这部分可以参考加入王凯研究的near-miss）
在可视化过程中，加入聚类算法，目的就是将不同类的轨迹及航速进行分类显示在地图上（电子海图）
2.	未来数据可视化：
（1）对交通流的预测，预测结果进行可视化，可以对应历史数据交通的分类方式进行预测
（2）轨迹预测，这一部分可以做成实时预测的动图（这部分研究可以加我做的内容）



