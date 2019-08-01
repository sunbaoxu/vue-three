<template>
  <div class="hello">
    
  </div>
</template>

<script>
var THREE   = require('three');

let SEPARATION = 100,
  AMOUNTX = 100,
  AMOUNTY = 70;

let container;
let camera, scene, renderer;

let particles,
  particle,
  count = 0;

let mouseX = 85,
  mouseY = -342;

let windowHalfX = window.innerWidth / 2;
let windowHalfY = window.innerHeight / 2;
export default {
  data() {
    return {
    };
  },
  methods: {
    init() {
      container = document.createElement("div");
      document.body.appendChild(container);
      camera = new THREE.PerspectiveCamera(
        120,
        window.innerWidth / window.innerHeight,
        1,
        10000
      );
      container.style.cssText = "position:fixed;top:0;left:0;cursor:pointer;opacity:0.9;z-index:10000";
      camera.position.z = 1000;

      scene =new THREE.Scene();

      //创建THREE.PointCloud粒子的容器
        var geometry = new THREE.Geometry();
        //创建THREE.PointCloud纹理
        var material = new THREE.PointCloudMaterial({size:4, vertexColors:true, color:0xffffff});

        //循环将粒子的颜色和位置添加到网格当中
        for (var x = -5; x <= 5; x++) {
            for (var y = -5; y <= 5; y++) {
                var particle = new THREE.Vector3(x * 10, y * 10, 0);
                geometry.vertices.push(particle);
                // geometry.colors.push(new THREE.Color());
            }
        }

        //实例化THREE.PointCloud
        var cloud = new THREE.PointCloud(geometry, material);
        scene.add(cloud);

      // renderer =new THREE.CanvasRenderer();
      // renderer.setSize(window.innerWidth, window.innerHeight);
      // container.appendChild(renderer.domElement);

      document.addEventListener("mousemove", this.onDocumentMouseMove, false);
      document.addEventListener("touchstart", this.onDocumentTouchStart, false);
      document.addEventListener("touchmove",this. onDocumentTouchMove, false);

      //

      window.addEventListener("resize", this.onWindowResize, false);
    },
    onWindowResize() {
      windowHalfX = window.innerWidth / 2;
      windowHalfY = window.innerHeight / 2;

      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();

      renderer.setSize(window.innerWidth, window.innerHeight);
    },
    onDocumentMouseMove(event) {
      mouseX = event.clientX - windowHalfX;
      mouseY = event.clientY - windowHalfY;
    },
    onDocumentTouchStart(event) {
      if (event.touches.length === 1) {
        event.preventDefault();

        mouseX = event.touches[0].pageX - windowHalfX;
        mouseY = event.touches[0].pageY - windowHalfY;
      }
    },
    onDocumentTouchMove(event) {
      if (event.touches.length === 1) {
        event.preventDefault();

        mouseX = event.touches[0].pageX - windowHalfX;
        mouseY = event.touches[0].pageY - windowHalfY;
      }
    },
    animate() {
      requestAnimationFrame(this.animate);

      this.render();
    },
    render() {
      camera.position.x += (mouseX - camera.position.x) * 0.05;
      camera.position.y += (-mouseY - camera.position.y) * 0.05;
      camera.lookAt(scene.position);

      var i = 0;

      for (var ix = 0; ix < AMOUNTX; ix++) {
        for (var iy = 0; iy < AMOUNTY; iy++) {
          particle = particles[i++];
          particle.position.y =
            Math.sin((ix + count) * 0.3) * 50 +
            Math.sin((iy + count) * 0.5) * 50;
          particle.scale.x = particle.scale.y =
            (Math.sin((ix + count) * 0.3) + 1) * 2 +
            (Math.sin((iy + count) * 0.5) + 1) * 2;
        }
      }

      renderer.render(scene, camera);

      count += 0.1;
    }
  },
  mounted() {
    // this.getImgCode();
    // this.init()
    // this.animate()
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
