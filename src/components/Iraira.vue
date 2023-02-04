<template>
    <button @click="start" class="button">落とす</button>
    <div class="game" ref="game"></div>
    <div class="ball">{{ ball }}</div>
    <div class="point">
       <div>-1</div>
       <div>+3</div>
       <div>-5</div>
       <div>-3</div> 
       <div>+10</div> 
       <div>-1</div> 
       <div>+3</div> 
       <div>-3</div> 
       <div>+5</div> 
       <div>-3</div>
    </div>
</template>
<script setup>
import Matter, { World } from 'matter-js'
import { ref,onMounted,reactive } from 'vue';


    const game = ref(null);
    let ball = ref(5);
    let box1 = reactive([]);
    let Engine = Matter.Engine;
    const engine = Engine.create();
    onMounted(()=> {
    var MouseConstraint = Matter.MouseConstraint;
    var Render = Matter.Render,
    Runner = Matter.Runner,
    Bodies = Matter.Bodies,
    Composite = Matter.Composite,
    Mouse = Matter.Mouse;
    

    
    // create an engine
    

    // create a renderer
    var render = Render.create({
        element: game.value,
        engine: engine,
        options: {
            width:1530,
            height:800,
            background: '#ffffff',
            wireframes: false,
        }
    });
    var image = new Image();
    image.src = "./apple.png";
    // create two boxes and a ground
    
    let hantei=new Array();
    for(let i=0;i<10;i++){
        hantei[i] = Bodies.rectangle(75+i*150, 775, 150, 50, { 
            isSensor: true,
            isStatic: true,
            render: {
                fillStyle: 'transparent'
            } 
        });
        const jama1 = Bodies.circle(35+i*150, 200, 40, { 
            isStatic: true,
        });
        const jama2 = Bodies.circle(145+i*150, 350, 40, { 
            isStatic: true,
        }); 
        const jama3 = Bodies.circle(35+i*150, 500, 40, { 
            isStatic: true,
        }); 
        World.add(engine.world,[hantei[i],jama1,jama2,jama3]);
    }
    var left = Bodies.rectangle(-100, 400, 200, 1000, { isStatic: true });
    var top = Bodies.rectangle(-100, -100, 1530, 200, { isStatic: true });
    var right = Bodies.rectangle(1630, 400, 200, 1000, { isStatic: true });
    var wall1 = Bodies.rectangle(15, 750, 30, 100, { isStatic: true });
    var wall2 = Bodies.rectangle(165, 750, 30, 100, { isStatic: true });
    var wall3 = Bodies.rectangle(315, 750, 30, 100, { isStatic: true });
    var wall4 = Bodies.rectangle(465, 750, 30, 100, { isStatic: true });
    var wall5 = Bodies.rectangle(615, 750, 30, 100, { isStatic: true });
    var wall6 = Bodies.rectangle(765, 750, 30, 100, { isStatic: true });
    var wall7 = Bodies.rectangle(915, 750, 30, 100, { isStatic: true });
    var wall8 = Bodies.rectangle(1065, 750, 30, 100, { isStatic: true });
    var wall9 = Bodies.rectangle(1215, 750, 30, 100, { isStatic: true });
    var wall10 = Bodies.rectangle(1365, 750, 30, 100, { isStatic: true });
    var wall11 = Bodies.rectangle(1515, 750, 30, 100, { isStatic: true });

    var mouse = Mouse.create(render.canvas),
    mouseConstraint = MouseConstraint.create(engine, {
        mouse: mouse,
        constraint: {
          render: {
            visible: false, // マウスを表示するかしないか
          }
        }
    });

    // keep the mouse in sync with rendering
    render.mouse = mouse;

    // Composite.add(
    // engine.world,
    // mouseConstraint
    // );

    // add all of the bodies to the world
    Composite.add(engine.world, [wall1,wall2,wall3,wall4,wall5,wall6,wall7,wall8,wall9,wall10,wall11,left,top,right]);

    // 衝突イベントハンドラを設定
    Matter.Events.on(engine, "collisionStart", function(event) {
    var pairs = event.pairs;
    for (var i = 0; i < pairs.length; i++) {
        var pair = pairs[i];
        console.log(pair)
        for(let j=0;j<box1.length;j++){
        if ((pair.bodyA === box1[j] && pair.bodyB === hantei[0]) || (pair.bodyA === hantei[0] && pair.bodyB === box1[j])) {
        // オブジェクトAとオブジェクトBが衝突した場合はゲームオーバー処理を行う
            if(ball.value>0){
                ball.value-=1;
            }
            box1.splice(j,1);
        }
        if ((pair.bodyA === box1[j] && pair.bodyB === hantei[1]) || (pair.bodyA === hantei[1] && pair.bodyB === box1[j])) {
        // オブジェクトAとオブジェクトBが衝突した場合はゲームオーバー処理を行う
            ball.value+=3;
            box1.splice(j,1);
        }
        if ((pair.bodyA === box1[j] && pair.bodyB === hantei[2]) || (pair.bodyA === hantei[2] && pair.bodyB === box1[j])) {
        // オブジェクトAとオブジェクトBが衝突した場合はゲームオーバー処理を行う
            if(ball.value>4){
                ball.value-=5;
            }else{
                ball.value=0;
            }
            box1.splice(j,1);
        }
        if ((pair.bodyA === box1[j] && pair.bodyB === hantei[3]) || (pair.bodyA === hantei[3] && pair.bodyB === box1[j])) {
        // オブジェクトAとオブジェクトBが衝突した場合はゲームオーバー処理を行う
            if(ball.value>2){
                ball.value-=3;
            }else{
                ball.value=0;
            }
            box1.splice(j,1);
        }
        if ((pair.bodyA === box1[j] && pair.bodyB === hantei[4]) || (pair.bodyA === hantei[4] && pair.bodyB === box1[j])) {
        // オブジェクトAとオブジェクトBが衝突した場合はゲームオーバー処理を行う
            ball.value+=10;
            box1.splice(j,1);
        }
        if ((pair.bodyA === box1[j] && pair.bodyB === hantei[5]) || (pair.bodyA === hantei[5] && pair.bodyB === box1[j])) {
        // オブジェクトAとオブジェクトBが衝突した場合はゲームオーバー処理を行う
            if(ball.value>0){
                ball.value-=1;
            }
            box1.splice(j,1);
        }
        if ((pair.bodyA === box1[j] && pair.bodyB === hantei[6]) || (pair.bodyA === hantei[6] && pair.bodyB === box1[j])) {
        // オブジェクトAとオブジェクトBが衝突した場合はゲームオーバー処理を行う
            ball.value+=3;
            box1.splice(j,1);
        }
        if ((pair.bodyA === box1[j] && pair.bodyB === hantei[7]) || (pair.bodyA === hantei[7] && pair.bodyB === box1[j])) {
        // オブジェクトAとオブジェクトBが衝突した場合はゲームオーバー処理を行う
            if(ball.value>2){
                ball.value-=3;
            }else{
                ball.value=0;
            }
            box1.splice(j,1);
        }
        if ((pair.bodyA === box1[j] && pair.bodyB === hantei[8]) || (pair.bodyA === hantei[8] && pair.bodyB === box1[j])) {
        // オブジェクトAとオブジェクトBが衝突した場合はゲームオーバー処理を行う
            ball.value+=5;
            box1.splice(j,1);
        }
        if ((pair.bodyA === box1[j] && pair.bodyB === hantei[9]) || (pair.bodyA === hantei[9] && pair.bodyB === box1[j])) {
        // オブジェクトAとオブジェクトBが衝突した場合はゲームオーバー処理を行う
            if(ball.value>2){
                ball.value-=3;
            }else{
                ball.value=0;
            }
            box1.splice(j,1);
        }
        }
    }
    });
    // run the renderer
    Render.run(render);

    // create runner
    var runner = Runner.create();

    // run the engine
    Runner.run(runner, engine);
  })

  const start=()=>{
    console.log(box1.length)
    if(ball.value>0){
        ball.value--;
            box1[box1.length] = Matter.Bodies.circle(
            Math.random()*1530, // x座標をランダムに設定
            50, 
            35,
            {
                isStatic: false, // 固定しない
                density: 0.5, // 質量
                friction: 0, // 摩擦
                restitution: 1, // 跳ね返り
                render: {
                    fillStyle: 'red'
                }
            }
        );
        Matter.Composite.add(engine.world, [box1[box1.length-1]]);
    }else{
        alert("ボールがないよ")
    }
}
</script>
<style scoped>
.button{
    position: absolute;
    top:5vh;
    left:2vw;
    width:100px;
    height:50px;
}
.game{
    margin:auto;
    margin-top:2vh;
    width: 1530px;
    height: 800px;
}
.point{
    display: flex;
    justify-content:space-around;
    width:1530px;
    margin:auto;
    font-size: 30px;
}
.ball{
    position: absolute;
    top:15vh;
    left:2vw;
    font-size: 5vw;
    font-weight: bold;
}
</style>
