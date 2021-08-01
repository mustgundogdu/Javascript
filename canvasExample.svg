<svg width="100" height="100" xmlns="http://www.w3.org/2000/svg">
<html>
<head><title>CANVAS EXAMPLE</title></head>
<body>
  <canvas id="scene" width="324" height="323"></canvas>
<style>
	body {
  		display: flex;
  		margin: 0;
  		align-items: center;
  		justify-content: center;
  		height: 100vh;
	}
	canvas {
  		width:98vmin;
  		height:98vmin;
	}
	
</style>
<script>
	console.clear();
	const canvas = document.querySelector('#scene');
	canvas.width = canvas.clientWidth;
	canvas.height = canvas.clientHeight;
	// 2D Context
	const ctx = canvas.getContext('2d');

	//genislik ve yukseklik
	if (window.devicePixelRatio > 1) {
  		canvas.width = canvas.clientWidth * 2;
  		canvas.height = canvas.clientHeight * 2;
  		ctx.scale(2, 2);
		}

	let width = canvas.clientWidth; // canvas genislik
	let height = canvas.clientHeight; // canvas yukseklik
	let rotation = 0; // kure rotasyon
	let dots = []; // nokta dizileri

	const DOTS_AMOUNT = 1000; // nokta miktari
	const DOT_RADIUS = 4; // nokta yaricapi
	let GLOBE_RADIUS = width * 0.7; // kure yaricapi
	let GLOBE_CENTER_Z = -GLOBE_RADIUS; // merkez kure z degeri
	let PROJECTION_CENTER_X = width / 2; // merkez canvas x degeri
	let PROJECTION_CENTER_Y = height / 2; // merkez canvas y degeri
	let FIELD_OF_VIEW = width * 0.8;

	//Dot sinifi
	class Dot 
	{
	//kurucu fonksiyon  
	constructor(x, y, z) {
    		this.x = x;
    		this.y = y;
    		this.z = z;
    
    		this.xProject = 0;
    		this.yProject = 0;
    		this.sizeProjection = 0;
 	 }
  	// 2D canvas hesaplamalari 
  		project(sin, cos) {
    			const rotX = cos * this.x + sin * (this.z - GLOBE_CENTER_Z); 
    			const rotZ = -sin * this.x + cos * (this.z - GLOBE_CENTER_Z) + GLOBE_CENTER_Z;
    			this.sizeProjection = FIELD_OF_VIEW / (FIELD_OF_VIEW - rotZ);
    			this.xProject = (rotX * this.sizeProjection) + PROJECTION_CENTER_X;
    			this.yProject = (this.y * this.sizeProjection) + PROJECTION_CENTER_Y;
  		}
  	// canvas cizimi
  	draw(sin, cos) {
	  //project fonksiyon cagrimi
    		this.project(sin, cos);
    		ctx.beginPath();
    		ctx.arc(this.xProject, this.yProject, DOT_RADIUS * this.sizeProjection, 0, Math.PI * 2);
    		ctx.closePath();
    		ctx.fill();
  		}
	}

	function createDots() {
  	// dots dizisi uzunluk sifirla
  	dots.length = 0;
  
  	// miktara gore nokta olusturma
  	for (let i = 0; i < DOTS_AMOUNT; i++) {
    		const theta = Math.random() * 2 * Math.PI; // rastgele 0 ile 2 pi arası deger uretme (pi degeri hesaplamak icin PI fonksiyonu kullanildi)
    		const phi = Math.acos((Math.random() * 2) - 1); // rastgele 1 ile -1 arasi deger uretme
    
    	// x y z kordinatlari hesapla ve Dot sinifina parametre degeri gonder
    		const x = GLOBE_RADIUS * Math.sin(phi) * Math.cos(theta);
    		const y = GLOBE_RADIUS * Math.sin(phi) * Math.sin(theta);
    		const z = (GLOBE_RADIUS * Math.cos(phi)) + GLOBE_CENTER_Z;
    		dots.push(new Dot(x, y, z));
  		}
	}


	function render(a) {
  	// Ekrani temizle
  	ctx.clearRect(0, 0, width, height);
  
  	// Kure rotasyonu artır
  	rotation = a * 0.0004;
  
  		const sineRotation = Math.sin(rotation); // Sinus rotasyonu
  		const cosineRotation = Math.cos(rotation); // Kosinus rotasyonu 
  
  	// dots dizisine rotasyon hesaplamalari ve ekleme
  	for (var i = 0; i < dots.length; i++) {
    		dots[i].draw(sineRotation, cosineRotation);
  	}
  
  		window.requestAnimationFrame(render);
	}


	// ekrani boyutlandirma
	function afterResize () {
	
  		width = canvas.offsetWidth;
  		height = canvas.offsetHeight;
  	if (window.devicePixelRatio > 1) {
    		canvas.width = canvas.clientWidth * 2;
    		canvas.height = canvas.clientHeight * 2;
    		ctx.scale(2, 2);
  	} else {
    		canvas.width = width;
    		canvas.height = height;
  	}
  		GLOBE_RADIUS = width * 0.7;
  		GLOBE_CENTER_Z = -GLOBE_RADIUS;
 		PROJECTION_CENTER_X = width / 2;
  		PROJECTION_CENTER_Y = height / 2;
  		FIELD_OF_VIEW = width * 0.8;
  
  		createDots(); // yeni noktalarla sifirlama
	}

	let resizeTimeout;

	function onResize () {
  	// timeout degiskenini temizle
  		resizeTimeout = window.clearTimeout(resizeTimeout);
  		resizeTimeout = window.setTimeout(afterResize, 500);
	}
	window.addEventListener('resize', onResize);

	createDots();

	window.requestAnimationFrame(render);

</script>
  </body>
</html>
