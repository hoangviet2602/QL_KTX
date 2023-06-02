<template>
  <div class="custom-notification" :class="notificationClass">
    <div class="notification-content">
      <span class="notification-message">{{ message }}</span>
      <button class="notification-close" @click="closeNotification">×</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CustomNotification',
  props: {
    message: {
      type: String,
      required: true,
    },
    type: {
      type: String,
      default: 'success',
      validator: (value) => ['info', 'success', 'warning', 'error'].includes(value),
    },
    duration: {
      type: Number,
      default: 3000, // Default duration of 3 seconds
    },
  },
  computed: {
    notificationClass() {
      return `notification-${this.type}`;
    },
  },
  mounted() {
    this.scheduleDismiss();
  },
  methods: {
    closeNotification() {
      this.$emit('close');
    },
    scheduleDismiss() {
      setTimeout(() => {
        this.closeNotification();
      }, this.duration);
    },
  },
};
</script>

<style scoped>
.custom-notification {
  position: fixed;
  top: 20px;
  right: 20px;
  padding: 10px 20px;
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #ffffff;
  color: #333333;
  font-family: Arial, sans-serif;
  font-size: 14px;
}

.notification-info {
  background-color: #3498db;
  color: #ffffff;
}

.notification-success {
  background-color: #27ae60;
  color: #ffffff;
}

.notification-warning {
  background-color: #f39c12;
  color: #ffffff;
}

.notification-error {
  background-color: #e74c3c;
  color: #ffffff;
}

.notification-content {
  display: flex;
  align-items: center;
}

.notification-message {
  margin-right: 10px;
}

.notification-close {
  border: none;
  background: none;
  cursor: pointer;
  font-weight: bold;
}
</style>
