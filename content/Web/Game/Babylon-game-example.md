---
title: Babylon 游戏案例
---
# 一个 club

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Babylon.js Simple Cube Game</title>
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
    </style>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babylonjs/5.0.0/babylon.js"></script>
</head>
<body>
    <canvas id="renderCanvas"></canvas>
    <script>
        const canvas = document.getElementById("renderCanvas");
        const engine = new BABYLON.Engine(canvas, true);

        const createScene = function () {
            const scene = new BABYLON.Scene(engine);

            const camera = new BABYLON.ArcRotateCamera("camera", -Math.PI / 2, Math.PI / 2.5, 3, new BABYLON.Vector3(0, 0, 0), scene);
            camera.attachControl(canvas, true);

            const light = new BABYLON.HemisphericLight("light", new BABYLON.Vector3(0, 1, 0), scene);

            const box = BABYLON.MeshBuilder.CreateBox("box", {size: 0.5}, scene);

            scene.registerBeforeRender(function () {
                box.rotation.y += 0.01;
                box.rotation.x += 0.01;
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

# car
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Babylon.js Simple 3D Racing Game</title>
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
    </style>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babylonjs/5.0.0/babylon.js"></script>
</head>
<body>
    <canvas id="renderCanvas"></canvas>
    <script>
        const canvas = document.getElementById("renderCanvas");
        const engine = new BABYLON.Engine(canvas, true);

        const createScene = function () {
            const scene = new BABYLON.Scene(engine);

            // Camera
            const camera = new BABYLON.FollowCamera("followCam", new BABYLON.Vector3(0, 5, -10), scene);
            camera.radius = 10;
            camera.heightOffset = 4;
            camera.rotationOffset = 0;
            camera.cameraAcceleration = 0.05;
            camera.maxCameraSpeed = 10;

            // Light
            const light = new BABYLON.HemisphericLight("light", new BABYLON.Vector3(0, 1, 0), scene);

            // Ground (race track)
            const ground = BABYLON.MeshBuilder.CreateGround("ground", {width: 100, height: 100}, scene);
            const groundMaterial = new BABYLON.StandardMaterial("groundMat", scene);
            groundMaterial.diffuseColor = new BABYLON.Color3(0.5, 0.5, 0.5);
            ground.material = groundMaterial;

            // Car
            const car = BABYLON.MeshBuilder.CreateBox("car", {width: 2, height: 1, depth: 4}, scene);
            car.position.y = 0.5;
            const carMaterial = new BABYLON.StandardMaterial("carMat", scene);
            carMaterial.diffuseColor = new BABYLON.Color3(1, 0, 0);
            car.material = carMaterial;

            camera.lockedTarget = car;

            // Game variables
            let speed = 0;
            const maxSpeed = 0.5;
            const acceleration = 0.001;
            const deceleration = 0.0005;
            let steering = 0;

            // Keyboard events
            const inputMap = {};
            scene.actionManager = new BABYLON.ActionManager(scene);
            scene.actionManager.registerAction(new BABYLON.ExecuteCodeAction(BABYLON.ActionManager.OnKeyDownTrigger, function (evt) {
                inputMap[evt.sourceEvent.key] = evt.sourceEvent.type === "keydown";
            }));
            scene.actionManager.registerAction(new BABYLON.ExecuteCodeAction(BABYLON.ActionManager.OnKeyUpTrigger, function (evt) {
                inputMap[evt.sourceEvent.key] = evt.sourceEvent.type === "keydown";
            }));

            // Game loop
            scene.onBeforeRenderObservable.add(() => {
                if(inputMap["ArrowUp"]) {
                    speed += acceleration;
                } else if(inputMap["ArrowDown"]) {
                    speed -= acceleration;
                } else {
                    if(speed > 0) {
                        speed -= deceleration;
                    } else if(speed < 0) {
                        speed += deceleration;
                    }
                }

                if(speed > maxSpeed) speed = maxSpeed;
                if(speed < -maxSpeed/2) speed = -maxSpeed/2;

                if(inputMap["ArrowLeft"]) {
                    steering -= 0.05;
                } else if(inputMap["ArrowRight"]) {
                    steering += 0.05;
                } else {
                    steering *= 0.9;
                }

                car.rotation.y += steering * speed;
                car.moveWithCollisions(car.forward.scaleInPlace(speed));
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