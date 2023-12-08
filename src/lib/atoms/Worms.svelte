<script>
  import { onMount, onDestroy } from 'svelte';

//*** SHIM ***
onMount(() => {
window.requestAnimFrame = (function() {
  return window.requestAnimationFrame ||
    window.webkitRequestAnimationFrame ||
    window.mozRequestAnimationFrame ||
    window.oRequestAnimationFrame ||
    window.msRequestAnimationFrame ||
    function(callback) {
      window.setTimeout(callback, 1000 / 60);
    };
})();

(function() {
	"use strict";
	
	//*** VARIABLES ***
	var _stageContext, _stageWidth, _stageHeight;
	var _wormArray = [];
	var _wormCount = 50;
	var cursorX, cursorY; // Added cursor position variables
	
	//*** INIT ***
	function init() {
		var stage = document.getElementById('stage');
		var margin = 30;
		var i = 0;
		var worm;
		_stageWidth = stage.width = window.innerWidth;
		_stageHeight = stage.height = window.innerHeight;
		_stageContext = stage.getContext('2d');
		
		for(i=0;i<_wormCount;i++) {
			worm = new Worm({top:margin,bottom:_stageHeight - margin, left:margin, right:_stageWidth - margin});	
			_wormArray.push(worm);
		}
	}
	
	//*** METHODS ***
	function clearStage() {
		_stageContext.clearRect(0,0,_stageWidth,_stageHeight);
	}
	
	function drawStage() {
		var i = 0;
		var worm;
		for(i=0;i<_wormCount;i++) {
			worm = _wormArray[i];
			worm.move(cursorX, cursorY); // Pass cursor position to the move method
			worm.draw();
		}
		
	}
	
	function onEnterFrame() {
		clearStage();
		drawStage();
		window.requestAnimFrame(function() {
			onEnterFrame();
		}, 60);
	}
	
	//*** CLASSES ***
	
	var Worm = function(options) {
		this.left = options.left;
		this.right = options.right;
		this.bottom = options.bottom;
		this.top = options.top;
		this.width = this.height = 2;
		this.color = '#FFFFFF';
		this.x = _stageWidth/2;
		this.y = _stageHeight/2;
		//speed vars
		this.xSpeed = this.ySpeed = 0;
		this.xDelta = this.yDelta = 0;
		this.xMax = 5;
		this.yMax = 3;
		this.totalSegments = Math.floor(Math.random() * 12) + 8;
		this.segmentArray = [];
		this.avoidanceDistance = 300; // Increased avoidance distance
		this.initialize();
	}

	Worm.prototype.initialize = function() {
		var i = 0;
		var holdPos;
		_stageContext.strokeStyle = '#ffd2d2';
		_stageContext.lineCap = 'round';
    
		for(i = 0;i<this.totalSegments;i++) {
			holdPos= {};
			holdPos.x = this.x; 
			holdPos.y = this.y;
			this.segmentArray.push(holdPos);
		}
	}
	
	Worm.prototype.moveSegments = function() {
		var i = 0;
		var holdObj;
		for(i=0;i<this.totalSegments;i++){
			holdObj = this.segmentArray[i];
			TweenMax.to(holdObj, (i*.15) + .15, {x:this.x, y:this.y, ease:Strong.easeOut});
		}
	}
	
	Worm.prototype.draw = function (x,y){
		var i = 0;	
		var holdObj;
		_stageContext.beginPath();
		_stageContext.moveTo(this.x,this.y);
		for(i=0;i<this.totalSegments;i++){
			holdObj = this.segmentArray[i];
			_stageContext.lineWidth = this.totalSegments - i;
			_stageContext.lineTo(holdObj.x, holdObj.y);
			_stageContext.stroke();
		}
		
	}
		
	Worm.prototype.move = function(cursorX, cursorY) {
		// Calculate the direction away from the cursor
		var directionX = this.x - cursorX;
		var directionY = this.y - cursorY;
		var distance = Math.sqrt(directionX * directionX + directionY * directionY);

		if (distance < this.avoidanceDistance) {
			// Normalize the direction vector
			var normalizedDirectionX = directionX / distance;
			var normalizedDirectionY = directionY / distance;

			// Move away from the cursor
			this.x += normalizedDirectionX * this.xMax;
			this.y += normalizedDirectionY * this.yMax;
		} else {
			// Move randomly within bounds
			this.xDelta = -1 + (Math.random() * 2);
			this.yDelta = -1 + (Math.random() * 2);
			this.xSpeed += this.xDelta;
			this.ySpeed += this.yDelta;

			if (this.xSpeed > this.xMax) {
				this.xSpeed = this.xMax;
			} else if (this.xSpeed < -this.xMax) {
				this.xSpeed = -this.xMax;
			}

			if (this.ySpeed > this.yMax) {
				this.ySpeed = this.yMax;
			} else if (this.ySpeed < -this.yMax) {
				this.ySpeed = -this.yMax;
			}

			this.x += this.xSpeed;
			this.y += this.ySpeed;
		}

		this.moveSegments();
	}
	
	init();

	document.addEventListener('mousemove', function(event) {
		cursorX = event.clientX;
		cursorY = event.clientY;
	});

	onEnterFrame();
})();
});

</script>

<canvas id='stage'></canvas>

<style>

    canvas {
    background-color: transparent;
    width: 100vw;
    height: 30rem;
    z-index: 2;
    position: absolute;
    margin-top: 39rem;
}

@media screen and (min-width: 720px) {

canvas {
margin-top: 5rem;
}

}

</style>