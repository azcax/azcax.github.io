#### Summary:

In this tutorial, I will show you how to create scene, camera, renderer, axis, cube, plane, grid and light. Let's start...

#### Result
![图片.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1517207213/bm5dfzn9defmngnylgjf.png)


#### What Will I Learn?

- html, css and javascript code structure
- how to set canvas with css
- how to rerfer to three.js library
- how to create scene
- how to create camera
- how to create renderer
- how to create axis
- how to create color
- how to create grid
- how to create cube
- how to create plane
- how to create spot light
- how to append renderer on canvas
- how to render scene with camera

#### Requirements

- source code editor, for example: vim, notepad++ etc.
- A browser that support webgl, for example: Google Chrome 9+, Firefox 4+, Opera 15+, Safari 5.1+, Internet Explorer 11 and Microsoft Edge etc.
- three.js library

#### Difficulty

- Intermediate

#### Tutorial Contents

- html, css and javascript code structure
```
<html>
	<head>
		<title>Three js Line</title>
		<style>
			body { margin: 0; }
			canvas { width: 100%; height: 100% }
		</style>
		<script src="../js/three.min.js"></script>
	</head>
	<body>
<script>
</script>
</body>
</html>
```
- how to set canvas with css

```
canvas { width: 100%; height: 100% }
```

- how to rerfer to three.js library

```
<script src="../js/three.min.js"></script>
```

- how to create scene

```
var scene = new THREE.Scene();
```

- how to create camera

```
var camera = new THREE.PerspectiveCamera(45, window.innerWidth/window.innerHeight, .1, 500)
camera.position.set(40,40,40);
camera.lookAt(scene.position);
```

- how to create renderer

```
var renderer = new THREE.WebGLRenderer();
renderer.setClearColor(0xdddddd);
renderer.setSize(window.innerWidth, window.innerHeight);
renderer.shadowMap.enabled = true;
renderer.shadowMap.type = THREE.PCFSoftShadowMap;
```

- how to create axis

```
var axis = new THREE.AxisHelper(10);
scene.add(axis);
```

- how to create color

```
var color = new THREE.Color("rgb(255, 0, 0)");
```

- how to create grid

```
var grid = new THREE.GridHelper(50,5,color,0x000000);
scene.add(grid);
```

- how to create cube

```
var cubeGeo = new THREE.BoxGeometry(5,5,5);
var cubeMaterial = new THREE.MeshLambertMaterial({color:0xff3300});
var cube = new THREE.Mesh(cubeGeo,cubeMaterial);
cube.position.set(2.5,2.5,2.5);
cube.castShadow = true;
cube.receiveShadow = false;
scene.add(cube);
```

- how to create plane
```
var planeGeo = new THREE.PlaneGeometry(30,30,30);
var planeMaterial = new THREE.MeshLambertMaterial({color:0x00ff00});
var plane = new THREE.Mesh(planeGeo,planeMaterial);
plane.rotation.x = -.5*Math.PI;
plane.receiveShadow = true;
scene.add(plane);
```
- how to create spot light
```
var spotLight = new THREE.SpotLight(0xffffff);
spotLight.position.set(15,30,50);
spotLight.castShadow = true;
scene.add(spotLight);
```
- how to append renderer on canvas
```
document.body.appendChild( renderer.domElement );
```
- how to render scene with camera
```
renderer.render(scene,camera);
```
- full source code
---
```
<html>
	<head>
		<title>Three js Line</title>
		<style>
			body { margin: 0; }
			canvas { width: 100%; height: 100% }
		</style>
		<script src="../js/three.min.js"></script>
	</head>
	<body>
<script>

threejs_axis_plane();
function threejs_axis_plane()
{
	// step1: how to create scene
	var scene = new THREE.Scene();
	
	// step2: how to create camera
	var camera = new THREE.PerspectiveCamera(45, window.innerWidth/window.innerHeight, .1, 500)
	camera.position.set(40,40,40);
	camera.lookAt(scene.position);
	
	// step3: how to create renderer
	var renderer = new THREE.WebGLRenderer();
	renderer.setClearColor(0xdddddd);
	renderer.setSize(window.innerWidth, window.innerHeight);
	renderer.shadowMap.enabled = true;
	renderer.shadowMap.type = THREE.PCFSoftShadowMap;
	
	// step4: how to create axis
	var axis = new THREE.AxisHelper(10);
	scene.add(axis);
	
	// step5: how to create color
	var color = new THREE.Color("rgb(255, 0, 0)");
	
	// step6: how to create grid
	var grid = new THREE.GridHelper(50,5,color,0x000000);
	scene.add(grid);
	
	// step7: how to create cube
	var cubeGeo = new THREE.BoxGeometry(5,5,5);
	var cubeMaterial = new THREE.MeshLambertMaterial({color:0xff3300});
	var cube = new THREE.Mesh(cubeGeo,cubeMaterial);
	cube.position.set(2.5,2.5,2.5);
	cube.castShadow = true;
	cube.receiveShadow = false;
	scene.add(cube);
	
	// step8: how to create plane
	var planeGeo = new THREE.PlaneGeometry(30,30,30);
	var planeMaterial = new THREE.MeshLambertMaterial({color:0x00ff00});
	var plane = new THREE.Mesh(planeGeo,planeMaterial);
	plane.rotation.x = -.5*Math.PI;
	plane.receiveShadow = true;
	scene.add(plane);

	// step9: how to create spot light
	var spotLight = new THREE.SpotLight(0xffffff);
	spotLight.position.set(15,30,50);
	spotLight.castShadow = true;
	scene.add(spotLight);

	// step10: how to append renderer on canvas
	document.body.appendChild( renderer.domElement );
	
	// step11: how to render scene with camera
	renderer.render(scene,camera);
}
</script>
</body>
</html>
```

---
- verify: http://azcax.org/threejs/threejs_axis_plane.html

---
# The Chinese Version

#### 可以学到什么?

- html,css javascript代码整体结构
- 怎么设置画布大小
- 怎么引用three.js
- 怎么创建场景
- 怎么创建相机
- 怎么创建渲染器
- 怎么创建座标轴
- 怎么创建颜色
- 怎么创建网格
- 怎么创建方块
- 怎么创建平面
- 怎么创建点光源
- 怎么将渲染器添加到画布上
- 怎么渲染场景

#### 需要的准备条件

- 代码编辑器，比如vim，notepad++等
- 支持webgl的浏览器，比如Google Chrome 9+, Firefox 4+, Opera 15+, Safari 5.1+, Internet Explorer 11 and Microsoft Edge等
- three.js库

#### 难易程度

- 中等

#### 教程内容
- html,css javascript代码整体结构

  用于创建3D场景的代码是javascript语句，放在```<script>```里面。下面将详细讲解关键代码。
```
<html>
	<head>
		<title>Three js Line</title>
		<style>
			body { margin: 0; }
			canvas { width: 100%; height: 100% }
		</style>
		<script src="../js/three.min.js"></script>
	</head>
	<body>
<script>
</script>
</body>
</html>
```

- 怎么设置画布大小

```
canvas { width: 100%; height: 100% }
```

- 怎么引用three.js

```
<script src="../js/three.min.js"></script>
```

- 怎么创建场景

```
var scene = new THREE.Scene();
```

- 怎么创建相机

```
var camera = new THREE.PerspectiveCamera(45, window.innerWidth/window.innerHeight, .1, 500)
camera.position.set(40,40,40);
camera.lookAt(scene.position);
```

- 怎么创建渲染器

```
var renderer = new THREE.WebGLRenderer();
renderer.setClearColor(0xdddddd);
renderer.setSize(window.innerWidth, window.innerHeight);
renderer.shadowMap.enabled = true;
renderer.shadowMap.type = THREE.PCFSoftShadowMap;
```

- 怎么创建座标轴

```
var axis = new THREE.AxisHelper(10);
scene.add(axis);
```

- 怎么创建颜色

```
var color = new THREE.Color("rgb(255, 0, 0)");
```

- 怎么创建网格

```
var grid = new THREE.GridHelper(50,5,color,0x000000);
scene.add(grid);
```

- 怎么创建方块

```
var cubeGeo = new THREE.BoxGeometry(5,5,5);
var cubeMaterial = new THREE.MeshLambertMaterial({color:0xff3300});
var cube = new THREE.Mesh(cubeGeo,cubeMaterial);
cube.position.set(2.5,2.5,2.5);
cube.castShadow = true;
cube.receiveShadow = false;
scene.add(cube);
```

- 怎么创建平面
```
var planeGeo = new THREE.PlaneGeometry(30,30,30);
var planeMaterial = new THREE.MeshLambertMaterial({color:0x00ff00});
var plane = new THREE.Mesh(planeGeo,planeMaterial);
plane.rotation.x = -.5*Math.PI;
plane.receiveShadow = true;
scene.add(plane);
```
- 怎么创建点光源
```
var spotLight = new THREE.SpotLight(0xffffff);
spotLight.position.set(15,30,50);
spotLight.castShadow = true;
scene.add(spotLight);
```
- 怎么将渲染器添加到画布上
```
document.body.appendChild( renderer.domElement );
```
- 怎么渲染场景
```
renderer.render(scene,camera);
```
- 完整的代码
---
```
<html>
	<head>
		<title>Three js Line</title>
		<style>
			body { margin: 0; }
			canvas { width: 100%; height: 100% }
		</style>
		<script src="../js/three.min.js"></script>
	</head>
	<body>
<script>

threejs_axis_plane();
function threejs_axis_plane()
{
	// step1: how to create scene
	var scene = new THREE.Scene();
	
	// step2: how to create camera
	var camera = new THREE.PerspectiveCamera(45, window.innerWidth/window.innerHeight, .1, 500)
	camera.position.set(40,40,40);
	camera.lookAt(scene.position);
	
	// step3: how to create renderer
	var renderer = new THREE.WebGLRenderer();
	renderer.setClearColor(0xdddddd);
	renderer.setSize(window.innerWidth, window.innerHeight);
	renderer.shadowMap.enabled = true;
	renderer.shadowMap.type = THREE.PCFSoftShadowMap;
	
	// step4: how to create axis
	var axis = new THREE.AxisHelper(10);
	scene.add(axis);
	
	// step5: how to create color
	var color = new THREE.Color("rgb(255, 0, 0)");
	
	// step6: how to create grid
	var grid = new THREE.GridHelper(50,5,color,0x000000);
	scene.add(grid);
	
	// step7: how to create cube
	var cubeGeo = new THREE.BoxGeometry(5,5,5);
	var cubeMaterial = new THREE.MeshLambertMaterial({color:0xff3300});
	var cube = new THREE.Mesh(cubeGeo,cubeMaterial);
	cube.position.set(2.5,2.5,2.5);
	cube.castShadow = true;
	cube.receiveShadow = false;
	scene.add(cube);
	
	// step8: how to create plane
	var planeGeo = new THREE.PlaneGeometry(30,30,30);
	var planeMaterial = new THREE.MeshLambertMaterial({color:0x00ff00});
	var plane = new THREE.Mesh(planeGeo,planeMaterial);
	plane.rotation.x = -.5*Math.PI;
	plane.receiveShadow = true;
	scene.add(plane);

	// step9: how to create spot light
	var spotLight = new THREE.SpotLight(0xffffff);
	spotLight.position.set(15,30,50);
	spotLight.castShadow = true;
	scene.add(spotLight);

	// step10: how to append renderer on canvas
	document.body.appendChild( renderer.domElement );
	
	// step11: how to render scene with camera
	renderer.render(scene,camera);
}
</script>
</body>
</html>
```

---
- 验证: http://azcax.org/threejs/threejs_axis_plane.html