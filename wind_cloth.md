#### Summary:

The goal of this tutorial is to give a brief introduction to simulate wind cloth by three.js. I will start by setting up a scene, camera, ligth, and renderer etc, so that I can render the wind cloth simulation.

#### Result:

![ͼƬ.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1517121531/fhxitmu8iltf4o1fxfot.png)

#### What Will I Learn?

- html, css and javascript code structure
- how to refer to three.js and Cloth.js library
- how to create a Perspective Camera
- how to create scene
- how to create light
- how to create cloth
- how to create ground
- how to create poles
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
<html lang="en">
	<head>
		<title>three.js Wind cloth</title>
		<meta charset="utf-8">
		<meta name="viewport" content="width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0">
		<style>
			body {
				font-family: Monospace;
				background-color: #000;
				color: #000;
				margin: 0px;
				overflow: hidden;
			}
		</style>
	</head>

	<body>
		<script src="js/three.min.js"></script>
		<script src="js/Cloth.js"></script>
		<script>
        // three js code
		</script>
	</body>
</html>
```

- step 2: how to rerfer to three.js and Cloth.js library
```
<script src="js/three.min.js"></script>
<script src="js/Cloth.js"></script>
```

- step 3: how to create a Perspective Camera
```
camera = new THREE.PerspectiveCamera( 30, window.innerWidth / window.innerHeight, 1, 10000 );
camera.position.set( 0, 50, 1500 );
```

- step 4: how to create scene
```
scene = new THREE.Scene();
scene.background = new THREE.Color( 0xcce0ff );
scene.fog = new THREE.Fog( 0xcce0ff, 500, 10000 );
```

- step 5: how to create light
```
var light, materials;
var d = 300;
scene.add( new THREE.AmbientLight( 0x666666 ) );
light = new THREE.DirectionalLight( 0xdfebff, 1 );
light.position.set( 50, 200, 100 );
light.position.multiplyScalar( 1.3 );
light.castShadow = true;
light.shadow.mapSize.width = 1024;
light.shadow.mapSize.height = 1024;
light.shadow.camera.left = - d;
light.shadow.camera.right = d;
light.shadow.camera.top = d;
light.shadow.camera.bottom = - d;
light.shadow.camera.far = 1000;
scene.add( light );
```

- step 6: how to create cloth
```
// cloth material
var loader = new THREE.TextureLoader();
var clothTexture = loader.load( 'textures/patterns/circuit_pattern.png' );
clothTexture.anisotropy = 16;
var clothMaterial = new THREE.MeshLambertMaterial( {
map: clothTexture,
side: THREE.DoubleSide,
alphaTest: 0.5
} );

// cloth geometry
clothGeometry = new THREE.ParametricGeometry( clothFunction, cloth.w, cloth.h );
				
// cloth mesh
clothMesh = new THREE.Mesh( clothGeometry, clothMaterial );
clothMesh.position.set( 0, 0, 0 );
clothMesh.castShadow = true;
scene.add( clothMesh );
clothMesh.customDepthMaterial = new THREE.MeshDepthMaterial( {
depthPacking: THREE.RGBADepthPacking,
map: clothTexture,
alphaTest: 0.5
} );
```

- step 7: how to create ground
```
// ground
var groundTexture = loader.load( 'textures/terrain/grasslight-big.jpg' );
groundTexture.wrapS = groundTexture.wrapT = THREE.RepeatWrapping;
groundTexture.repeat.set( 25, 25 );
groundTexture.anisotropy = 16;
var groundMaterial = new THREE.MeshLambertMaterial( { map: groundTexture } );
var mesh = new THREE.Mesh( new THREE.PlaneBufferGeometry( 20000, 20000 ), groundMaterial );
mesh.position.y = - 250;
mesh.rotation.x = - Math.PI / 2;
mesh.receiveShadow = true;
scene.add( mesh );
```

- step 8: how to create poles
```
// poles
var poleGeo = new THREE.BoxBufferGeometry( 5, 375, 5 );
var poleMat = new THREE.MeshLambertMaterial();
var mesh = new THREE.Mesh( poleGeo, poleMat );
mesh.position.x = 125;
mesh.position.y = - 62;
mesh.receiveShadow = true;
mesh.castShadow = true;
scene.add( mesh );

var mesh = new THREE.Mesh( new THREE.BoxBufferGeometry( 255, 5, 5 ), poleMat );
mesh.position.y = - 250 + ( 750 / 2 );
mesh.position.x = 0;
mesh.receiveShadow = true;
mesh.castShadow = true;
scene.add( mesh );

var gg = new THREE.BoxBufferGeometry( 10, 10, 10 );
var mesh = new THREE.Mesh( gg, poleMat );
mesh.position.y = - 250;
mesh.position.x = 125;
mesh.receiveShadow = true;
mesh.castShadow = true;
scene.add( mesh );
```

- step 9: how to create renderer
```
// renderer
renderer = new THREE.WebGLRenderer( { antialias: true } );
renderer.setPixelRatio( window.devicePixelRatio );
renderer.setSize( window.innerWidth, window.innerHeight );
renderer.shadowMap.renderSingleSided = false;
container.appendChild( renderer.domElement );
renderer.gammaInput = true;
renderer.gammaOutput = true;
renderer.shadowMap.enabled = true;
```

- step 10: how to set animation
```
function animate() {
requestAnimationFrame( animate );
var time = Date.now();
var windStrength = Math.cos( time / 7000 ) * 20 + 40;
windForce.set( Math.sin( time / 2000 ), Math.cos( time / 3000 ), Math.sin( time / 1000 ) )
windForce.normalize()
windForce.multiplyScalar( windStrength );
simulate( time );
render();
}
function render() {
var p = cloth.particles;
for ( var i = 0, il = p.length; i < il; i ++ ) {
clothGeometry.vertices[ i ].copy( p[ i ].position );
}
clothGeometry.verticesNeedUpdate = true;
clothGeometry.computeFaceNormals();
clothGeometry.computeVertexNormals();
renderer.render( scene, camera );
}
```

- full source code��
---
```
<html lang="en">
	<head>
		<title>three.js Wind cloth</title>
		<meta charset="utf-8">
		<meta name="viewport" content="width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0">
		<style>
			body {
				font-family: Monospace;
				background-color: #000;
				color: #000;
				margin: 0px;
				overflow: hidden;
			}
		</style>
	</head>

	<body>
		<script src="js/three.min.js"></script>
		<script src="js/Cloth.js"></script>
		<script>

			/* wind cloth */
			var pinsFormation = [];
			var pins = [ 6 ];
			pinsFormation.push( pins );
			pins = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ];
			pinsFormation.push( pins );
			pins = [ 0 ];
			pinsFormation.push( pins );
			pins = []; // cut the rope ;)
			pinsFormation.push( pins );
			pins = [ 0, cloth.w ]; // classic 2 pins
			pinsFormation.push( pins );
			pins = pinsFormation[ 1 ];

			function togglePins() {
				pins = pinsFormation[ ~~ ( Math.random() * pinsFormation.length ) ];
			}
			
			var container;
			var camera, scene, renderer;
			var clothGeometry;
			var sphere;
			var clothMesh;

			init();
			animate();

			function init() {
				container = document.createElement( 'div' );
				document.body.appendChild( container );
				
				// scene
				scene = new THREE.Scene();
				scene.background = new THREE.Color( 0xcce0ff );
				scene.fog = new THREE.Fog( 0xcce0ff, 500, 10000 );

				// camera
				camera = new THREE.PerspectiveCamera( 30, window.innerWidth / window.innerHeight, 1, 10000 );
				camera.position.set( 0, 50, 1500 );

				// lights
				var light, materials;
				var d = 300;
				scene.add( new THREE.AmbientLight( 0x666666 ) );
				light = new THREE.DirectionalLight( 0xdfebff, 1 );
				light.position.set( 50, 200, 100 );
				light.position.multiplyScalar( 1.3 );
				light.castShadow = true;
				light.shadow.mapSize.width = 1024;
				light.shadow.mapSize.height = 1024;
				light.shadow.camera.left = - d;
				light.shadow.camera.right = d;
				light.shadow.camera.top = d;
				light.shadow.camera.bottom = - d;
				light.shadow.camera.far = 1000;
				scene.add( light );

				// cloth material
				var loader = new THREE.TextureLoader();
				var clothTexture = loader.load( 'textures/patterns/circuit_pattern.png' );
				clothTexture.anisotropy = 16;
				var clothMaterial = new THREE.MeshLambertMaterial( {
					map: clothTexture,
					side: THREE.DoubleSide,
					alphaTest: 0.5
				} );

				// cloth geometry
				clothGeometry = new THREE.ParametricGeometry( clothFunction, cloth.w, cloth.h );
				
				// cloth mesh
				clothMesh = new THREE.Mesh( clothGeometry, clothMaterial );
				clothMesh.position.set( 0, 0, 0 );
				clothMesh.castShadow = true;
				scene.add( clothMesh );
				clothMesh.customDepthMaterial = new THREE.MeshDepthMaterial( {
					depthPacking: THREE.RGBADepthPacking,
					map: clothTexture,
					alphaTest: 0.5
				} );

				// ground
				var groundTexture = loader.load( 'textures/terrain/grasslight-big.jpg' );
				groundTexture.wrapS = groundTexture.wrapT = THREE.RepeatWrapping;
				groundTexture.repeat.set( 25, 25 );
				groundTexture.anisotropy = 16;
				var groundMaterial = new THREE.MeshLambertMaterial( { map: groundTexture } );
				var mesh = new THREE.Mesh( new THREE.PlaneBufferGeometry( 20000, 20000 ), groundMaterial );
				mesh.position.y = - 250;
				mesh.rotation.x = - Math.PI / 2;
				mesh.receiveShadow = true;
				scene.add( mesh );

				// poles
				var poleGeo = new THREE.BoxBufferGeometry( 5, 375, 5 );
				var poleMat = new THREE.MeshLambertMaterial();
				var mesh = new THREE.Mesh( poleGeo, poleMat );
				mesh.position.x = 125;
				mesh.position.y = - 62;
				mesh.receiveShadow = true;
				mesh.castShadow = true;
				scene.add( mesh );

				var mesh = new THREE.Mesh( new THREE.BoxBufferGeometry( 255, 5, 5 ), poleMat );
				mesh.position.y = - 250 + ( 750 / 2 );
				mesh.position.x = 0;
				mesh.receiveShadow = true;
				mesh.castShadow = true;
				scene.add( mesh );

				var gg = new THREE.BoxBufferGeometry( 10, 10, 10 );
				var mesh = new THREE.Mesh( gg, poleMat );
				mesh.position.y = - 250;
				mesh.position.x = 125;
				mesh.receiveShadow = true;
				mesh.castShadow = true;
				scene.add( mesh );

				// renderer
				renderer = new THREE.WebGLRenderer( { antialias: true } );
				renderer.setPixelRatio( window.devicePixelRatio );
				renderer.setSize( window.innerWidth, window.innerHeight );
				renderer.shadowMap.renderSingleSided = false;
				container.appendChild( renderer.domElement );
				renderer.gammaInput = true;
				renderer.gammaOutput = true;
				renderer.shadowMap.enabled = true;

				window.addEventListener( 'resize', onWindowResize, false );
				wind = true;
			}

			function onWindowResize() {
				camera.aspect = window.innerWidth / window.innerHeight;
				camera.updateProjectionMatrix();
				renderer.setSize( window.innerWidth, window.innerHeight );
			}

			function animate() {
				requestAnimationFrame( animate );
				var time = Date.now();
				var windStrength = Math.cos( time / 7000 ) * 20 + 40;
				windForce.set( Math.sin( time / 2000 ), Math.cos( time / 3000 ), Math.sin( time / 1000 ) )
				windForce.normalize()
				windForce.multiplyScalar( windStrength );
				simulate( time );
				render();
			}

			function render() {
				var p = cloth.particles;
				for ( var i = 0, il = p.length; i < il; i ++ ) {
					clothGeometry.vertices[ i ].copy( p[ i ].position );
				}
				clothGeometry.verticesNeedUpdate = true;
				clothGeometry.computeFaceNormals();
				clothGeometry.computeVertexNormals();
				renderer.render( scene, camera );
			}

		</script>
	</body>
</html>
```

- verify:
```
git clone 
```

#### Curriculum

- [How to use three.js build 3D scene,camera and a spinning cube | ���ʹ��three.js����3D����������Լ�һ����ת�ķ���](https://steemit.com/utopian-io/@azcax/three-js-3d-or-how-to-use-three-js-build-3d-scene-camera-and-a-spinning-cube)
---
# The Chinese version:
---

#### ����ѧ��ʲô?

- html,css javascript��������ṹ
- ��ô����three.js, Cloth.js
- ��ô����͸��ͶӰ�����
- ��ô��������
- ��ô�����ƹ�
- ��ô��������
- ��ô�������
- ��ô����֧��
- ��ô������Ⱦ��
- ��ô��������

#### ��Ҫ��׼������

- ����༭��������vim��notepad++��
- ֧��webgl�������������Google Chrome 9+, Firefox 4+, Opera 15+, Safari 5.1+, Internet Explorer 11 and Microsoft Edge��

#### ���׳̶�

- �е�

#### �̳�����

- ����1��html,css javascript��������ṹ�����ڴ���3D�����Ĵ�����javascript��䣬����```<script>```���档���潫��ϸ����ؼ����롣
```
<html lang="en">
	<head>
		<title>three.js Wind cloth</title>
		<meta charset="utf-8">
		<meta name="viewport" content="width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0">
		<style>
			body {
				font-family: Monospace;
				background-color: #000;
				color: #000;
				margin: 0px;
				overflow: hidden;
			}
		</style>
	</head>

	<body>
		<script src="js/three.min.js"></script>
		<script src="js/Cloth.js"></script>
		<script>
        // three js code
		</script>
	</body>
</html>
```

- ��ô����three.js, Cloth.js
```
<script src="js/three.min.js"></script>
<script src="js/Cloth.js"></script>
```

- ��ô����͸��ͶӰ�����
```
camera = new THREE.PerspectiveCamera( 30, window.innerWidth / window.innerHeight, 1, 10000 );
camera.position.set( 0, 50, 1500 );
```

- ��ô��������
```
scene = new THREE.Scene();
scene.background = new THREE.Color( 0xcce0ff );
scene.fog = new THREE.Fog( 0xcce0ff, 500, 10000 );
```

- ��ô�����ƹ�
```
var light, materials;
var d = 300;
scene.add( new THREE.AmbientLight( 0x666666 ) );
light = new THREE.DirectionalLight( 0xdfebff, 1 );
light.position.set( 50, 200, 100 );
light.position.multiplyScalar( 1.3 );
light.castShadow = true;
light.shadow.mapSize.width = 1024;
light.shadow.mapSize.height = 1024;
light.shadow.camera.left = - d;
light.shadow.camera.right = d;
light.shadow.camera.top = d;
light.shadow.camera.bottom = - d;
light.shadow.camera.far = 1000;
scene.add( light );
```

- ��ô��������
```
// cloth material
var loader = new THREE.TextureLoader();
var clothTexture = loader.load( 'textures/patterns/circuit_pattern.png' );
clothTexture.anisotropy = 16;
var clothMaterial = new THREE.MeshLambertMaterial( {
map: clothTexture,
side: THREE.DoubleSide,
alphaTest: 0.5
} );

// cloth geometry
clothGeometry = new THREE.ParametricGeometry( clothFunction, cloth.w, cloth.h );
				
// cloth mesh
clothMesh = new THREE.Mesh( clothGeometry, clothMaterial );
clothMesh.position.set( 0, 0, 0 );
clothMesh.castShadow = true;
scene.add( clothMesh );
clothMesh.customDepthMaterial = new THREE.MeshDepthMaterial( {
depthPacking: THREE.RGBADepthPacking,
map: clothTexture,
alphaTest: 0.5
} );
```

- ��ô�������
```
// ground
var groundTexture = loader.load( 'textures/terrain/grasslight-big.jpg' );
groundTexture.wrapS = groundTexture.wrapT = THREE.RepeatWrapping;
groundTexture.repeat.set( 25, 25 );
groundTexture.anisotropy = 16;
var groundMaterial = new THREE.MeshLambertMaterial( { map: groundTexture } );
var mesh = new THREE.Mesh( new THREE.PlaneBufferGeometry( 20000, 20000 ), groundMaterial );
mesh.position.y = - 250;
mesh.rotation.x = - Math.PI / 2;
mesh.receiveShadow = true;
scene.add( mesh );
```

- ��ô����֧��
```
// poles
var poleGeo = new THREE.BoxBufferGeometry( 5, 375, 5 );
var poleMat = new THREE.MeshLambertMaterial();
var mesh = new THREE.Mesh( poleGeo, poleMat );
mesh.position.x = 125;
mesh.position.y = - 62;
mesh.receiveShadow = true;
mesh.castShadow = true;
scene.add( mesh );

var mesh = new THREE.Mesh( new THREE.BoxBufferGeometry( 255, 5, 5 ), poleMat );
mesh.position.y = - 250 + ( 750 / 2 );
mesh.position.x = 0;
mesh.receiveShadow = true;
mesh.castShadow = true;
scene.add( mesh );

var gg = new THREE.BoxBufferGeometry( 10, 10, 10 );
var mesh = new THREE.Mesh( gg, poleMat );
mesh.position.y = - 250;
mesh.position.x = 125;
mesh.receiveShadow = true;
mesh.castShadow = true;
scene.add( mesh );
```

- ��ô������Ⱦ��
```
// renderer
renderer = new THREE.WebGLRenderer( { antialias: true } );
renderer.setPixelRatio( window.devicePixelRatio );
renderer.setSize( window.innerWidth, window.innerHeight );
renderer.shadowMap.renderSingleSided = false;
container.appendChild( renderer.domElement );
renderer.gammaInput = true;
renderer.gammaOutput = true;
renderer.shadowMap.enabled = true;
```

- ��ô��������
```
function animate() {
requestAnimationFrame( animate );
var time = Date.now();
var windStrength = Math.cos( time / 7000 ) * 20 + 40;
windForce.set( Math.sin( time / 2000 ), Math.cos( time / 3000 ), Math.sin( time / 1000 ) )
windForce.normalize()
windForce.multiplyScalar( windStrength );
simulate( time );
render();
}
function render() {
var p = cloth.particles;
for ( var i = 0, il = p.length; i < il; i ++ ) {
clothGeometry.vertices[ i ].copy( p[ i ].position );
}
clothGeometry.verticesNeedUpdate = true;
clothGeometry.computeFaceNormals();
clothGeometry.computeVertexNormals();
renderer.render( scene, camera );
}
```

- full source code��
---
```
<html lang="en">
	<head>
		<title>three.js Wind cloth</title>
		<meta charset="utf-8">
		<meta name="viewport" content="width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0">
		<style>
			body {
				font-family: Monospace;
				background-color: #000;
				color: #000;
				margin: 0px;
				overflow: hidden;
			}
		</style>
	</head>

	<body>
		<script src="js/three.min.js"></script>
		<script src="js/Cloth.js"></script>
		<script>

			/* wind cloth */
			var pinsFormation = [];
			var pins = [ 6 ];
			pinsFormation.push( pins );
			pins = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ];
			pinsFormation.push( pins );
			pins = [ 0 ];
			pinsFormation.push( pins );
			pins = []; // cut the rope ;)
			pinsFormation.push( pins );
			pins = [ 0, cloth.w ]; // classic 2 pins
			pinsFormation.push( pins );
			pins = pinsFormation[ 1 ];

			function togglePins() {
				pins = pinsFormation[ ~~ ( Math.random() * pinsFormation.length ) ];
			}
			
			var container;
			var camera, scene, renderer;
			var clothGeometry;
			var sphere;
			var clothMesh;

			init();
			animate();

			function init() {
				container = document.createElement( 'div' );
				document.body.appendChild( container );
				
				// scene
				scene = new THREE.Scene();
				scene.background = new THREE.Color( 0xcce0ff );
				scene.fog = new THREE.Fog( 0xcce0ff, 500, 10000 );

				// camera
				camera = new THREE.PerspectiveCamera( 30, window.innerWidth / window.innerHeight, 1, 10000 );
				camera.position.set( 0, 50, 1500 );

				// lights
				var light, materials;
				var d = 300;
				scene.add( new THREE.AmbientLight( 0x666666 ) );
				light = new THREE.DirectionalLight( 0xdfebff, 1 );
				light.position.set( 50, 200, 100 );
				light.position.multiplyScalar( 1.3 );
				light.castShadow = true;
				light.shadow.mapSize.width = 1024;
				light.shadow.mapSize.height = 1024;
				light.shadow.camera.left = - d;
				light.shadow.camera.right = d;
				light.shadow.camera.top = d;
				light.shadow.camera.bottom = - d;
				light.shadow.camera.far = 1000;
				scene.add( light );

				// cloth material
				var loader = new THREE.TextureLoader();
				var clothTexture = loader.load( 'textures/patterns/circuit_pattern.png' );
				clothTexture.anisotropy = 16;
				var clothMaterial = new THREE.MeshLambertMaterial( {
					map: clothTexture,
					side: THREE.DoubleSide,
					alphaTest: 0.5
				} );

				// cloth geometry
				clothGeometry = new THREE.ParametricGeometry( clothFunction, cloth.w, cloth.h );
				
				// cloth mesh
				clothMesh = new THREE.Mesh( clothGeometry, clothMaterial );
				clothMesh.position.set( 0, 0, 0 );
				clothMesh.castShadow = true;
				scene.add( clothMesh );
				clothMesh.customDepthMaterial = new THREE.MeshDepthMaterial( {
					depthPacking: THREE.RGBADepthPacking,
					map: clothTexture,
					alphaTest: 0.5
				} );

				// ground
				var groundTexture = loader.load( 'textures/terrain/grasslight-big.jpg' );
				groundTexture.wrapS = groundTexture.wrapT = THREE.RepeatWrapping;
				groundTexture.repeat.set( 25, 25 );
				groundTexture.anisotropy = 16;
				var groundMaterial = new THREE.MeshLambertMaterial( { map: groundTexture } );
				var mesh = new THREE.Mesh( new THREE.PlaneBufferGeometry( 20000, 20000 ), groundMaterial );
				mesh.position.y = - 250;
				mesh.rotation.x = - Math.PI / 2;
				mesh.receiveShadow = true;
				scene.add( mesh );

				// poles
				var poleGeo = new THREE.BoxBufferGeometry( 5, 375, 5 );
				var poleMat = new THREE.MeshLambertMaterial();
				var mesh = new THREE.Mesh( poleGeo, poleMat );
				mesh.position.x = 125;
				mesh.position.y = - 62;
				mesh.receiveShadow = true;
				mesh.castShadow = true;
				scene.add( mesh );

				var mesh = new THREE.Mesh( new THREE.BoxBufferGeometry( 255, 5, 5 ), poleMat );
				mesh.position.y = - 250 + ( 750 / 2 );
				mesh.position.x = 0;
				mesh.receiveShadow = true;
				mesh.castShadow = true;
				scene.add( mesh );

				var gg = new THREE.BoxBufferGeometry( 10, 10, 10 );
				var mesh = new THREE.Mesh( gg, poleMat );
				mesh.position.y = - 250;
				mesh.position.x = 125;
				mesh.receiveShadow = true;
				mesh.castShadow = true;
				scene.add( mesh );

				// renderer
				renderer = new THREE.WebGLRenderer( { antialias: true } );
				renderer.setPixelRatio( window.devicePixelRatio );
				renderer.setSize( window.innerWidth, window.innerHeight );
				renderer.shadowMap.renderSingleSided = false;
				container.appendChild( renderer.domElement );
				renderer.gammaInput = true;
				renderer.gammaOutput = true;
				renderer.shadowMap.enabled = true;

				window.addEventListener( 'resize', onWindowResize, false );
				wind = true;
			}

			function onWindowResize() {
				camera.aspect = window.innerWidth / window.innerHeight;
				camera.updateProjectionMatrix();
				renderer.setSize( window.innerWidth, window.innerHeight );
			}

			function animate() {
				requestAnimationFrame( animate );
				var time = Date.now();
				var windStrength = Math.cos( time / 7000 ) * 20 + 40;
				windForce.set( Math.sin( time / 2000 ), Math.cos( time / 3000 ), Math.sin( time / 1000 ) )
				windForce.normalize()
				windForce.multiplyScalar( windStrength );
				simulate( time );
				render();
			}

			function render() {
				var p = cloth.particles;
				for ( var i = 0, il = p.length; i < il; i ++ ) {
					clothGeometry.vertices[ i ].copy( p[ i ].position );
				}
				clothGeometry.verticesNeedUpdate = true;
				clothGeometry.computeFaceNormals();
				clothGeometry.computeVertexNormals();
				renderer.render( scene, camera );
			}

		</script>
	</body>
</html>
```

- ��֤:
```
git clone 
```

#### �̳��б�

- [How to use three.js build 3D scene,camera and a spinning cube | ���ʹ��three.js����3D����������Լ�һ����ת�ķ���](https://steemit.com/utopian-io/@azcax/three-js-3d-or-how-to-use-three-js-build-3d-scene-camera-and-a-spinning-cube)
    