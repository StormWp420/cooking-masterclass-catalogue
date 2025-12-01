<template>
  <div id="app">
    <Header :wishlistCount="wishlistCount" />
    
    <main class="catalogue">
      <div class="container">
        <h1>Cooking Masterclasses</h1>
        
        <div class="courses-grid">
          <CourseCard 
            v-for="course in courses" 
            :key="course.id"
            :course="course"
            @save-course="saveToWishlist"
          />
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import CourseCard from './components/CourseCard.vue'

export default {
  name: 'App',
  components: {
    Header,
    CourseCard
  },
  data() {
    return {
      wishlistCount: 0,
      courses: [
        {
          id: 1,
          title: "Italian Pasta Masterclass",
          chef: "Chef Marco",
          price: 89,
          level: "Intermediate",
          available: true,
          image: "/images/pasta.jpg"
        },
        {
          id: 2,
          title: "French Pastry Fundamentals",
          chef: "Chef Sophie",
          price: 120,
          level: "Beginner",
          available: false,
          image: "/images/pastry.jpg"
        },
        {
          id: 3,
          title: "Japanese Sushi Art",
          chef: "Chef Kenji",
          price: 150,
          level: "Advanced",
          available: true,
          image: "/images/sushi.jpg"
        },
        {
          id: 4,
          title: "Modern Vegan Cuisine",
          chef: "Chef Lisa",
          price: 95,
          level: "Intermediate",
          available: true,
          image: "/images/vegan.jpg"
        }
      ]
    }
  },
  methods: {
    saveToWishlist(courseId) {
      // In a real app, you'd add to an array and track which courses are saved
      this.wishlistCount++
      console.log(`Course ${courseId} added to wishlist`)
      
      // Optional: Mark course as saved to prevent duplicate saves
      const course = this.courses.find(c => c.id === courseId)
      if (course) {
        course.saved = true
      }
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Arial', sans-serif;
  background-color: #f8f9fa;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.catalogue {
  padding: 2rem 0;
}

.catalogue h1 {
  text-align: center;
  margin-bottom: 2rem;
  color: #2c3e50;
}

.courses-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
  padding: 1rem 0;
}

@media (max-width: 768px) {
  .courses-grid {
    grid-template-columns: 1fr;
    gap: 1rem;
  }
}
</style>