# 通达信指标代码说明文档

## 目录
1. [背景和K线绘制](#背景和K线绘制)
2. [均线系统](#均线系统)
3. [交易信号](#交易信号)
4. [技术指标](#技术指标)
5. [买卖点判断](#买卖点判断)
6. [其他功能](#其他功能)

## 背景和K线绘制

### 背景设置
```
DRAWGBK(O>C,RGB(28,172,187),RGB(27,47,113),0,'背景图',0);
```
- 功能：设置图表背景颜色
- 参数说明：
  - O>C：当开盘价大于收盘价时（阴线）
  - RGB(28,172,187)：阳线背景色
  - RGB(27,47,113)：阴线背景色

### K线绘制
```
STICKLINE(C>=O, C, O, -1, 0),COLOR0000FF;  // 阳线
STICKLINE(C<O, C, O, -1, 0),COLOR00FF00;   // 阴线
```
- 功能：绘制基本K线图
- 颜色说明：
  - 蓝色(0000FF)：阳线
  - 绿色(00FF00)：阴线

## 均线系统

### 均线定义
```
M1:=5;   // 5日均线
M2:=10;  // 10日均线
M3:=20;  // 20日均线
M4:=60;  // 60日均线

MA1:=MA(CLOSE,M1);  // 计算5日均线
MA2:=MA(CLOSE,M2);  // 计算10日均线
MA3:=MA(CLOSE,M3);  // 计算20日均线
MA4:=MA(CLOSE,M4);  // 计算60日均线
```

### 年线
```
年线:MA(CLOSE,250)COLORWHITE,LINETHICK2;
```
- 功能：计算并绘制250日均线（年线）
- 显示：白色粗线

## 交易信号

### 涨跌停判断
```
ZTDS:=IF(CODELIKE('688'),0.2,IF(DATE>=CYBDATE AND CODELIKE('300'),0.2,0.1));
当天涨停:=REF(ROUND(INTPART(ROUND(C*100))*(1+ZTDS))/100,1);
ZT:=(C>REF(C,1)*1.08 AND H=C AND C>=当天涨停-0.05);
```
- 功能：判断股票是否涨停
- 说明：
  - 科创板(688)：20%涨跌幅
  - 创业板(300)：20%涨跌幅（注册制后）
  - 其他：10%涨跌幅

### 买入信号
```
BUYWZ:=(趋势加速XGTJ OR 弱转强XGTJ) AND NOT(H=L AND C>REF(C,1)) AND NOT(STGPGL) AND NOT(新股还) AND NOT(TSGPGL);
```
- 功能：综合买入信号判断
- 条件：
  1. 趋势加速或弱转强
  2. 非一字板
  3. 非ST股
  4. 非新股
  5. 非退市股

## 技术指标

### RSI指标
```
N1:=9;
RSI:=SMA(MAX(CLOSE-LC,0),N1,1)/SMA(ABS(CLOSE-LC),N1,1)*100;
```
- 功能：计算9日RSI
- 应用：
  - RSI>80：超买区
  - RSI<20：超卖区

### 筹码分析
```
筹码峰值均价:SSRP.SSRP,COLOR40408F,LINETHICK1,COLORYELLOW,CROSSDOT;
```
- 功能：显示筹码分布峰值

## 买卖点判断

### 乾坤猎牛
```
乾坤猎牛:=X_9X AND X_10X AND X_11X AND X_12X AND X_13X;
```
- 功能：特殊买点判断
- 条件组合：
  1. 放量
  2. 均线多头
  3. 价格突破
  4. 成交量配合

### 太极信号
```
太极:=(REF(RSI,1)<=20 AND RSI>20);
```
- 功能：RSI超卖反转信号
- 使用场景：超卖区反弹机会

## 其他功能

### 龙虎榜数据
```
游资买入:=IF(BETWEEN(GPJYVALUE(17,1,0), 0,500),GPJYVALUE(17,1,0),0);
营业部买入:=IF(GPJYVALUE(17,1,0)>=500,GPJYVALUE(17,1,0),0);
机构买入:=GPJYVALUE(9,2,0);
```
- 功能：统计不同资金的买入情况
- 分类：
  - 游资：单笔小于500万
  - 营业部：单笔大于等于500万
  - 机构：专门的机构交易

## 使用说明

1. 本指标适用于：
   - 日线级别分析
   - A股市场（主板、科创板、创业板）
   - 短线交易策略

2. 主要功能：
   - K线形态识别
   - 均线系统分析
   - 量价关系判断
   - 买卖点提示
   - 资金流向监控

3. 注意事项：
   - 指标信号仅供参考，需要结合其他因素综合判断
   - 不同市场（主板、科创板、创业板）的涨跌幅限制不同
   - 建议在实盘交易中谨慎使用，先进行回测验证 