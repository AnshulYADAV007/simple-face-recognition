<template>
  <div class="signup">
    <div class="card">
      <h1>Sign Up</h1>
      <div class="camera">
        <canvas ref="canvas"></canvas>
        <button @click="takePicture">Take Picture</button>
      </div>
      <div class="form">
        <label for="username">Username:</label>
        <input type="text" id="username" v-model="username">
        <button @click="register">Register</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      video: null,
      stream: null
    };
  },
  mounted() {
    const canvas = this.$refs.canvas;
    const context = canvas.getContext('2d');
    navigator.mediaDevices.getUserMedia({ video: true })
      .then((stream) => {
        this.stream = stream
        this.video = document.createElement('video');
        this.video.srcObject = stream;
        this.video.play();
        this.timer = setInterval(() => {
          context.drawImage(this.video, 0, 0, canvas.width, canvas.height);
        }, 100);
      })
      .catch((err) => {
        console.log(err);
      });
  },
  methods: {
    takePicture() {
      clearInterval(this.timer);
      const canvas = this.$refs.canvas;
      const context = canvas.getContext('2d');
      context.drawImage(this.video, 0, 0, canvas.width, canvas.height);
      this.stream.getTracks().forEach(track => {track.stop()})
    },
    register() {
      const canvas = this.$refs.canvas;
      const image = canvas.toDataURL('image/png');
      console.log(image)
      // send image and username to server to complete registration
    },
  },
};
</script>

<style>
.signup {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.card {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 400px;
  height: 500px;
  border: 1px solid black;
  border-radius: 10px;
}

.camera {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 70%;
  margin-bottom: 20px;
}

.camera canvas {
  width: 300px;
  height: 225px;
  border: 1px solid black;
  border-radius: 10px;
}

.form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.form label {
  font-size: 20px;
  margin-bottom: 10px;
}

.form input {
  font-size: 20px;
  margin-bottom: 20px;
  padding: 5px;
}

.form button {
  font-size: 20px;
  padding: 5px 10px;
}
</style>
