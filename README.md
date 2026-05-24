# NRH Dataset 2016

本数据集 NRH Dataset 2016, 是 NYCZ RideHailings Dataset 2016 的缩写，可用于训练城市交通预测的机器学习模型，比如某个小时内，某个区域的出租车上车人数和下车人数，比如使用 ST-GCN, ST-MGCN 等算法。

本数据集，是根据纽约市政府发布的 TLC Taxi 数据集 2016 整理制作的：1）清洗模糊数据；2）增加 POI 信息；3）增加天气信息；4）按区域和时间重新计算数据，更方便进入算法训练。

https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page

## 数据集官方站点

* [GitHub](https://github.com/chatopera/nrh_dataset_2016) | [Gitee](https://gitee.com/chatopera/nrh_dataset_2016)

## 购买地址

[https://store.chatopera.com/product/nrhd201605/](https://store.chatopera.com/product/nrhd201605/)

下单支付后，进入【我的证书】页面，获得数据集下载 URL。

> 关于本数据集使用授权声明，请阅读 [LICENSE](./LICENSE)

文件夹内容：语料说明，数据集语料 csv，LICENSE 使用授权声明。

```
.
├── LICENSE
├── nrh_ntas_spatial_adj_1_slim.csv
├── nrh_nta_taxi_test_nyc_2016.csv
├── nrh_nta_taxi_train_nyc_2016.csv
├── nyc_ntas_codes_20260519.csv
└── README.txt

0 directories, 6 files
```

## 数据文件

* 训练集： nrh_nta_taxi_train_nyc_2016.csv （582，461 条）

* 测试集： nrh_nta_taxi_test_nyc_2016.csv （64，726 条）

### 辅助文件

* 区域邻接矩阵： nrh_ntas_spatial_adj_1_slim.csv

* 区域信息文件： nyc_ntas_codes_20260519.csv


## 数据格式及示例

基本数据：

| key | comment |
| --- | --- |
| nta_id | 区域唯一标识，更多区域的信息，对应到文件 nyc_ntas_codes_20260519.csv，比如区域名称，区域面积（Shape_Area 平方米），区域周长（Shape_Length 米）等 |
| ev_dt_hr | 统计时间段，比如 2016-01-01 00 代表从 2016-01-01 00:00:00 ~ 2016-01-01 00:59:59 的观察时间段 |
| ev_taxi_park_type | 统计时间段内的观察事件，pickup 代表出租车上车事件，dropoff 代表出租车下车时间 |
| ev_count | 事件发生次数，比如上车或下车的次数 |
| `poi_` 开头的 |  `poi_` 开头的是该区域内的 POI 数据， poi_education(教育)，poi_healthcare（医疗），poi_natural(自然景观)，poi_office(办公楼)，poi_public_transport（公共交通），poi_shop（购物中心），poi_tourism（旅游景点） |
| `wf_` 开头的 | 天气信息，wf_rain(是否下雨)，wf_hum(湿度)，wf_fog（起雾），具体见下文（天气信息的详细介绍） | 

样例：

```
nta_id,ev_dt_hr,ev_taxi_park_type,boro_code,boro_name,ct2010,ev_count,nta_code,nta_name,poi_education,poi_healthcare,poi_natural,poi_office,poi_public_transport,poi_shop,poi_tourism,wf_conds,wf_dewpti,wf_dewptm,wf_fog,wf_hail,wf_heatindexi,wf_heatindexm,wf_hum,wf_icon,wf_precipi,wf_precipm,wf_pressurei,wf_pressurem,wf_rain,wf_snow,wf_tempi,wf_tempm,wf_thunder,wf_tornado,wf_visi,wf_vism,wf_wdird,wf_wdire,wf_wgusti,wf_wgustm,wf_windchilli,wf_windchillm,wf_wspdi,wf_wspdm
nta1,2016-12-26 22,dropoff,5,Staten Island,900,0,SI22,West New Brighton-New Brighton-St. George,4,0,8,0,6,1,1,Overcast,48.0,8.9,0,0,88.0,31.1,93,cloudy,0.0,0.0,30.14,1020.6,0,0,50.0,10.0,0,0,9.0,14.5,0,Variable,18.4,29.6,43.5,6.4,6.9,11.1
```

## 天气信息的详细介绍

* datetime: Date and time of day (EST)
* tempm: Temperature in Celcius
* tempi: Temperature in Fahrenheit
* dewptm: Dewpoint in Celcius
* dewpti: Dewpoint in Fahrenheit
* hum: Humidity %
* wspdm: Wind speed in kph
* wspdi: Wind speed in mph
* wgustm: Wind gust in kph
* wgusti: Wind gust in mph
* wdird: Wind direction in degrees
* wdire: Wind direction description
* vism: Vivibility in Km
* visi: Visibility in miles
* pressurem: Pressure in mBar
* pressurei: Pressure in inHg
* windchillm: Wind chill in Celcius
* windchilli: Wind chill in Fahrenheit
* heatindexm: Heat index Celcius
* heatindexi: Heat index Fahrenheit
* precipm: Precipitation in mm
* precipi: Precipitation in inches
* conds: Conditions: See full list of conditions
* icon
* fog: Boolean
* rain: Boolean
* snow: Boolean
* hail: Boolean
* thunder: Boolean
* tornado: Boolean

## 辅助文件

### 区域信息文件

nyc_ntas_codes_20260519.csv： 将纽约市一共划分为了 2000 个中等规模的区域（一个区域称为一个 NTA,Neighborhood Tabulation Areas[^ntadef]）, 为什么我们使用 NTA 作为划分方法？[#1](https://github.com/chatopera/nrh_dataset_2016/issues/1)。

记录更多关于区域的信息： 

```
NtaId,NtaCode,NtaName,BoroCode,BoroName,CT2010,Shape_Leng,Shape_Area,poi_education,poi_healthcare,poi_natural,poi_office,poi_public_transport,poi_shop,poi_tourism
nta1,SI22,West New Brighton-New Brighton-St. George,5,Staten Island,000900,7729.01679383,2497009.71359,4,0,8,0,6,1,1
```

* Shape_Leng： 区域的周长，单位米
* Shape_Area： 区域的面积，单位 平方千米


### 区域邻接矩阵

文件：
nrh_ntas_spatial_adj_1_slim.csv

矩阵格式：Ntas 之间的距离，单位是： 米。 行和列都是索引。一个行的索引和一个列的索引，都是 Nta Id, 是对应的两个区域，那么矩阵上的这个值，就是二者之间的中心点的直线距离。

[^ntadef]: Neighborhood Tabulation Areas (NTAs) are medium-sized statistical geographies used in New York City to report data from the Decennial Census and American Community Survey (ACS).