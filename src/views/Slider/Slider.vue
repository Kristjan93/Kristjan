<template>
  <div class="the-content-housing">
    <h2 class="the-title">
      <span class="the-cool-thing">(</span>
      Slider
      <span class="the-cool-thing">)</span>
    </h2>

    <div class="slider-container"
			@mouseover="mouseOverGeneral"
			@mouseleave="mouseLeaveGeneral"
		>
			<div 
				@mouseover="mouseOverLeft"
				@mouseleave="mouseLeaveLeft"
				class="move move-left">
			</div>
			<div
				@mouseover="mouseOverRight"
				@mouseleave="mouseLeaveRight"
				class="move move-right">
			</div>
      <div 
				class="slider"
				:style="`width: ${totalWidth}px`"
			>
        <div class="slide slide1"></div>
        <div class="slide slide2"></div>
        <div class="slide slide3"></div>
        <div class="slide slide4"></div>
        <div class="slide slide5"></div>
        <div class="slide slide6"></div>
        <div class="slide slide7"></div>
        <div class="slide slide8"></div>
        <div class="slide slide9"></div>
        <div class="slide slide10"></div>
        <div class="slide slide11"></div>
        <div class="slide slide12"></div>
        <div class="slide slide13"></div>
        <div class="slide slide14"></div>
        <div class="slide slide15"></div>
        <div class="slide slide16"></div>
        <div class="slide slide17"></div>
        <div class="slide slide18"></div>
        <div class="slide slide19"></div>
        <div class="slide slide20"></div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.the-content-housing {
	position: relative;
	padding-bottom: 300px;

  .the-title {
		max-width: 660px;
		margin: 0 auto;
    color: #fffffa;
    font-family: "Amatic SC", cursive;
    font-weight: bold;
    font-size: 32px;
    padding: 0;
    text-align: left;
    margin-bottom: 100px;
  }

  .the-cool-thing {
    color: #fffffa;
    font-family: "Beth Ellen", cursive;
    font-size: 26px;
  }
}

.slider-container {
	position: relative;
	overflow: hidden;

	.move {
		position: absolute;
		display: inline-block;
		width: 50%;
		height: 100%;
		top: 0;
		z-index: 10;
		background-color: transparent;
		
		&.move-left { 
			left: 0;
		}

		&.move-right { 
			right: 0;
		}		
	}


  .slider {
		display: flex;
		align-items: center;

		.slide {
			margin-right: 50px;

			&:last-child {
				margin-right: 0;
			}
		}
  }
}
</style>

<script>
const generateRandomColor = () => {
  const letters = "0123456789ABCDEF";
  let color = "#";
  for (var i = 0; i < 6; i++) {
    color += letters[Math.floor(Math.random() * 16)];
  }
  return color;
};

const generateDimensions = () => {
	return parseInt( (Math.random() * (+280 - +150) + +150).toFixed(0));
}

export default {
	data: () => ({
		totalWidth: 0,
		runAnimation: false,
		animationRunning: false,
		sliderPosition: 0,
		moveLeft: false,
		moveRight: false,
		window: {
      width: null,
      height: null
    }
	}),
  mounted() {
		// Get that sweet width.
		window.addEventListener('resize', this.handleResize)
		this.handleResize();
		
		let totalWidth = 0;

		// Make those random ass boxes.
    this.$el.querySelectorAll(".slider .slide").forEach(slide => {
			slide.style.backgroundColor = generateRandomColor();
			const dimension = generateDimensions()
			slide.style.minWidth = `${dimension}px`;
			slide.style.minHeight = `${dimension}px`;
			const gap = parseInt(getComputedStyle(slide).marginRight, 10);

			totalWidth = totalWidth + (dimension + gap);
		});

		const slider = this.$el.querySelector('.slider');

		this.sliderPosition = -(totalWidth / 2).toFixed(0);
		slider.style.transform = `translateX(${this.sliderPosition}px)`

		// console.log(this.totalWidth, totalWidth)
		this.totalWidth = totalWidth;
  },
  methods: {
		mouseOverGeneral() { 
			this.runAnimation = true; 
			this.animation()
		},
		mouseLeaveGeneral() { 
			this.runAnimation = false; 
		},
		
		mouseOverLeft() {
			this.moveLeft = true
		},
		mouseLeaveLeft() {
			this.moveLeft = false;
		},
		mouseOverRight() {
			this.moveRight = true;
		},
		mouseLeaveRight() {
			this.moveRight = false;
		},

		handleResize() {
      this.window.width = window.innerWidth;
      this.window.height = window.innerHeight;
		},

		itsTimeToStop() {
			const half = (this.window.width / 2).toFixed(0);

			const rightCondition = this.sliderPosition.toFixed(0) <= -(this.totalWidth - half);
			if(this.moveLeft && rightCondition) {
				return true
			}

			const leftCondition = this.sliderPosition  >= half;
			if(this.moveRight && leftCondition) {
				return true
			}

			return false
		},

		theRealAnimation(speed) {
			if(!this.runAnimation || this.itsTimeToStop()) {
				this.animationRunning = false;
				return;
			}

			this.animationRunning = true;
			
			if(this.moveLeft) { this.sliderPosition -= speed; }
			else if(this.moveRight) { this.sliderPosition += speed; }

			const slider = this.$el.querySelector('.slider')
			slider.style.transform = `translateX(${this.sliderPosition}px)`

			// Need to make the box look like its speeding up but no to infinity.
			if(speed < 8) { speed = speed + 0.1 }

			window.requestAnimationFrame(() => this.theRealAnimation(speed))
		},

		animation() {
			if(this.runAnimation && !this.animationRunning) {
				window.requestAnimationFrame(() => this.theRealAnimation(1))
			}
		}
  }
};
</script>