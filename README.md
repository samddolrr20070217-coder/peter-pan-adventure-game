const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

canvas.width = innerWidth;
canvas.height = innerHeight;

const player = {
  x:100,
  y:200,
  w:50,
  h:80,
  speed:7
};

let up=false;
let down=false;

document.addEventListener("keydown",(e)=>{
  if(e.key==="ArrowUp") up=true;
  if(e.key==="ArrowDown") down=true;
});

document.addEventListener("keyup",(e)=>{
  if(e.key==="ArrowUp") up=false;
  if(e.key==="ArrowDown") down=false;
});

document.getElementById("up").ontouchstart=()=>up=true;
document.getElementById("up").ontouchend=()=>up=false;

document.getElementById("down").ontouchstart=()=>down=true;
document.getElementById("down").ontouchend=()=>down=false;

function drawPlayer(){

  ctx.fillStyle="#00ff88";

  ctx.fillRect(
    player.x,
    player.y,
    player.w,
    player.h
  );

  ctx.beginPath();

  ctx.arc(
    player.x+25,
    player.y-15,
    20,
    0,
    Math.PI*2
  );

  ctx.fill();
}

function update(){

  if(up) player.y-=player.speed;
  if(down) player.y+=player.speed;

  if(player.y<0) player.y=0;

  if(player.y+player.h>canvas.height)
    player.y=canvas.height-player.h;
}

function loop(){

  ctx.clearRect(0,0,canvas.width,canvas.height);

  update();

  drawPlayer();

  requestAnimationFrame(loop);
}

loop();
