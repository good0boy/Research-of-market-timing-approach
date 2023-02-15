## 市场择时方法研究（这里只提供我自己用的最多的两种择时方法）<br>

### 阻力支撑相对强度（RSRS）<br>

阻力支撑相对强度(Resistance Support Relative Strength, RSRS)是另一种阻力位与支撑位的运用方式，它不再把阻力位与支撑位当做一个定值，而是看做一个变量，反应了交易者对目前市场状态顶底的一种预期判断。<br>
每日最高价和最低价是一种阻力位与支撑位，它是当日全体市场参与者的交易行为所认可的阻力与支撑。一个很自然的想法是建立最高价和最低价的线性回归，并计算出斜率。即：<br>
high=α+β⋅low+ϵ,ϵ∼N(0,σ2)<br>
当斜率值很大时，支撑强度大于阻力强度。在牛市中阻力渐小，上方上涨空间大；在熊市中支撑渐强，下跌势头欲止。<br>
当斜率值很小时，阻力强度大于支撑强度。在牛市中阻力渐强，上涨势头渐止；在熊市中支撑渐送，下方下跌空间渐大。<br>

第一种方法是直接将斜率作为指标值。当日RSRS斜率指标择时策略如下：<br>
1、取前N日最高价与最低价序列。（N = 18）<br>
2、将两个序列进行OLS线性回归。<br>
3、将拟合后的β值作为当日RSRS斜率指标值。<br>
4、当RSRS斜率大于S<sub>buy</sub>时，全仓买入，小于S<sub>sell</sub> 时，卖出平仓。（S<sub>buy</sub>=1,S<sub>sell</sub>= 0.8）<br>

第二种方法是在斜率基础上进行标准化，取标准分作为指标值。RSRS斜率标准分指标择时策略如下：<br>
1、取前M日的RSRS斜率时间序列。（M = 600）<br>
2、计算当日RSRS斜率的标准分RSRS<sub>std</sub>：

RSRS<sub>std</sub> =(RSRS−μ)/σ <br>

其中μ为前M日的斜率均值，σ为前M日的标准差。<br>
3、若RSRS<sub>std</sub>大于S<sub>buy</sub>，则全仓买入；若RSRS<sub>std</sub>小于S<sub>sell</sub>，则卖出平仓。（S<sub>buy</sub>=0.7,S<sub>sell</sub>=−0.7）<br>

### 大盘均线择时<br>
大盘择时主要以指数（上证、沪深300等）的开盘价（open）、现价（now）、5日均线值（ma5_today）来对比分类,具体逻辑如下：<br>
1、now>open: **buy**<br>
2、now<=open &  now、open>ma(5)_today: **buy**<br>
3、now、open<ma(5)_today: **sell**<br>
3、else：**keep**<br>
