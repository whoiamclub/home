---
title: threejs基础
date: 2017-06-30 10:07:16
tags: [webGL,javascript]
categories: 前端
---

Threejs中3个基础元素是场景（scene）、相机（camera）和渲染器（renderer）。

<!-- more -->

#### 1.场景
场景是所有物体的容器，用THREE.Scene来表示。

构件一个场景

    var scene = new THREE.Scene();
#### 2.相机
相机决定了场景中第一视角的位置。
相机的种类：
透视相机（THREE.PerspectiveCamera）

    var camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 0.1, 1000);
#### 3.渲染器
 渲染器决定了渲染的结果应该画在页面的什么元素上面，并且以怎样的方式来绘制。
 
    var renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);
#### 4.添加物体到场景中
    
    /*创建一个物体*/
    var geometry = new THREE.CubeGeometry(1,1,1); 
    var material = new THREE.MeshBasicMaterial({color: 0x00ff00});
    /*为物体添加细节*/
    var cube = new THREE.Mesh(geometry, material);
    /*将物体添加到场景中*/
    scene.add(cube);
#### 5.渲染
    
    /*使用渲染器，结合相机和场景*/
    renderer.render(scene, camera);
    /*渲染函数的原型*/
    render( scene, camera, renderTarget, forceClear )
    /*
    scene：前面定义的场景
    camera：前面定义的相机
    renderTarget：渲染的目标，默认是渲染到前面定义的render变量中
    forceClear：每次绘制之前都将画布的内容给清除，即使自动清除标志autoClear为false，也会清除。
    */
#### 6.渲染循环
     
渲染有两种方式：实时渲染和离线渲染 。

    /*实时渲染（游戏循环）*/
    function render() {
        cube.rotation.x += 0.1;
        cube.rotation.y += 0.1;
        renderer.render(scene, camera);
        requestAnimationFrame(render);
    }

``` bash
<!DOCTYPE html>
<html>
<head>
    <title></title>
    <style>canvas { width: 100%; height: 100% }</style>
    <script src="js/three.js"></script>
</head>
<body>
    <script>
        var scene = new THREE.Scene();
        
        var camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 0.1, 1000);
        
        var renderer = new THREE.WebGLRenderer();
        
        renderer.setSize(window.innerWidth, window.innerHeight);
        
        document.body.appendChild(renderer.domElement);
        var geometry = new THREE.CubeGeometry(1,1,1);
        var material = new THREE.MeshBasicMaterial({color: 0x00ff00});
        var cube = new THREE.Mesh(geometry, material); 
        scene.add(cube);
        camera.position.z = 5;
        function render() {
            requestAnimationFrame(render);
            cube.rotation.x += 0.1;
            cube.rotation.y += 0.1;
            renderer.render(scene, camera);
        }
        render();
    </script>
</body>
</html>
```