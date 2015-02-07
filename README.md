var win = Ti.UI.createWindow({
	backgroundColor:'#ffffff',
	layout:'vertical'
});
var timeView = Ti.UI.createView({
	top:0,
	width:'100%',
	height:'50%',
	backgroundColor:'#1C1C1C'
});
var label = Ti.UI.createLabel({
	color:'#404040',
	text:'00:00:00.0',
	height:Ti.UI.SIZE,
	textAlign:'center',
	verticalAlign:Ti.UI.TEXT_VERTICAL_ALIGNMENT_CENTER,
	font:{
		fontSize:'30sp',
		fontWeight:'bold',
	}
});
timeView.add(label);
win.add(timeView);

var buttonsView = Ti.UI.createView({
	width:'100%',
	height:'15%',
	layout:'horizontal'
});
var buttonStartLap = Ti.UI.createButton({
	title:'GO!',
	color:'#COBFBF',
	width:'50%',
	height:Ti.UI.FILL,
	backgroundColor:'#727F7F',
	font:{
		fontSize:'25sp',
		fontWeight:'bold'
	}
});

buttonsView.add(buttonStartLap);

var buttonStopReset = Ti.UI.createButton({
	title:'Stop',
	color:'#COBFBE',
	width:'50%',
	height:Ti.UI.FILL,
	backgroundColor:'#404040',
	font:{
		fontSize:'25sp',
		fontWeight:'bold'
	}
});
buttonsView.add(buttonStopReset);
win.add(buttonsView);
ButtonStartLap.addEventListener('click',function(e) {
	stopWatch.start();
}
buttonStopReset.addEventListener('click',function (e) {
	stopWatch.stop();
	label.text = 'Ready?';

Stopwatch = function(listener,resolution){
	this.starTime = 0;
	this.startTime = 0;
	this.totalElapsed = 0;
	this.started = false;
	this.listener = (listener !=undefined ? listener : null);
	this.tickResolution = (resolution != undefined ? resolution : 500);
	this.tickInterval = null;
	this.onehour = 1000 * 60 * 60;
	this.onemin = 1000 * 60;
	this.onesec = 1000;
};
Stopwatch.prototype.start = function() {
	var delegate = function(that, method) { return function() { return method.call(that); }; };
	if (!this.started) {
		this.startTime = new Date().getTime();
		this.stopTime = 0;
		this.started = true;
		this.tickInterval = setInterval(delegate(this, this.onTick),
		this.tickResolution);
	}
	};
	Stopwatch.prototype.stop = function() {
		if (this.started) {
			this.stopTime = new Date().getTime();
			this.started = false;
			var elapsed = this.stopTime - this.startTime;
			this.totalElapsed += elapsed;
			if (this.tickInterval != null)
			clearInterval(this.tickInterval);
	}
	return this.getElapsed();
	};
	Stopwatch.prototype.reset = function() {
	this.totalElapsed = 0;
	this.startTime = new Date().getTime();
	this.stopTime = this.startTime;
	};
	Stopwatch.prototype.restart = function() {
		this.stop();
		this.reset();
		this.start();
	};

win.open();

