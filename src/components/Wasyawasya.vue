<template>
    <div ref="matbox" style="width:800px;margin:auto; margin-top: 200px;" />
</template>
<script>
import Matter from 'matter-js'
import { ref,onMounted } from 'vue';

export default {
  setup() {
    const matbox = ref(null);
    onMounted(()=> {
        var Engine = Matter.Engine,
            Render = Matter.Render,
            Runner = Matter.Runner,
            Bodies = Matter.Bodies,
            Composite = Matter.Composite,
            MouseConstraint = Matter.MouseConstraint,
            Mouse = Matter.Mouse;


        // create an engine
        var engine = Engine.create();

        // create a renderer
        var render = Render.create({
            element: matbox.value,
            engine: engine,
            options: {
                // width:500,
                // heigth:500,
                background: "#ffffff",
                wireframes: false
            }
        });

        // create two boxes and a ground
        var boxA = Bodies.circle(450, 100, 50, {
            restitution: 1.2,
            isStatic: false, // 固定しない
            density: 5, // 質量
            friction: 0, // 摩擦
            render: {
                fillStyle: "blue"
            }
        });
        var boxB = Bodies.circle(450, 100, 50, {
            restitution: 1.2,
            isStatic: false, // 固定しない
            density: 0.5, // 質量
            friction: 0, // 摩擦
            render: {
                fillStyle: "red"
            }
        });
        var boxC = Bodies.circle(450, 100, 50, {
            restitution: 1.2,
            isStatic: false, // 固定しない
            density: 0.5, // 質量
            friction: 0, // 摩擦
            render: {
                fillStyle: "red"
            }
        });
        var boxD = Bodies.circle(450, 100, 50, {
            restitution: 1.2,
            isStatic: false, // 固定しない
            density: 0.5, // 質量
            friction: 0, // 摩擦
            render: {
                fillStyle: "red"
            }
        });
        // var ground1 = Bodies.rectangle(400, 600, 800, 60, {
        //     isStatic: true,
        //     restitution: 1
        // });
        // var ground2 = Bodies.rectangle(400, 0, 800, 60, { isStatic: true });
        // var ground3 = Bodies.rectangle(0, 400, 60, 800, { isStatic: true });
        // var ground4 = Bodies.rectangle(800, 400, 60, 800, { isStatic: true });

        // 壁となるボディを作成する
        var wallOptions = {
            isStatic: true
        };

        var walls = [
            Bodies.rectangle(400, 0, 800, 50, wallOptions),
            Bodies.rectangle(400, 600, 800, 50, wallOptions),
            Bodies.rectangle(0, 300, 50, 600, wallOptions),
            Bodies.rectangle(800, 300, 50, 600, wallOptions)
        ];

        var ball = Bodies.circle(450, 100, 5, {
            restitution: 1.2,
            isStatic: false, // 固定しない
            density: 0.5, // 質量
            friction: 0, // 摩擦
            render: {
                fillStyle: "black"
            }
        });

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
        // Composite.add(engine.world, [boxA, boxB, boxC, boxD]);
        walls.forEach(element => {
            Composite.add(engine.world, element)
        });
        let balls1 = [];
        for (let i = 0; i < 100; i++) {
            balls1[i] = Bodies.circle(0 + i*8, 50, 10, {
                restitution: 0.9,
                isStatic: false, // 固定しない
                density: 0.5, // 質量
                friction: 0, // 摩擦
                render: {
                    fillStyle: "red"
                }
            });
        }
        let balls2 = [];
        for (let i = 0; i < 100; i++) {
            balls2[i] = Bodies.circle(0 + i*8, 40, 10, {
                restitution: 0.9,
                isStatic: false, // 固定しない
                density: 0.5, // 質量
                friction: 0, // 摩擦
                render: {
                    fillStyle: "red"
                }
            });
        }
        let balls3 = [];
        for (let i = 0; i < 100; i++) {
            balls3[i] = Bodies.circle(0 + i*8, 30, 10, {
                restitution: 0.9,
                isStatic: false, // 固定しない
                density: 0.5, // 質量
                friction: 0, // 摩擦
                render: {
                    fillStyle: "red"
                }
            });
        }
        let balls4 = [];
        for (let i = 0; i < 100; i++) {
            balls4[i] = Bodies.circle(0 + i*8, 20, 10, {
                restitution: 0.9,
                isStatic: false, // 固定しない
                density: 0.5, // 質量
                friction: 0, // 摩擦
                render: {
                    fillStyle: "red"
                }
            });
        }
        let balls5 = [];
        for (let i = 0; i < 100; i++) {
            balls5[i] = Bodies.circle(0 + i*8, 10, 10, {
                restitution: 0.9,
                isStatic: false, // 固定しない
                density: 0.5, // 質量
                friction: 0, // 摩擦
                render: {
                    fillStyle: "red"
                }
            });
        }
        Composite.add(engine.world, balls1);
        Composite.add(engine.world, balls2);
        Composite.add(engine.world, balls3);
        Composite.add(engine.world, balls4);
        Composite.add(engine.world, balls5);
        setTimeout(() => {

            Composite.add(engine.world, boxA);
        }, 5000);

        // run the renderer
        Render.run(render);

        // create runner
        var runner = Runner.create();

        // run the engine
        Runner.run(runner, engine);
  })
    return {
        matbox,
    };
  }
  
};
</script>
<style scoped>
</style>
