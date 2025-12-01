<template>
  <div class="course-card" :class="{ 'sold-out': !course.available }">
    <div class="card-image">
      <img :src="course.image" :alt="course.title" />
      <div v-if="!course.available" class="sold-out-badge">Sold Out</div>
    </div>
    
    <div class="card-content">
      <h3 class="course-title">{{ course.title }}</h3>
      <p class="course-chef">By {{ course.chef }}</p>
      
      <div class="course-details">
        <span class="level" :class="course.level.toLowerCase()">
          {{ course.level }}
        </span>
        <span class="price">${{ course.price }}</span>
      </div>
      
      <button 
        class="save-btn" 
        :disabled="!course.available || course.saved"
        @click="saveCourse"
        :class="{ 'saved': course.saved }"
      >
        {{ course.saved ? 'Saved!' : (course.available ? 'Save to Wishlist' : 'Unavailable') }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CourseCard',
  props: {
    course: {
      type: Object,
      required: true
    }
  },
  methods: {
    saveCourse() {
      if (this.course.available && !this.course.saved) {
        this.$emit('save-course', this.course.id)
      }
    }
  }
}
</script>

<style scoped>
.course-card {
  background: white;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.course-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 15px rgba(0, 0, 0, 0.15);
}

.course-card.sold-out {
  opacity: 0.7;
}

.card-image {
  position: relative;
  height: 200px;
  overflow: hidden;
}

.card-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.sold-out-badge {
  position: absolute;
  top: 10px;
  right: 10px;
  background: #e74c3c;
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: bold;
}

.card-content {
  padding: 1.5rem;
}

.course-title {
  font-size: 1.2rem;
  margin-bottom: 0.5rem;
  color: #2c3e50;
}

.course-chef {
  color: #7f8c8d;
  margin-bottom: 1rem;
  font-style: italic;
}

.course-details {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.5rem;
}

.level {
  padding: 0.3rem 0.8rem;
  border-radius: 15px;
  font-size: 0.8rem;
  font-weight: 600;
  text-transform: uppercase;
}

.level.beginner {
  background: #d4edda;
  color: #155724;
}

.level.intermediate {
  background: #fff3cd;
  color: #856404;
}

.level.advanced {
  background: #f8d7da;
  color: #721c24;
}

.price {
  font-size: 1.5rem;
  font-weight: bold;
  color: #27ae60;
}

.save-btn {
  width: 100%;
  padding: 0.8rem;
  background: #3498db;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 1rem;
  cursor: pointer;
  transition: background 0.3s ease;
}

.save-btn:hover:not(:disabled) {
  background: #2980b9;
}

.save-btn:disabled {
  background: #bdc3c7;
  cursor: not-allowed;
}

.save-btn.saved {
  background: #27ae60;
}
</style>