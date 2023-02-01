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
    // module aliases
var Engine = Matter.Engine, 
    Render = Matter.Render,
    Runner = Matter.Runner,
    Bodies = Matter.Bodies,
    Composite = Matter.Composite;

// create an engine
var engine = Engine.create();

// create a renderer
var render = Render.create({
    element: game.value,
    engine: engine
});

// create two boxes and a ground
var boxA = Bodies.rectangle(400, 200, 80, 80);
var boxB = Bodies.rectangle(450, 50, 80, 80);
var ground = Bodies.rectangle(400, 610, 810, 60, { isStatic: true });

// add all of the bodies to the world
Composite.add(engine.world, [boxA, boxB, ground]);

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
    /* margin-top:30vh; */
    width: 400px;
    height: 400px;
}
</style>
