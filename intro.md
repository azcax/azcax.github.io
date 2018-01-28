#### Summary:

The goal of this tutorial is to give a brief introduction to three.js. I will start by setting up a scene, camera and renderer, so that I can render the scene with camera and a spinning cube.

#### Result
![ͼƬ.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1516862179/did1hjv0vehag0h1pktj.png)


#### What Will I Learn?

- html, css and javascript code structure
- how to set canvas with css
- how to rerfer to three.js library
- how to create a Perspective Camera
- how to create scene
- how to create 3D object
- how to create Material
- how to add 3D object in scene
- how to create renderer
- how to create animation

#### Requirements

- source code editor, for example: vim, notepad++ etc.
- A browser that support webgl, for example: Google Chrome 9+, Firefox 4+, Opera 15+, Safari 5.1+, Internet Explorer 11 and Microsoft Edge etc.

#### Difficulty

- Intermediate

#### Tutorial Contents

- step 1: html, css and javascript code structure
```
<html>
	<head>
		<title>Three js Cube</title>
		<style>
			body { margin: 0; }
			canvas { width: 100%; height: 100% }
		</style>
		<script src="http://threejs.org/build/three.min.js"></script>
	</head>
	<body>
        <script>
        // three js code
        </script>
    </body>
</html>
```
html����ṹ������3D�����Ĵ�����js��䣬���Թؼ������Ƿ���<script>���档���潫��ϸ����ؼ����롣

- step 2: how to set canvas with css

```
canvas { width: 100%; height: 100% }
```

- step 3: how to rerfer to three.js library

```
<script src="http://threejs.org/build/three.min.js"></script>
```

- step 4: how to create a Perspective Camera

```
camera = new THREE.PerspectiveCamera( 70, window.innerWidth / window.innerHeight, 0.01, 10 );
camera.position.z = 1;
```

- step 5: how to create scene

```
scene = new THREE.Scene();
```

- step 6: how to create 3D object

```
geometry = new THREE.BoxGeometry( 0.2, 0.2, 0.2 );
```

- step 7: how to create Material

```
material = new THREE.MeshNormalMaterial();
mesh = new THREE.Mesh( geometry, material );
```

- step 8: how to add 3D object in scene

```
scene.add( mesh );
```

- step 9��how to create renderer

```
renderer = new THREE.WebGLRenderer( { antialias: true } );
renderer.setSize( window.innerWidth, window.innerHeight );
```

- step 10: how to create animation

```
requestAnimationFrame( animate );
mesh.rotation.x += 0.01;
mesh.rotation.y += 0.02;
renderer.render( scene, camera );
```

- full source code��
---
```
<html>
	<head>
		<title>Three js Cube</title>
		<style>
			body { margin: 0; }
			canvas { width: 100%; height: 100% }
		</style>
		<script src="http://threejs.org/build/three.min.js"></script>
	</head>
	<body>
<script>
	var camera, scene, renderer;
	var geometry, material, mesh;

	init();
	animate();

	function init()
	{
		camera = new THREE.PerspectiveCamera( 70, window.innerWidth / window.innerHeight, 0.01, 10 );
		camera.position.z = 1;
		scene = new THREE.Scene();
		geometry = new THREE.BoxGeometry( 0.2, 0.2, 0.2 );
		material = new THREE.MeshNormalMaterial();
		mesh = new THREE.Mesh( geometry, material );
		scene.add( mesh );
		renderer = new THREE.WebGLRenderer( { antialias: true } );
		renderer.setSize( window.innerWidth, window.innerHeight );
		document.body.appendChild( renderer.domElement );
	}
	function animate()
	{
		requestAnimationFrame( animate );
		mesh.rotation.x += 0.01;
		mesh.rotation.y += 0.02;
		renderer.render( scene, camera );
	}
</script>
</body>
</html>
```

---
- verify��

copy&paste above full source code to editor��save it to HTML file��then load it into the browser that supports webgl. Enjoy!

---
# Below is the chinese version

#### ����ѧ��ʲô?

- html,css javascript��������ṹ
- ��ô���û�����С
- ��ô����three.js
- ��ô����͸��ͶӰ�����
- ��ô��������
- ��ô����3D������
- ��ô��������
- ��ô��3D��������ӵ�������
- ��ô������Ⱦ��
- ��ô��������

#### ��Ҫ��׼������

- ����༭��������vim��notepad++��
- ֧��webgl�������������Google Chrome 9+, Firefox 4+, Opera 15+, Safari 5.1+, Internet Explorer 11 and Microsoft Edge��

#### ���׳̶�

- �е�

#### �̳�����
- ����1��html,css javascript��������ṹ�����ڴ���3D�����Ĵ�����javascript��䣬����<script>���档���潫��ϸ����ؼ����롣
```
<html>
	<head>
		<title>Three js Cube</title>
		<style>
			body { margin: 0; }
			canvas { width: 100%; height: 100% }
		</style>
		<script src="http://threejs.org/build/three.min.js"></script>
	</head>
	<body>
	<script>
		// three js code
	</script>
	</body>
</html>
```

- ����2����ô���û�����С

```
canvas { width: 100%; height: 100% }
```

- ����3����ô����three.js

```
<script src="http://threejs.org/build/three.min.js"></script>
```

- ����4����ô����͸��ͶӰ�����

```
camera = new THREE.PerspectiveCamera( 70, window.innerWidth / window.innerHeight, 0.01, 10 );
camera.position.z = 1;
```

- ����5����ô��������

```
scene = new THREE.Scene();
```

- ����6����ô����3D������

```
geometry = new THREE.BoxGeometry( 0.2, 0.2, 0.2 );
```

- ����7����ô��������

```
material = new THREE.MeshNormalMaterial();
mesh = new THREE.Mesh( geometry, material );
```

- ����8����ô��3D��������ӵ�������

```
scene.add( mesh );
```

- ����9����ô������Ⱦ��

```
renderer = new THREE.WebGLRenderer( { antialias: true } );
renderer.setSize( window.innerWidth, window.innerHeight );
```

- ����10����ô��������

```
requestAnimationFrame( animate );
mesh.rotation.x += 0.01;
mesh.rotation.y += 0.02;
renderer.render( scene, camera );
```

- �����������£�
---
```
<html>
	<head>
		<title>Three js Cube</title>
		<style>
			body { margin: 0; }
			canvas { width: 100%; height: 100% }
		</style>
		<script src="http://threejs.org/build/three.min.js"></script>
	</head>
	<body>
<script>
	var camera, scene, renderer;
	var geometry, material, mesh;

	init();
	animate();

	function init()
	{
		camera = new THREE.PerspectiveCamera( 70, window.innerWidth / window.innerHeight, 0.01, 10 );
		camera.position.z = 1;
		scene = new THREE.Scene();
		geometry = new THREE.BoxGeometry( 0.2, 0.2, 0.2 );
		material = new THREE.MeshNormalMaterial();
		mesh = new THREE.Mesh( geometry, material );
		scene.add( mesh );
		renderer = new THREE.WebGLRenderer( { antialias: true } );
		renderer.setSize( window.innerWidth, window.innerHeight );
		document.body.appendChild( renderer.domElement );
	}
	function animate()
	{
		requestAnimationFrame( animate );
		mesh.rotation.x += 0.01;
		mesh.rotation.y += 0.02;
		renderer.render( scene, camera );
	}
</script>
</body>
</html>
```

---
- ��֤��
�����������Ĵ��븴��ճ�����༭���У�����Ϊ��չ��Ϊhtml���ļ���Ȼ����֧��webgl��������д򿪼����Կ�����ת�ķ��顣