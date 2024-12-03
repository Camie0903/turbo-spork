<template>
  <div style="background-color: #8BC6EC;
background-image: linear-gradient(135deg, #8BC6EC 0%, #9599E2 100%);
" :class="['floating', { paused: isPaused }]">
    <h2>Portfolio Coming Soon</h2>
    <p>Hi there! I'm currently building my portfolio. Stay tuned for something amazing!!</p>
    <!-- <form @submit.prevent="subscribe" class="subscribe-form">
      <input
        v-model="email"
        type="email"
        placeholder="Enter your email"
        required
        @focus="pauseAnimation"
        @blur="resumeAnimation"
      />
      <button type="submit">Notify Me</button>
    </form> -->
    <p v-if="message" class="message">{{ message }}</p>
    <footer>
      <p style="color: #2c3e50;">&copy; 2024 Cameron Tamboer. All rights reserved.</p>
    </footer>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const email = ref("");
    const message = ref("");
    const isPaused = ref(false); // Reactive variable to control the animation

    const subscribe = () => {
      if (email.value) {
        message.value = `Thanks for subscribing, ${email.value}!`;
        email.value = "";
        resumeAnimation(); // Resume animation when the button is clicked
      } else {
        message.value = "Please enter a valid email address.";
      }
    };

    const pauseAnimation = () => {
      isPaused.value = true;
    };

    const resumeAnimation = () => {
      isPaused.value = false;
    };

    return { email, message, subscribe, isPaused, pauseAnimation, resumeAnimation };
  },
};
</script>

<style scoped>
/* Force background to apply directly to body */
body {
  background-color: #8BC6EC !important;
  background-image: linear-gradient(135deg, #8BC6EC 0%, #9599E2 100%) !important;
  color: #ffffff;
}

/* Floating div animation */
.floating {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 300px;
  padding: 20px;
  background-color: rgba(255, 255, 255, 0.1);
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  animation: float 37s ease-in-out infinite;
}

.floating.paused {
  animation-play-state: paused;
}

/* Keyframes for the floating animation */
@keyframes float {
  0% {
    top: 50%;
    left: 50%;
  }
  25% {
    top: 30%;
    left: 30%;
  }
  50% {
    top: 70%;
    left: 70%;
  }
  75% {
    top: 30%;
    left: 90%;
  }
  100% {
    top: 50%;
    left: 50%;
  }
}

/* Form and input styles */
.subscribe-form {
  display: flex;
  gap: 10px;
  justify-content: center;
}

input[type="email"] {
  padding: 0.5rem;
  border: none;
  border-radius: 5px;
  outline: none;
}

button {
  padding: 0.5rem 1rem;
  background: #ffffff;
  color: #f50057;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background: #f5a623;
  color: #ffffff;
}

/* Message styles */
.message {
  margin-top: 1rem;
  font-weight: bold;
}

/* Footer styles */
footer {
  margin-top: 2rem;
  font-size: 0.8rem;
  color: #ffffffaa;
}
</style>