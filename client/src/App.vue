<template>
  <div id="app" class="app-container">
    <header class="header">
      <div class="logo-container">
        <img src="https://via.placeholder.com/100" alt="Логотип" class="logo" />
      </div>
      <h1>ISH</h1>
      <div class="account-buttons">
        <button @click="createAccount" class="gradient-button">Создать аккаунт</button>
        <button @click="viewProfile" class="gradient-button">Мой профиль</button>
        <button @click="resetSwipes" class="gradient-button">Сбросить свайпы</button>
      </div>
    </header>
    <main class="main-content">
      <div class="card-container">
        <transition name="fade">
          <div v-if="hasCards" class="card" :class="{ swipeLeft: isSwipedLeft, swipeRight: isSwipedRight }">
            <img :src="currentCard.image" alt="Profile Image" class="profile-image" />
            <h2>{{ currentCard.name }}</h2>
            <p>{{ currentCard.description }}</p>
            <div class="swipe-buttons">
              <button class="swipe-button dislike" @click="swipeLeft">Не нравится</button>
              <button class="swipe-button like" @click="swipeRight">Нравится</button>
            </div>
          </div>
          <div v-else>
            <p>Нет доступных карточек.</p>
          </div>
        </transition>
      </div>
    </main>
    <footer class="footer">
      <div class="social-icons">
        <a href="https://telegram.org" target="_blank" class="social-icon">
          <img src="https://upload.wikimedia.org/wikipedia/commons/8/88/Telegram_logo.svg" alt="Telegram" />
        </a>
        <a href="https://vk.com" target="_blank" class="social-icon">
          <img src="https://upload.wikimedia.org/wikipedia/commons/5/51/VK.com_logo.svg" alt="ВКонтакте" />
        </a>
        <a href="https://whatsapp.com" target="_blank" class="social-icon">
          <img src="https://upload.wikimedia.org/wikipedia/commons/6/6b/WhatsApp.svg" alt="WhatsApp" />
        </a>
      </div>
      <p class="footer-text">© 2025 ISH. Все права защищены.</p>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cards: [
        { name: 'Алексей', description: 'Люблю путешествовать и читать книги.', image: 'https://via.placeholder.com/150' },
        { name: 'Мария', description: 'Фотограф, увлекаюсь искусством.', image: 'https://via.placeholder.com/150' },
        { name: 'Дмитрий', description: 'Спортсмен, люблю активный отдых.', image: 'https://via.placeholder.com/150' },
        { name: 'Екатерина', description: 'Обожаю готовить и заниматься спортом.', image: 'https://via.placeholder.com/150' },
        { name: 'Сергей', description: 'Музыкант, играю на гитаре.', image: 'https://via.placeholder.com/150' },
        { name: 'Анна', description: 'Люблю природу и активный отдых.', image: 'https://via.placeholder.com/150' },
      ],
      currentIndex: 0,
      isSwipedLeft: false,
      isSwipedRight: false,
    };
  },
  computed: {
    currentCard() {
      return this.cards[this.currentIndex];
    },
    hasCards() {
      return this.cards.length > 0 && this.currentIndex < this.cards.length;
    },
  },
  methods: {
    createAccount() {
      alert('Создание аккаунта...');
    },
    viewProfile() {
      alert('Просмотр профиля...');
    },
    swipeLeft() {
      this.isSwipedLeft = true;
      setTimeout(() => {
        this.currentIndex++;
        this.isSwipedLeft = false;
        if (this.currentIndex >= this.cards.length) {
          this.currentIndex = this.cards.length - 1; // Останавливаться на последней карточке
        }
      }, 300); // Время анимации
    },
    swipeRight() {
      alert(`Вы понравились ${this.currentCard.name}`);
      this.isSwipedRight = true;
      setTimeout(() => {
        this.currentIndex++;
        this.isSwipedRight = false;
        if (this.currentIndex >= this.cards.length) {
          this.currentIndex = this.cards.length - 1; // Останавливаться на последней карточке
        }
      }, 300); // Время анимации
    },
    resetSwipes() {
      this.currentIndex = 0; // Сбросить индекс к первой карточке
    },
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

/* Основные стили */
.app-container {
  text-align: center;
  background: linear-gradient(to bottom right, #ff7e5f, #feb47b); /* Градиентный фон */
  color: #333;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between; /* Разделение контента и footer */
  font-family: 'Roboto', sans-serif;
}

.header {
  background-color: rgba(255, 255, 255, 0.9); /* Полупрозрачный фон */
  color: #ff5864; /* Цвет текста */
  padding: 20px;
  width: 100%;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  border-radius: 10px;
  margin-top: 20px; /* Отступ сверху для заголовка */
  display: flex;
  align-items: center; /* Центрирование содержимого по вертикали */
}

.logo-container {
  margin-right: 20px; /* Отступ справа для логотипа */
}
.logo {
  width: 100px; /* Ширина логотипа */
  height: auto; /* Автоматическая высота для сохранения пропорций */
}

.account-buttons {
  margin-left: auto; /* Сдвиг кнопок вправо */
}

.gradient-button {
  margin: 0 10px;
  padding: 10px 20px;
  background: linear-gradient(to right, #ff7e5f, #feb47b); /* Градиентная заливка */
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.2s;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.gradient-button:hover {
  transform: scale(1.05);
}

.main-content {
  margin-top: 20px;
  display: flex;
  justify-content: center; /* Центрирование карточки */
  align-items: center; /* Центрирование карточки по вертикали */
  height: 100%; /* Занять всю высоту */
}

.card-container {
  border: 1px solid #ff5864; /* Цвет рамки карточки */
  border-radius: 10px;
  padding: 20px;
  background-color: white;
  width: 400px; /* Увеличенный размер карточки */
  height: 500px; /* Увеличенная высота карточки */
  margin: auto;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  transition: transform 0.3s;
}

.card {
  transition: transform 0.3s;
}

.profile-image {
  width: 100%;
  border-radius: 10px;
  margin-bottom: 15px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.card h2 {
  margin: 0;
  font-size: 28px; /* Увеличенный размер шрифта для имени */
  font-weight: bold;
}

.card p {
  font-size: 18px; /* Увеличенный размер шрифта для описания */
  margin: 10px 0;
}

.swipe-buttons {
  margin-top: 20px;
}

.swipe-button {
  margin: 0 10px;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-weight: bold;
  transition: background-color 0.3s, transform 0.2s;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.swipe-button.like {
  background-color: #4caf50; /* Зеленый цвет для "Нравится" */
  color: white;
}

.swipe-button.dislike {
  background-color: #f44336; /* Красный цвет для "Не нравится" */
  color: white;
}

.swipe-button:hover {
  transform: scale(1.05);
}

.swipe-button.like:hover {
  background-color: #45a049; /* Темно-зеленый при наведении */
}

.swipe-button.dislike:hover {
  background-color: #d32f2f; /* Темно-красный при наведении */
}

/* Анимация для карточек */
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active в <2.1.8 */ {
  opacity: 0;
}

/* Анимации для свайпов */
.swipeLeft {
  animation: swipe-left 0.3s forwards;
}

.swipeRight {
  animation: swipe-right 0.3s forwards;
}

@keyframes swipe-left {
  0% {
    transform: translateX(0);
    opacity: 1;
  }
  100% {
    transform: translateX(-100%);
    opacity: 0;
  }
}

@keyframes swipe-right {
  0% {
    transform: translateX(0);
    opacity: 1;
  }
  100% {
    transform: translateX(100%);
    opacity: 0;
  }
}

/* Стили для footer */
.footer {
  background-color: rgba(255, 255, 255, 0.9); /* Цвет такой же, как у header */
  color: #ff5864; /* Цвет текста */
  padding: 20px;
  width: 100%;
  box-shadow: 0 -2px 4px rgba(0, 0, 0, 0.1);display: flex;
  flex-direction: column;
  align-items: center; /* Центрирование содержимого */
}

.social-icons {
  display: flex;
  justify-content: center; /* Центрирование иконок */
  gap: 20px; /* Отступ между иконками */
  margin-bottom: 10px; /* Отступ снизу */
}

.social-icon img {
  width: 40px; /* Ширина иконок */
  height: 40px; /* Высота иконок */
  transition: transform 0.3s; /* Плавный эффект при наведении */
}

.social-icon img:hover {
  transform: scale(1.1); /* Увеличение иконки при наведении */
}

.footer-text {
  font-size: 14px; /* Размер шрифта для текста в footer */
  margin: 0; /* Убираем отступы */
}
</style>