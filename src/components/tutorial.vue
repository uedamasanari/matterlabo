<template>
    <div class="game" ref="game"></div>
</template>
<script>
import Matter from 'matter-js'
import { ref,onMounted } from 'vue';

export default {
  setup() {
    const game = ref(null);
    onMounted(()=> {
    console.log(game.value);
    var MouseConstraint = Matter.MouseConstraint;
    var Engine = Matter.Engine, 
    Render = Matter.Render,
    Runner = Matter.Runner,
    Bodies = Matter.Bodies,
    Composite = Matter.Composite,
    Mouse = Matter.Mouse;
    

    
    // create an engine
    var engine = Engine.create();

    // create a renderer
    var render = Render.create({
        element: game.value,
        engine: engine,
        options: {
            width:400,
            height:400,
            background: '#ffffff',
            wireframes: false,
        }
    });

    // create two boxes and a ground
    var box1= Bodies.rectangle(
        Math.floor(Math.random()*400), // x座標をランダムに設定
        100, 
        40,
        40,
        {
            isStatic: false, // 固定しない
            density: 1.5, // 質量
            friction: 0, // 摩擦
            restitution: 1.3, // 跳ね返り
        }
        );
    var box2 = Bodies.rectangle(
        Math.floor(Math.random()*400), // x座標をランダムに設定
        200, 
        40,
        40,
        {
            isStatic: false, // 固定しない
            density: 1.5, // 質量
            friction: 0, // 摩擦
            restitution: 1.3, // 跳ね返り
        }
        );
        var box3 = Bodies.rectangle(
        Math.floor(Math.random()*400), // x座標をランダムに設定
        50, 
        40,
        40,
        {
            isStatic: false, // 固定しない
            density: 1.5, // 質量
            friction: 0, // 摩擦
            restitution: 1.3, // 跳ね返り
        }
        );
        var box4 = Bodies.rectangle(
        Math.floor(Math.random()*400), // x座標をランダムに設定
        60, 
        40,
        40,
        {
            isStatic: false, // 固定しない
            density: 1.5, // 質量
            friction: 0, // 摩擦
            restitution: 1.3, // 跳ね返り
        }
        );
        var box5 = Bodies.rectangle(
        Math.floor(Math.random()*400), // x座標をランダムに設定
        300, 
        40,
        40,
        {
            isStatic: false, // 固定しない
            density: 1.5, // 質量
            friction: 0, // 摩擦
            restitution: 1.3, // 跳ね返り
        }
        );
        var box6 = Bodies.rectangle(
        Math.floor(Math.random()*400), // x座標をランダムに設定
        350, 
        40,
        40,
        {
            isStatic: false, // 固定しない
            density: 1.5, // 質量
            friction: 0, // 摩擦
            restitution: 1.3, // 跳ね返り
        }
        );
        var box7 = Bodies.rectangle(
        Math.floor(Math.random()*400), // x座標をランダムに設定
        350, 
        40,
        40,
        {
            isStatic: false, // 固定しない
            density: 1.5, // 質量
            friction: 0, // 摩擦
            restitution: 1.3, // 跳ね返り
        }
        );
        var box8 = Bodies.rectangle(
        Math.floor(Math.random()*400), // x座標をランダムに設定
        400, 
        40,
        40,
        {
            isStatic: false, // 固定しない
            density: 1.5, // 質量
            friction: 0, // 摩擦
            restitution: 1.3, // 跳ね返り
        }
        );
        var box9 = Bodies.rectangle(
        Math.floor(Math.random()*400), // x座標をランダムに設定
        200, 
        40,
        40,
        {
            isStatic: false, // 固定しない
            density: 1.5, // 質量
            friction: 0, // 摩擦
            restitution: 1.3, // 跳ね返り
        }
        );
        var box10 = Bodies.rectangle(
        Math.floor(Math.random()*400), // x座標をランダムに設定
        200, 
        40,
        40,
        {
            isStatic: false, // 固定しない
            density: 1.5, // 質量
            friction: 0, // 摩擦
            restitution: 1.3, // 跳ね返り
        }
        );
    var ground1 = Bodies.rectangle(200, 400, 400, 60, { isStatic: true });
    var ground2 = Bodies.rectangle(0, 0, 60, 800, { isStatic: true });
    var ground3 = Bodies.rectangle(400, 0, 60, 800, { isStatic: true });
    var ground4 = Bodies.rectangle(0, 0, 800, 60, { isStatic: true });
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

    Composite.add(
    engine.world,
    mouseConstraint
    );

    // add all of the bodies to the world
    Composite.add(engine.world, [box1,box2,box3,box4,box5,box6,box7,box8,box9,box10,ground1,ground2,ground3,ground4]);

    // run the renderer
    Render.run(render);

    // create runner
    var runner = Runner.create();

    // run the engine
    Runner.run(runner, engine);
  })
    return {
        game,
    };
  }
  
};
</script>
<style scoped>
.game{
    margin:auto;
    margin-top:30vh;
    width: 400px;
    height: 400px;
}
</style>
