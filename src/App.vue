<script setup>
import { ref } from 'vue';
import quizData from './data/quiz.json';

const quizzes = ref(quizData);
const searchQuery = ref("");

function filterQuiz() {
  if (!searchQuery.value.trim()){
    quizzes.value = quizData;
    return;
  }

  else{
    quizzes.value = quizData.filter(quiz => {
    return quiz.categoryName.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
           quiz.description.toLowerCase().includes(searchQuery.value.toLowerCase());
  });
  }

}

</script>
<template>
  <main>
    <div class="container">
      <header class="app-header">
        <h1>Quiz Wiz 🎉</h1>
        <p>Test your knowledge across various exciting topics!</p>
      </header>

      <section class="search-section">
        <div class="search-bar">
          <input v-model.trim="searchQuery" type="text" placeholder="Search quizzes or topics...">
          <button @click="filterQuiz">Search</button>
        </div>
      </section>

      <section v-if="quizzes.length > 0"  class="quiz-categories">
        <h2>Popular Categories</h2>
        <div class="category-grid">
          <div v-for="quiz in quizzes" :key="quiz.id" class="category-card">
            <h3>{{ quiz.categoryName }}</h3>
            <p>{{ quiz.description }}</p>
            <p> {{ quiz.questions.length }} {{ quiz.questions.length === 1 ? 'Question' : 'Questions' }}.</p>
          </div>
        </div>
      </section>
      <div v-else class="quiz-categories">
        <h2>GADA COK ITU</h2>
      </div>
    </div>
  </main>
</template>

<style scoped>
/* Base Styles & Resets */
:root {
  --primary-blue: #2563eb;
  --light-blue: #4f9efc;
  --background-light: #f8f9fa;
  --card-background: #ffffff;
  --text-dark: #333333;
  --text-medium: #666666;
  --border-light: #e0e0e0;
  --shadow-light: rgba(0, 0, 0, 0.05);
  --shadow-medium: rgba(0, 0, 0, 0.1);
}

/* No global body/html styles here as they would be handled by a root App.vue or global CSS */
/* We assume a basic reset is applied globally or by a framework */
body { /* This will apply if this component is the root or imported without body styles */
  font-family: 'Inter', sans-serif;
  background-color: var(--background-light);
  line-height: 1.6;
  color: var(--text-dark);
}

/* Main Layout */
main {
  display: flex;
  justify-content: center;
  padding: 40px 20px;
  min-height: 100vh;
  width: 100%; /* Ensure main takes full width */
}

.container {
  background-color: var(--card-background);
  width: 100%;
  max-width: 960px; /* Increased max-width for a broader layout */
  padding: 30px;
  border-radius: 16px;
  box-shadow: 0 10px 30px var(--shadow-light);
  display: flex;
  flex-direction: column;
  gap: 30px; /* Space between sections */
}

/* App Header */
.app-header {
  text-align: center;
  margin-bottom: 20px;
}

.app-header h1 {
  font-size: 2.8rem;
  font-weight: 700;
  color: var(--primary-blue);
  margin-bottom: 10px;
}

.app-header p {
  font-size: 1.1rem;
  color: var(--text-medium);
}

/* Search Section */
.search-section {
  margin-bottom: 30px;
}

.search-bar {
  display: flex;
  gap: 10px;
  max-width: 600px; /* Limit search bar width */
  margin: 0 auto;
  background-color: var(--card-background);
  border-radius: 12px;
  box-shadow: 0 4px 15px var(--shadow-light);
  padding: 8px;
}

.search-bar input {
  flex-grow: 1;
  border: none;
  padding: 12px 18px;
  font-size: 1rem;
  border-radius: 8px; /* Slightly less rounded than container */
  outline: none;
  color: var(--text-dark);
}

.search-bar input::placeholder {
  color: var(--text-medium);
  opacity: 0.7;
}

.search-bar input:focus {
  box-shadow: 0 0 0 2px var(--light-blue);
}

.search-bar button {
  background: linear-gradient(135deg, var(--light-blue), var(--primary-blue));
  color: white;
  border: none;
  padding: 12px 25px;
  font-size: 1rem;
  font-weight: 600;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s ease;
  box-shadow: 0 3px 8px rgba(37, 99, 235, 0.3);
}

.search-bar button:hover {
  transform: translateY(-1px);
  box-shadow: 0 5px 12px rgba(37, 99, 235, 0.4);
}

.search-bar button:active {
  transform: translateY(0);
  box-shadow: 0 2px 5px rgba(37, 99, 235, 0.3);
}

/* Quiz Categories Section */
.quiz-categories {
  text-align: center;
}

.quiz-categories h2 {
  font-size: 2rem;
  font-weight: 600;
  color: var(--text-dark);
  margin-bottom: 25px;
}

.category-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); /* Flexible grid columns */
  gap: 20px;
  justify-content: center;
  max-width: 900px; /* Align grid with container max-width */
  margin: 0 auto;
}

.category-card {
  background-color: var(--card-background);
  padding: 25px;
  border-radius: 12px;
  box-shadow: 0 4px 15px var(--shadow-light);
  text-align: center;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  cursor: pointer;
  border: 1px solid var(--border-light);
}

.category-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 20px var(--shadow-medium);
  border-color: var(--primary-blue);
}

.category-card h3 {
  font-size: 1.4rem;
  font-weight: 600;
  color: var(--primary-blue);
  margin-bottom: 8px;
}

.category-card p {
  font-size: 0.95rem;
  color: var(--text-medium);
}

/* Responsive Adjustments */
@media (max-width: 768px) {
  .app-header h1 {
    font-size: 2.2rem;
  }
  .quiz-categories h2 {
    font-size: 1.8rem;
  }
  .container {
    padding: 20px;
    gap: 20px;
  }
  .search-bar {
    flex-direction: column;
    padding: 10px;
  }
  .search-bar input {
    margin-bottom: 10px;
    text-align: center;
  }
  .search-bar button {
    width: 100%;
  }
  .category-grid {
    grid-template-columns: 1fr; /* Stack cards on small screens */
  }
}

@media (max-width: 480px) {
  main {
    padding: 20px 10px;
  }
  .app-header h1 {
    font-size: 2rem;
  }
  .search-bar input,
  .search-bar button {
    padding: 10px 15px;
    font-size: 0.95rem;
  }
  .category-card {
    padding: 20px;
  }
  .category-card h3 {
    font-size: 1.2rem;
  }
}
</style>
