<template>
  <section class="home" ref="homeWrap">

  </section>
</template>

<script>
import * as THREE from 'three';
export default {
  data (){
    return {
      cube :null,
      scene :null,
      camera :null,
      renderer :null
    }
  },
  methods :{
    init() {
      this.scene = new THREE.Scene();
      
      //摄像机 
      this.camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );
      //渲染器
      this.renderer = new THREE.WebGLRenderer();
      //渲染器大小
      this.renderer.setSize( window.innerWidth /2, window.innerHeight /2);

      //立方体
      var geometry = new THREE.BoxGeometry( 1, 1, 1 );
      //颜色
      var material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
      //网格
      this.cube = new THREE.Mesh( geometry, material );
      this.scene.add( this.cube );
      
      this.camera.position.z = 2;
      

      this.$refs.homeWrap.appendChild( this.renderer.domElement );
      //动画
      this.animate();

    },
    //动画
    animate() {
      requestAnimationFrame( this.animate );
      this.cube.rotation.x += 0.01;
      this.cube.rotation.y += 0.01;

      this.renderer.render( this.scene, this.camera );
    }
  },
  mounted (){
    this.init()
  }
}
</script>
<style lang="scss">
.home{
  padding-top: 50px;
}
</style>

