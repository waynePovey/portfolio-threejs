<template>
  <div id="container"></div>
</template>

<script>
import * as THREE from 'three';

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      camera: null,
      scene: null,
      renderer: null,
      mesh: null
    }
  },
  methods: {
    init: function() {
      let container = document.getElementById('container');
      this.scene = new THREE.Scene();

      this.camera = new THREE.PerspectiveCamera(70, container.clientWidth/container.clientHeight, 0.01, 10);
      this.camera.position.z = 5;


      let geometry = new THREE.BoxGeometry(2, 2, 2);
      let material = new THREE.MeshBasicMaterial();

      this.mesh = new THREE.Mesh(geometry, material);
      this.scene.add(this.mesh);

      this.renderer = new THREE.WebGLRenderer({antialias: true});
      this.renderer.setSize(container.clientWidth, container.clientHeight);
      container.appendChild(this.renderer.domElement);
    },
    animate: function() {
      requestAnimationFrame(this.animate);
        this.mesh.rotation.x += 0.01;
        this.mesh.rotation.y += 0.02;
        this.renderer.render(this.scene, this.camera);
    }
  },
  mounted() {
    this.init();
    this.animate();
  }
}

</script>

<style scoped lang="scss">
  #container {
      position: absolute;
      height: 100%;
      width: 100%;
      
  }
    
  canvas {
    width: 100%;
    height: 100%;
  }  
</style>
