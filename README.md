Project Saadhana -Web application to interact either computer

Deevenseru
Deevenseru
12 min read
·
3 hours ago





Current Scenario: Traditional computer interaction methods like mice and keyboards can be limiting for individuals with physical disabilities or repetitive strain injuries.
Identifying Facial Movements and Controlling Your Cursor: A New Era of Accessibility
In today’s digital age, technology is constantly evolving to make our lives easier and more accessible. One exciting development is the use of facial recognition technology to control computer interfaces. Our team has developed a web application that takes this a step further by utilizing facial movement detection to move the cursor on your screen.
How Does It Work?
Our web application leverages advanced computer vision techniques to analyze facial expressions in real-time. By detecting specific movements, such as head nods, eye blinks, or mouth movements, the system can accurately interpret user intent and translate it into cursor movements.
Key Features and Benefits:
Intuitive Control: The system’s user-friendly interface allows for seamless interaction, making it easy for users to navigate their devices without physical input.
Enhanced Accessibility: This technology opens up new possibilities for individuals with disabilities, providing them with greater independence and control over their digital experiences.
Innovative Application: Beyond accessibility, this technology has potential applications in gaming, virtual reality, and other fields that require hands-free interaction.

doc<!type html>
<html>
<head>
  <!-- <base href="/"> -->
  <meta charset="utf-8">
  <meta http-equiv="Cache-control" content="no-cache, no-store, must-revalidate">
  <meta http-equiv="Pragma" content="no-cache">
  <meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no">
  <title>UFO Shooting</title>

  <link href="https://unpkg.com/material-components-web@latest/dist/material-components-web.min.css" rel="stylesheet">
  <script src="https://unpkg.com/material-components-web@latest/dist/material-components-web.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.4/gsap.min.js" integrity="sha512-f8mwTB+Bs8a5c46DEm7HQLcJuHMBaH/UFlcgyetMqqkvTcYg4g5VXsYR71b3qC82lZytjNYvBj2pf0VekA9/FQ==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
</head>
<body>
  <canvas class="game-canvas" id="game-canvas"></canvas>
  <div class="camera">
    <div class="output-wrapper">
      <video autoplay class="input-video" id="input-video"></video>
      <canvas class="output-canvas" id="output-canvas" width="720px" height="480px"></canvas>
    </div>
    <form class="form-controller">
      <div class="form-group">
        <label class="form-label">Movement scale ratio: <strong class="slider-movement-scale-value">3</strong></label>
        <div class="flex-space-between">
          <span>1</span>
          <span>10</span>
        </div>
        <div class="mdc-slider mdc-slider--discrete slider-movement-scale">
          <input class="mdc-slider__input" type="range" min="1" max="10" value="3" name="volume" step="1" aria-label="Movement scale slider">
          <div class="mdc-slider__track">
            <div class="mdc-slider__track--inactive"></div>
            <div class="mdc-slider__track--active">
              <div class="mdc-slider__track--active_fill"></div>
            </div>
          </div>
          <div class="mdc-slider__thumb">
            <div class="mdc-slider__value-indicator-container" aria-hidden="true">
              <div class="mdc-slider__value-indicator">
                <span class="mdc-slider__value-indicator-text">
                  3
                </span>
              </div>
            </div>
            <div class="mdc-slider__thumb-knob"></div>
          </div>
        </div>
      </div>
    </form>
  </div>
  <div class="score-dialog">
    <p class="score-point">0</p>
    <p class="score-label">Points</p>
    <p class="score-label" style="margin-top: 16px;">Hello welcome to Twilight.AI .</p>
    <p class="score-label" style="margin-top: 16px;"><b>An ai model that identifies face form the core level of the host device and stays on the target movement </b> all the data is stored natively on uour device Twillight.AI uses its face mapping algorithms to keep track of your face <b>To gamify the user experience  MOVE YOUR HEAD TO MOVE THE GREEN DOT open your mouth</b> to start firing.</p>
    <p class="score-label" style="margin-top: 16px;">Make sure to give permission to enable your camera.</p>
    <div class="dialog-actions">
      <button class="start-btn">Start game</button>
    </div>
  </div>
</body>
</html>


@use "@material";
@use "@material/floating-label/mdc-floating-label";
@use "@material/line-ripple/mdc-line-ripple";
@use "@material/notched-outline/mdc-notched-outline";
@use "@material/textfield";
@use "@material/slider/styles";

* {
  box-sizing: border-box;
}

body {
  font-family: helvetica, arial, sans-serif;
  margin: 0;
  padding: 0;
  border: 0;
  background-color: #000000;
  color: #ffffff;
  --mdc-theme-primary: #007f8b;
  --mdc-theme-on-primary: #f1f3f4;
}

h1 {
  font-style: italic;
  color: #007f8b;
}

h2 {
  clear: both;
}

em {
  font-weight: bold;
}

video {
  clear: both;
  display: block;
  transform: rotateY(180deg);
  -webkit-transform: rotateY(180deg);
  -moz-transform: rotateY(180deg);
  /* height: 280px; */
}

section {
  opacity: 1;
  transition: opacity 500ms ease-in-out;
}

.input-video,
.output-canvas {
  display: block;
  max-width: 100%;
  margin: 0 auto;
  transform: rotateY(180deg);
  -webkit-transform: rotateY(180deg);
  -moz-transform: rotateY(180deg);
}
.result {
  text-align: center;
  font-size: 24px;
  padding: 16px;
}
.input-video {
  display: none;
}

.output-wrapper {
  position: relative;
  background: linear-gradient(-45deg, #cccccc, #ffffff, #D9D9D9);
  background-size: 400% 400%;
  animation: gradient 2s ease infinite;
}

@keyframes gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

.output-wrapper::after {
  position: absolute;
  content: "";
  display: block;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 1;
  border: 80px solid transparent;
}
.output-wrapper.top::after {
  border-top-color: rgba(0, 255, 0, 0.4);
}
.output-wrapper.left::after {
  border-left-color: rgba(0, 255, 0, 0.4);
}
.output-wrapper.right::after {
  border-right-color: rgba(0, 255, 0, 0.4);
}
.output-wrapper.bottom::after {
  border-bottom-color: rgba(0, 255, 0, 0.4);
}

.camera {
  position: fixed;
  right: 32px;
  bottom: 0;
  width: 240px;
  z-index: 1;
  opacity: 0.5;
}
.camera:hover {
  opacity: 1;
}

@media (max-width: 576px) {
  .camera {
    width: 120px;
    font-size: 10px;
  }
}

.screen-simulation {
  height: 100vh;
  padding: 2em;
}

.output-screen {
  position: relative;
  max-width: 100%;
  max-height: 100%;
  width: 100%;
  height: 100%;
  margin: 0 auto;
  border: 1px solid #000;
}

.output-point {
  position: absolute;
  display: block;
  width: 8px;
  height: 8px;
  top: calc(50% - 4px);
  left: calc(50% - 4px);
  background-color: #000;
  border-radius: 50%;
}

.form-controller {
  padding: 16px 0;
}
.form-group:not(:last-child) {
  margin-bottom: 16px;
}

.txt-center {
  text-align: center;
}
.flex-space-between {
  display: flex;
  justify-content: space-between;
  padding: 8px 16px 0;
  margin-bottom: -8px;
}

.mouse-simulation {
  position: absolute;
  left: 136px;
  bottom: 16px;
  width: 80px;
  height: 100px;
  border: 2px solid #000000;
  border-radius: 38px;
  overflow: hidden;
  display: flex;
  flex-wrap: wrap;
}
.mouse-simulation-left,
.mouse-simulation-right {
  display: flex;
  width: 38px;
  background-color: transparent;
  border: 1px solid #000000;
}
.mouse-simulation-body {
  display: flex;
  width: 100%;
  border: 1px solid #000000;
}

.arrow-simulation {
  position: absolute;
  display: flex;
  flex-wrap: wrap;
  left: 32px;
  bottom: 32px;
  width: 70px;
  height: 70px;
  border: 2px solid #000000;
  transform: rotateZ(45deg);
}
.arrow-simulation-body {
  position: absolute;
  left: 9px;
  bottom: 9px;
  width: 48px;
  height: 48px;
  background-color: #ffffff;
  border: 2px solid #000000;
  transform: rotateZ(45deg);
  z-index: 1;
}
.arrow-simulation-top,
.arrow-simulation-left,
.arrow-simulation-right,
.arrow-simulation-bottom {
  width: 50%;
}

.arrow-simulation.top .arrow-simulation-top {
  background-color: #30FF30;
}
.arrow-simulation.left .arrow-simulation-left {
  background-color: #30FF30;
}
.arrow-simulation.right .arrow-simulation-right {
  background-color: #30FF30;
}
.arrow-simulation.bottom .arrow-simulation-bottom {
  background-color: #30FF30;
}

.guideline {
  text-align: center;
}
.guideline img {
  width: 80%;
}

.score-wrapper {
  position: fixed;
  top: 16px;
  left: 16px;
}

.score-dialog {
  position: fixed;
  top: 50%;
  left: 50%;
  width: 400px;
  padding: 32px;
  transform: translate(-50%, -50%);
  background-color: #ffffff;
  color: #000000;
  text-align: center;
  z-index: 2;
}

.score-dialog p {
  margin: 0;
}
.score-dialog .score-point {
  font-size: 40px;
  font-weight: 500;
}
.score-dialog .dialog-actions {
  margin-top: 32px;
}

.score-dialog button {
  width: 100%;
  padding: 8px;
  border: 0;
  border-radius: 16px;
  background-color: cadetblue;
  color: #ffffff;
  font-size: 24px;
  font-weight: 500;
  cursor: pointer;
}


import {
  FaceLandmarker, 
  FaceLandmarkerResult, 
  FilesetResolver
} from "https://cdn.jsdelivr.net/npm/@mediapipe/tasks-vision@0.10.0";


class Player {
  x: number;
  y: number;
  radius: number;
  color: string;

  constructor(x: number, y: number, radius: number, color: string) {
    this.x = x;
    this.y = y;
    this.radius = radius;
    this.color = color;
  }

  draw(ctx: CanvasRenderingContext2D) {
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2, false);
    ctx.fillStyle = this.color;
    ctx.fill();
  }
}
class Projectile {
  x: number;
  y: number;
  radius: number;
  color: string;
  velocity: {x: number, y: number};

  constructor(x: number, y: number, radius: number, color: string, velocity) {
    this.x = x;
    this.y = y;
    this.radius = radius;
    this.color = color;
    this.velocity = velocity;
  }

  draw(ctx: CanvasRenderingContext2D) {
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2, false);
    ctx.fillStyle = this.color;
    ctx.fill();
  }

  update(ctx: CanvasRenderingContext2D) {
    this.draw(ctx);
    this.x += this.velocity.x;
    this.y += this.velocity.y;
  }
}
class Enemy {
  x: number;
  y: number;
  radius: number;
  color: string;
  velocity: {x: number, y: number};

  constructor(x: number, y: number, radius: number, color: string, velocity) {
    this.x = x;
    this.y = y;
    this.radius = radius;
    this.color = color;
    this.velocity = velocity;
  }

  draw(ctx: CanvasRenderingContext2D) {
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2, false);
    ctx.fillStyle = this.color;
    ctx.fill();
  }

  update(ctx: CanvasRenderingContext2D) {
    this.draw(ctx);
    this.x += this.velocity.x;
    this.y += this.velocity.y;
  }
}
class Particle {
  x: number;
  y: number;
  radius: number;
  color: string;
  velocity: {x: number, y: number};
  alpha: number;

  constructor(x: number, y: number, radius: number, color: string, velocity) {
    this.x = x;
    this.y = y;
    this.radius = radius;
    this.color = color;
    this.velocity = velocity;
    this.alpha = 1;
  }

  draw(ctx: CanvasRenderingContext2D) {
    ctx.save();
    ctx.globalAlpha = this.alpha;
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2, false);
    ctx.fillStyle = this.color;
    ctx.fill();
    ctx.restore();
  }

  update(ctx: CanvasRenderingContext2D) {
    this.draw(ctx);
    // Slow fown
    this.velocity.x *= 0.99;
    this.velocity.y *= 0.99;
    this.x += this.velocity.x;
    this.y += this.velocity.y;
    this.alpha -= 0.01;
  }
}
class GameBoard {
  gameCanvas: HTMLCanvasElement;
  ctxGame: CanvasRenderingContext2D;
  // scoreEl: HTMLElement;
  width: number;
  height: number;
  player: Player;
  projectiles: Projectile[] = [];
  enemies: Enemy[] = [];
  particles: Particle[] = [];
  score: number;
  onGameOver: (score: number) => void;
  animateObj;
  spawmEnemiesInterval;
  gameLevel = {
    1: 4000,
    2: 3000,
    3: 2000,
    4: 1000,
    5: 800,
    6: 600,
    7: 500,
    8: 400,
    9: 300,
    other: 300
  }
  currentLevel = 1;

  constructor(canvas, ctx, onGameOver, width = window.innerWidth, height = window.innerHeight) {
    this.gameCanvas = canvas;
    this.ctxGame = ctx;
    this.onGameOver = onGameOver;
    this.width = width;
    this.height = height

    this.gameCanvas.width = this.width;
    this.gameCanvas.height = this.height;
    this.player = new Player(this.gameCanvas.width / 2, this.gameCanvas.height / 2, 20, '#ffffff');
    this.score = 20;
    this.currentLevel = 1;
  }

  init() {
    this.player = new Player(this.gameCanvas.width / 2, this.gameCanvas.height / 2, 20, '#ffffff');
    this.projectiles = [];
    this.enemies.length = 0;
    this.particles = [];
    this.score = 20;
    this.currentLevel = 1;
  }

  clearSpawmEnemier() {
    if (this.spawmEnemiesInterval) {
      clearInterval(this.spawmEnemiesInterval);
    }
  }
  
  changesize(width = window.innerWidth, height = window.innerHeight) {
    this.width = width;
    this.height = height

    this.gameCanvas.width = this.width;
    this.gameCanvas.height = this.height;
    this.player.x = this.gameCanvas.width / 2;
    this.player.y = this.gameCanvas.height / 2;
  }

  spawmEnemies = () => {
    this.spawmEnemiesInterval = setInterval(() => {
      const radius = Math.random() * (30 - 4) + 10;
      let x;
      let y;
  
      if (Math.random() < 0.5) {
        x = Math.random() < 0.5 ? 0 - radius : this.gameCanvas.width + radius;
        y = Math.random() * this.gameCanvas.height;
      } else {
        x = Math.random() * this.gameCanvas.width;
        y = Math.random() < 0.5 ? 0 - radius : this.gameCanvas.height + radius;
      }
      const angel = Math.atan2(
        this.gameCanvas.height / 2 - y,
        this.gameCanvas.width / 2 - x
      );
      const velocity = {
        x: Math.cos(angel),
        y: Math.sin(angel)
      }
      this.enemies.push(new Enemy(
        x,
        y,
        radius,
        `hsl(${Math.random() * 360}, 50%, 50%)`,
        velocity
      ));
    },
 
    this.gameLevel[this.currentLevel] || this.gameLevel['other']);
  };

  start = () => {
    this.init();
    this.run();
    this.spawmEnemies();
    this.updateScore();
  }

  run = () => {
    this.animateObj = requestAnimationFrame(this.run);
    this.ctxGame.fillStyle = 'rgba(0,0,0,0.1)';
    this.ctxGame.fillRect(0, 0, this.gameCanvas.width, this.gameCanvas.height);
    this.player.draw(this.ctxGame);
    this.updateScore();

    this.particles.forEach((particle, index) => {
      if (particle.alpha <= 0) {
        this.particles.splice(index, 1);
      } else {
        particle.update(this.ctxGame);
      }
    });

    this.projectiles.forEach((projectile, index) => {
      projectile.update(this.ctxGame);

     
      if (
        projectile.x + projectile.radius < 0 ||
        projectile.x - projectile.radius > this.gameCanvas.width ||
        projectile.y + projectile.radius < 0 ||
        projectile.y - projectile.radius > this.gameCanvas.height
      ) {
        setTimeout(() => {
          this.projectiles.splice(index, 1);
        }, 0);
      }
    });

    this.enemies.forEach((enemy, index) => {
      enemy.update(this.ctxGame);

      const distancePlayer = Math.hypot(this.player.x - enemy.x, this.player.y - enemy.y);
      if (distancePlayer - enemy.radius - this.player.radius < 1) {
        cancelAnimationFrame(this.animateObj);
        
        if (this.onGameOver) {
          this.onGameOver(this.score);
        }
        this.clearSpawmEnemier();
      }

      this.projectiles.forEach((projectile, indexPro) => {
        const distance = Math.hypot(projectile.x - enemy.x, projectile.y - enemy.y);
        if (distance - enemy.radius - projectile.radius < 1) {

          
          for (let i = 0; i < enemy.radius * 2; i++) {
            this.particles.push(new Particle(
              projectile.x,
              projectile.y,
              Math.random() * 2,
              enemy.color,
              {
                x: (Math.random() - 0.5) * (Math.random() * 6),
                y: (Math.random() - 0.5) * (Math.random() * 6)
              }
            ));
          }

          if (enemy.radius - 6 > 10) {
            
            window['gsap'].to(enemy, {
              radius: enemy.radius - 6
            })
            this.score += 10;
            setTimeout(() => {
              this.projectiles.splice(indexPro, 1);
            }, 0);
          } else {
            
            this.score += 20;
            setTimeout(() => {
              this.enemies.splice(index, 1);
              this.projectiles.splice(indexPro, 1);
            }, 0);
          }
   
        }
      });
    });
  };

  createProjectile = (x: number, y: number) => {
    const angel = Math.atan2(
      y - this.gameCanvas.height / 2,
      x - this.gameCanvas.width / 2
    );
    const velocity = {
      x: Math.cos(angel) * 6,
      y: Math.sin(angel) * 6
    };
    this.projectiles.push(new Projectile(
      this.gameCanvas.width / 2,
      this.gameCanvas.height / 2,
      5,
      '#ffffff',
      velocity
    ));

    
    this.score -= 1;
  };

  updateScore = () => {
    this.ctxGame.font = '20px sans-serif';
    this.ctxGame.textBaseline = 'top';
    this.ctxGame.fillStyle = '#FFFFFF';
    this.ctxGame.fillText(`Score: ${this.score} - Current level: ${this.currentLevel}`, 16, 16);

    
    if (this.currentLevel < 9 && this.score > this.currentLevel * 1000) {
      this.currentLevel += 1;
      this.clearSpawmEnemier();
      this.spawmEnemies();
    }
  }
}


export class FaceDetector {
  faceLandmarker: FaceLandmarker;
  cameraWidth: number;
  cameraHeight: number;
  cameraEl: HTMLVideoElement;
  canvas: HTMLCanvasElement;
  canvasCtx: CanvasRenderingContext2D;
  constructor(
    faceLandmarker: FaceLandmarker,
    cameraEl: HTMLVideoElement,
    canvasEl: HTMLCanvasElement,
    width: number = 720,
    height: number = 480
  ) {
    this.cameraEl = cameraEl;
    this.faceLandmarker = faceLandmarker;
    this.cameraWidth = window.innerWidth < window.innerHeight ? height : width;
    this.cameraHeight = window.innerWidth < window.innerHeight ? width : height;
    this.canvas = canvasEl;
    this.canvas.width = this.cameraWidth;
    this.canvas.height = this.cameraHeight;
    this.canvasCtx = this.canvas.getContext('2d');
  }

  draw = (results: FaceLandmarkerResult, cameraEl: HTMLVideoElement) => {
    this.canvasCtx.save();
    this.canvasCtx.clearRect(0, 0, this.canvas.width, this.canvas.height);
    this.canvasCtx.drawImage(cameraEl, 0, 0, this.canvas.width, this.canvas.height);
    if (results.faceLandmarks.length) {
      const facePoints = [
        // Face oval
        // results.multiFaceLandmarks[0][10],
        // results.multiFaceLandmarks[0][323],
        // results.multiFaceLandmarks[0][93],
        // results.multiFaceLandmarks[0][152],
        results.faceLandmarks[0][8], // between eyes 168, 8, 9
        // Lips inner
        // results.multiFaceLandmarks[0][78],
        // results.multiFaceLandmarks[0][13],
        // results.multiFaceLandmarks[0][308],
        // results.multiFaceLandmarks[0][14],
      ]
      // Example draw key points
      for (const key of facePoints) {
        this.canvasCtx.beginPath();
        this.canvasCtx.arc(key.x * this.cameraWidth, key.y * this.cameraHeight, 4, 0, 2 * Math.PI);
        this.canvasCtx.fillStyle = '#30FF30';
        this.canvasCtx.fill();
      }
    }
    this.canvasCtx.restore();
    this.onResults(results);
  };

  onResults: (results) =>void }
{

const MDCSlider = mdc.slider.MDCSlider;
const videoElement = document.getElementById('input-video') as HTMLVideoElement;
const canvasElement = document.getElementById('output-canvas') as HTMLCanvasElement;

const outputScreen = document.getElementsByClassName('output-screen')[0] as HTMLElement;

const startBtn = document.getElementsByClassName('start-btn')[0] as HTMLButtonElement;
const scoreDialog = document.getElementsByClassName('score-dialog')[0] as HTMLElement;
const scorePoint = document.getElementsByClassName('score-point')[0] as HTMLElement;

const CAMERA_WIDTH = 720;
const CAMERA_HEIGHT = 480;
const MOVEMENT_SCALE = 3;
let SCREEN_WIDTH = 720;
let SCREEN_HEIGHT = 480;
const FRAME_TO_FIGHT = 6;


const sliderMovementScale = new MDCSlider(document.querySelector('.slider-movement-scale'));
const txtMovementScale = document.getElementsByClassName('slider-movement-scale-value')[0] as HTMLElement;


sliderMovementScale.listen('MDCSlider:change', () => {
  txtMovementScale.innerHTML = `${sliderMovementScale.getValue()}`;
});


sliderMovementScale.setValue(MOVEMENT_SCALE);


let startPoint: {x: number, y: number} = null;
let prevPoint: {x: number, y: number} = null;


let frameToFight = FRAME_TO_FIGHT;


let isGameRunning = false;


const detectSimulationScreen = () => {
  if (outputScreen) {
    SCREEN_WIDTH = outputScreen.offsetWidth - 2; 
    SCREEN_HEIGHT = outputScreen.offsetHeight - 2
  }
};
detectSimulationScreen();

const distance2Points = (point1, point2) => {
  return Math.sqrt((point2.x - point1.x)**2 + (point2.y - point1.y)**2 + (point2.z - point1.z)**2);
};

const moveDistance = (point1, point2) => {
  return {
    moveX: point2.x - point1.x,
    moveY: point2.y - point1.y
  }
};

const getMovementScale = (point1, point2) => {
  const scaleRatio = sliderMovementScale.getValue();
  return {
    newX: (point2.x - point1.x) * scaleRatio,
    newY: (point2.y - point1.y) * scaleRatio
  };
}

const detectMovement = (newPoint) => {
  if (!startPoint || !startPoint['x'] || !startPoint['y']) {
    startPoint = {x: newPoint.x, y: newPoint.y};
    prevPoint = {x: newPoint.x, y: newPoint.y};
    return prevPoint;
  }

  const movement =  getMovementScale(startPoint, newPoint);
  prevPoint.x = startPoint.x + movement.newX;
  prevPoint.y = startPoint.y + movement.newY;
  return {
    x: prevPoint['x'],
    y: prevPoint['y']
  }
};

const detectMouthOpen = (landmarks) => {
  return distance2Points(landmarks[0][13], landmarks[0][14]) > 0.02;
}

function onResults(results: FaceLandmarkerResult) {
  if (results.faceLandmarks.length) {
    const isOpenMouth = detectMouthOpen(results.faceLandmarks);
    const { x, y } = detectMovement(results.faceLandmarks[0][8]);
    
    const newX = window.innerWidth - (x * window.innerWidth); 
    const newY = y * window.innerHeight;
    
   
    if (isGameRunning) {
      ctxGame.beginPath();
      ctxGame.arc(newX, newY, 4, 0, 2 * Math.PI);
      ctxGame.fillStyle = '#30FF30';
      ctxGame.fill();
  
      if (isOpenMouth) {
        frameToFight += 1;
        if (frameToFight > FRAME_TO_FIGHT) {
          gameBoard.createProjectile(newX, newY);
          frameToFight = 0;
        }
      } else {
        frameToFight = FRAME_TO_FIGHT;
      }
    }
  }
};

let faceDetector: FaceDetector

async function createFaceDetector() {
  console.log("Loading face landmarker model.");
  const vision = await FilesetResolver.forVisionTasks('https://cdn.jsdelivr.net/npm/@mediapipe/tasks-vision@0.10.0/wasm');
  const faceLandmarker = await FaceLandmarker.createFromOptions(vision, {
    baseOptions: {
      modelAssetPath: `https://storage.googleapis.com/mediapipe-models/face_landmarker/face_landmarker/float16/1/face_landmarker.task`,
    },
    runningMode: 'VIDEO',
    outputFaceBlendshapes: true,
    numFaces: 1
  });
  console.log("Face landmarker model loaded successfully.")
  faceDetector = new FaceDetector(
    faceLandmarker,
    videoElement,
    canvasElement,
    CAMERA_WIDTH,
    CAMERA_HEIGHT,
  );
  faceDetector.onResults = onResults;
}

createFaceDetector();


function hasGetUserMedia() {
  return !!(navigator.mediaDevices && navigator.mediaDevices.getUserMedia);
}

const constraints = {
  video: true
};


navigator.mediaDevices.getUserMedia(constraints).then(function (stream) {
  videoElement.srcObject = stream;
  videoElement.addEventListener('loadeddata', predictWebcam);
});

async function predictWebcam() {
  let nowInMs = Date.now();
  if (!faceDetector) {
    window.requestAnimationFrame(predictWebcam);
    return 
  }
  const results = await faceDetector.faceLandmarker.detectForVideo(videoElement, nowInMs);
  faceDetector.draw(results, videoElement);
  window.requestAnimationFrame(predictWebcam);
}


const gameCanvas = document.getElementById('game-canvas') as HTMLCanvasElement;
const ctxGame = gameCanvas.getContext('2d') as CanvasRenderingContext2D;

const gameOverFunc = (score: number) => {
  isGameRunning = false;
  scorePoint.innerHTML = `${score}`;
  scoreDialog.style.display = 'block';
}

const gameBoard = new GameBoard(gameCanvas, ctxGame, gameOverFunc);

startBtn.addEventListener('click', () => {
  isGameRunning = true;
  gameBoard.start();
  scoreDialog.style.display = 'none';
});

window.addEventListener('resize', resizeGameBoard, false);

function resizeGameBoard() {
  gameBoard.changesize();
}
Technical Insights:
Facial Landmark Detection: We employ state-of-the-art algorithms to identify key facial features like eyes, nose, and mouth.
Movement Tracking: By monitoring changes in the position and orientation of these features, we can detect subtle movements and trigger corresponding cursor actions.
Real-time Processing: Our system processes video frames in real-time, ensuring a smooth and responsive user experience.
Future Possibilities:
We are excited about the future of facial movement-based control and are actively exploring new ways to expand the capabilities of our technology. Some potential future developments include:
Advanced Gesture Recognition: Recognizing more complex facial gestures to perform a wider range of actions.
Personalized Calibration: Adapting the system to individual user preferences and facial characteristics.
Integration with Other Devices: Enabling control of various devices, such as smart home appliances, through facial commands.
We believe that this technology has the power to revolutionize the way we interact with computers and other devices. By harnessing the power of facial recognition and machine learning, we can create a more inclusive and accessible digital future for all.
[https://codepen.io/SERU-DEEVEN/pen/NWZzrjY]
We is committed to pushing the boundaries of technology and making a positive impact on people’s lives. Stay tuned for more exciting developments in the field of facial recognition .
https://github.com/DEVELOPER-DEEVEN/intellisense.git
https://www.linkedin.com/in/deeven-seru-8176b0254/# intellisense
