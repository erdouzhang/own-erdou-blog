---
layout:     post
title:      "LayerDate插件"
subtitle:   " \" 日期插件\""
date:       2018-08-15 22:10:00
author:     "Erdou"
header-img: "img/"
catalog: true
tags:
    - 日期
---

> "staring..."

### layDate 日期与时间组件
1.官网:http://www.layui.com/doc/modules/laydate.html#ondone(API)
2.单独使用:http://www.layui.com/laydate/
layDate 是 layui 独立维护的三大组件之一,获得layDate文件包后,解压并将laydate整个文件夹（不要拆分结构）存放到你项目的任意目录,使用时只需引入laydate.js即可。
3.npm安装：npm install layui-laydate
---

### 使用(APP项目中使用)

1.html结构

<div class="top_input">
  <input style="width: 40%;" type="text" class="mui-date" id="btnStartTime" onfocus="this.blur();" placeholder="请选择开始时间">
  <span class="text_node">&nbsp;至&nbsp;</span>
  <input style="width: 40%;" type="text" class="mui-date" id="btnEndTime" onfocus="this.blur();" placeholder="请选择结束时间">
</div>

> 注意：onfocus="this.blur();" 为了防止手机端弹出输入法，使用input元素框andorid中调起输入法

2.JS结构
  a)var startTimer = laydate.render({
	elem: '#btnStartTime', //指定元素  
	type: 'datetime',
	theme: 'grid',
	format: 'yyyy-MM-dd HH时', //可任意组合 时间显示的格式
        min: waterMui.minDateCal(), // 当前时间最小时间
	max: new Date().getTime(),
	zIndex: 99999999,
	//btns: ['now', 'confirm'],
	done: function(value, date) {
		// console.log('你选择的日期是：' + value + '\n获得的对象是' + JSON.stringify(date));
		// 判断当前时间是否小于结束时间  
		var startCurrentDate = new Date(value.substr(0,value.length-1)+':00:00'); // 开始时间
		var endCurrentDom = waterMui.currentDOMObj('btnEndTime'); // 结束时间				
		if(!startCurrentDate||!value) {   // 清除按钮会回调该方法
			mui.toast('请选择开始时间');
			return;
		}				
		// 结束时间不为空
		if(endCurrentDom.value) {
			var endTimerCurrentDate = endCurrentDom.value.substr(0,endCurrentDom.value.length-1)+':00:00';
			 // 开始时间的毫秒数
			var startTimerMill = startCurrentDate.getTime();
			// 结束时间毫秒数
			var endTimerMill = new Date(endTimerCurrentDate).getTime();
			// 开始时间大于结束时间
			if(startTimerMill >= endTimerMill) {
				mui.toast('开始时间不能大于结束时间');
				return;
			}
			// 请求数据
			var s = waterMui.todayTime(startCurrentDate);
			var e = waterMui.todayTime(new Date(endTimerCurrentDate));
			historyRain(Id, s, e);
		} else {
			mui.toast("请选择结束时间");
			return;
		}
	}
});
b)var endtimer = laydate.render({
	elem: '#btnEndTime', //指定元素  
	type: 'datetime',
	theme: 'grid',
	zIndex: 99999999,
	format: 'yyyy-MM-dd HH时', //可任意组合
	max: new Date().getTime(),
	done: function(value, date) {
		var startTimeTab = waterMui.currentDOMObj('btnStartTime');
		//var startTimer = modyStrTime.replace(/-/g, '').replace(' ', '').substr(0, 10);
		var endStrTime = value.replace(/-/g, '').replace(' ', '').substr(0, 10);
		if(!endStrTime || !value) {
			mui.toast('请选择结束时间');
			return;
		}
		if(startTimeTab.value) {
			var modyStrTime = startTimeTab.value.substr(0,startTimeTab.value.length-1)+':00:00'; // 开始时间
			// 时间判断是否请求数据
			var timerStartRe = new Date(modyStrTime);
			// 获取开始时间的毫秒值
			var millTimerStart = timerStartRe.getTime();
			// 结束时间
			var timerEndRe = new Date(value.substr(0,value.length-1)+':00:00');
			// 结束时间的毫秒值
			var millTimerEnd = timerEndRe.getTime();
			if(millTimerStart >= millTimerEnd) {
				mui.toast('开始时间不能大于结束时间');
				return;
			}
			 historyRain(Id, waterMui.todayTime(timerStartRe), waterMui.todayTime(timerEndRe));
		} else {
			mui.toast('请选择开始时间');
			return;
		}
	}
});
