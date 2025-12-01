<template>
  <header class="header">
    <div class="container">
      <div class="header-content">
        <div class="logo">
          <h2>🍳 Cooking Masterclass</h2>
        </div>
        <div class="wishlist-indicator">
          <span class="wishlist-count">{{ wishlistCount }}</span>
          ❤️ Wishlist
        </div>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'Header',
  props: {
    wishlistCount: {
      type: Number,
      required: true,
      default: 0
    }
  }
}
</script>

<style scoped>
.header {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 1rem 0;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

.header-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo h2 {
  margin: 0;
  font-weight: 600;
}

.wishlist-indicator {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-weight: 500;
}

.wishlist-count {
  background: #e74c3c;
  color: white;
  border-radius: 50%;
  width: 25px;
  height: 25px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.8rem;
}
</style>