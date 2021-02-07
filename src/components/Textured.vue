<template>
  <div>
    <video id="video" src="./texture/video.mp4"></video>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  mounted() {
    let scene, camera, renderer, cube1, cube2, cube3;
    function Init() {
      scene = new THREE.Scene();
      camera = new THREE.PerspectiveCamera(
        75,
        window.innerWidth / window.innerHeight,
        0.1,
        1000
      );

      renderer = new THREE.WebGLRenderer({ antialias: true });

      renderer.setSize(window.innerWidth, window.innerHeight);
      document.body.appendChild(renderer.domElement);

      /*const controls = new OrbitControls(camera, renderer.domElement);
      camera.position.set(0, 20, 100);
      controls.update();*/

      const geometry = new THREE.BoxGeometry(2, 2, 2);
      const material1 = new THREE.MeshBasicMaterial({ color: 0x0000fff }); ///Renk veriyor
      const material2 = new THREE.MeshBasicMaterial({ color: 0x00fffff }); ///Renk veriyor
      const material3 = new THREE.MeshBasicMaterial({ color: 0x0088888 }); ///Renk veriyor
      /*const video = document.getElementById("video");
      const texture = new THREE.VideoTexture(video);
      const material = new THREE.MeshBasicMaterial({ map: texture });*/
      cube1 = new THREE.Mesh(geometry, material1);
      cube2 = new THREE.Mesh(geometry, material2);
      cube3 = new THREE.Mesh(geometry, material3);
      cube1.position.x = 5;
      cube2.position.x = -5;
      scene.add(cube1);
      scene.add(cube2);
      scene.add(cube3);

      camera.position.z = 10;
    }

    function animate() {
      requestAnimationFrame(animate);
      cube1.rotation.x += 0.01;
      cube2.rotation.y += 0.01;
      cube3.rotation.z += 0.01;
      //controls.update();
      renderer.render(scene, camera);
    }

    function onWindowResize() {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    }

    window.addEventListener("resize", onWindowResize, false);

    Init();
    animate();
  },
  methods: {},
};
</script>

<style scoped>
body {
  margin: 0;
}

canvas {
  width: 100%;
  height: 100%;
}

#video {
  display: none;
}
</style>