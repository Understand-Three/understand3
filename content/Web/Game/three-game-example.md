---
title: threejs 游戏案例
---
# club

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Simple Three.js Example</title>
  <style>
    body {
      margin: 0;
    }

    canvas {
      display: block;
    }
  </style>
</head>

<body>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <script>
    // 创建场景、相机和渲染器
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
    const renderer = new THREE.WebGLRenderer();

    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);

    // 创建一个立方体
    const geometry = new THREE.BoxGeometry();
    const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
    const cube = new THREE.Mesh(geometry, material);
    scene.add(cube);

    camera.position.z = 5;

    // 动画循环
    function animate () {
      requestAnimationFrame(animate);

      cube.rotation.x += 0.01;
      cube.rotation.y += 0.01;

      renderer.render(scene, camera);
    }

    animate();

    // 窗口大小调整
    window.addEventListener('resize', onWindowResize, false);

    function onWindowResize () {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    }
  </script>
</body>

</html>
```


# RPG
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Babylon.js Simple RPG Game</title>
    <style>
        html, body {
            overflow: hidden;
            width: 100%;
            height: 100%;
            margin: 0;
            padding: 0;
        }
        #renderCanvas {
            width: 100%;
            height: 100%;
            touch-action: none;
        }
        #ui {
            position: absolute;
            top: 10px;
            left: 10px;
            color: white;
            font-family: Arial, sans-serif;
        }
    </style>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babylonjs/5.0.0/babylon.js"></script>
</head>
<body>
    <canvas id="renderCanvas"></canvas>
    <div id="ui">
        <div id="healthBar">Health: <span id="healthValue">100</span></div>
        <div id="dialogBox" style="display: none;"></div>
    </div>
    <script>
        const canvas = document.getElementById("renderCanvas");
        const engine = new BABYLON.Engine(canvas, true);

        const createScene = function () {
            const scene = new BABYLON.Scene(engine);

            // Camera
            const camera = new BABYLON.FollowCamera("camera", new BABYLON.Vector3(0, 5, -10), scene);
            camera.radius = 10;
            camera.heightOffset = 4;
            camera.rotationOffset = 0;
            camera.cameraAcceleration = 0.05;
            camera.maxCameraSpeed = 10;

            // Light
            const light = new BABYLON.HemisphericLight("light", new BABYLON.Vector3(0, 1, 0), scene);

            // Ground
            const ground = BABYLON.MeshBuilder.CreateGround("ground", {width: 100, height: 100}, scene);
            const groundMaterial = new BABYLON.StandardMaterial("groundMat", scene);
            groundMaterial.diffuseColor = new BABYLON.Color3(0.2, 0.6, 0.2);
            ground.material = groundMaterial;

            // Player
            const player = BABYLON.MeshBuilder.CreateBox("player", {width: 1, height: 2, depth: 1}, scene);
            player.position.y = 1;
            const playerMaterial = new BABYLON.StandardMaterial("playerMat", scene);
            playerMaterial.diffuseColor = new BABYLON.Color3(0, 0, 1);
            player.material = playerMaterial;

            camera.lockedTarget = player;

            // NPCs
            const createNPC = function(name, position, color) {
                const npc = BABYLON.MeshBuilder.CreateBox(name, {width: 1, height: 2, depth: 1}, scene);
                npc.position = position;
                const npcMaterial = new BABYLON.StandardMaterial(name + "Mat", scene);
                npcMaterial.diffuseColor = color;
                npc.material = npcMaterial;
                return npc;
            };

            const npc1 = createNPC("npc1", new BABYLON.Vector3(5, 1, 5), new BABYLON.Color3(1, 0, 0));
            const npc2 = createNPC("npc2", new BABYLON.Vector3(-5, 1, -5), new BABYLON.Color3(0, 1, 0));

            // Game variables
            let playerHealth = 100;
            let isInteracting = false;

            // Keyboard events
            const inputMap = {};
            scene.actionManager = new BABYLON.ActionManager(scene);
            scene.actionManager.registerAction(new BABYLON.ExecuteCodeAction(BABYLON.ActionManager.OnKeyDownTrigger, function (evt) {
                inputMap[evt.sourceEvent.key] = evt.sourceEvent.type === "keydown";
            }));
            scene.actionManager.registerAction(new BABYLON.ExecuteCodeAction(BABYLON.ActionManager.OnKeyUpTrigger, function (evt) {
                inputMap[evt.sourceEvent.key] = evt.sourceEvent.type === "keydown";
            }));

            // Interaction
            const interact = function(npc) {
                if (isInteracting) return;
                isInteracting = true;
                const dialogBox = document.getElementById("dialogBox");
                dialogBox.style.display = "block";
                dialogBox.textContent = `Hello, I'm ${npc.name}!`;
                setTimeout(() => {
                    dialogBox.style.display = "none";
                    isInteracting = false;
                }, 3000);
            };

            // Game loop
            scene.onBeforeRenderObservable.add(() => {
                let playerSpeed = 0.1;
                if(inputMap["w"] || inputMap["ArrowUp"]) {
                    player.moveWithCollisions(player.forward.scaleInPlace(playerSpeed));
                }
                if(inputMap["s"] || inputMap["ArrowDown"]) {
                    player.moveWithCollisions(player.forward.scaleInPlace(-playerSpeed));
                }
                if(inputMap["a"] || inputMap["ArrowLeft"]) {
                    player.rotation.y -= 0.05;
                }
                if(inputMap["d"] || inputMap["ArrowRight"]) {
                    player.rotation.y += 0.05;
                }
                if(inputMap["e"]) {
                    if (player.intersectsMesh(npc1, true)) {
                        interact(npc1);
                    } else if (player.intersectsMesh(npc2, true)) {
                        interact(npc2);
                    }
                }

                // Update health bar
                document.getElementById("healthValue").textContent = playerHealth;
            });

            return scene;
        };

        const scene = createScene();

        engine.runRenderLoop(function () {
            scene.render();
        });

        window.addEventListener("resize", function () {
            engine.resize();
        });
    </script>
</body>
</html>
```