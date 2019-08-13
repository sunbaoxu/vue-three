<template>
  <section class="home" ref="homeWrap">

  </section>
</template>

<script>
import * as THREE from 'three';
import {WEBGL} from '../lib/webGl';

export default {
  data (){
    return {
      line :null,
      scene :null,
      camera :null,
      renderer :null
    }
  },
  methods :{
    init() {
      this.scene = new THREE.Scene();
      
      //摄像机 
      // this.camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );
      this.camera = new THREE.PerspectiveCamera( 45, window.innerWidth / window.innerHeight, 1, 500 );
      this.camera.position.set( 0, 0, 100 );
      this.camera.lookAt( 0, 0, 0 );
      //渲染器
      this.renderer = new THREE.WebGLRenderer();
      //渲染器大小
      this.renderer.setSize( window.innerWidth /2, window.innerHeight /2);

      //立方体
      // var geometry = new THREE.BoxGeometry( 1, 1, 1 );
      var geometry = new THREE.Geometry();
      geometry.vertices.push(new THREE.Vector3( -10, 0, 0) );
      geometry.vertices.push(new THREE.Vector3( 0, 10, 0) );
      geometry.vertices.push(new THREE.Vector3( 10, 0, 0) );
      geometry.vertices.push(new THREE.Vector3( 10, 0, 0) );
      //颜色
      var material = new THREE.LineBasicMaterial( { color: 0x0000ff } );
      //网格
      // this.cube = new THREE.Mesh( geometry, material );
      this.line = new THREE.Line( geometry, material );
      this.scene.add( this.line );
      this.renderer.render( this.scene, this.camera );

      
      // this.camera.position.z = 2;
      

      //是否可以使用webgl2
      if ( WEBGL.isWebGL2Available() === false ) {
        this.$refs.homeWrap.appendChild( WEBGL.getWebGL2ErrorMessage() );
      } else{
        this.$refs.homeWrap.appendChild( this.renderer.domElement );
      }
      //动画
      // this.animate();

    },
    //动画
    animate() {
      requestAnimationFrame( this.animate );
      // this.cube.rotation.x += 0.01;
      // this.cube.rotation.y += 0.01;

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

