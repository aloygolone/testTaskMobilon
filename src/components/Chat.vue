<template>
  <div class="chat-container">
    <div class="chat-window left-chat">
      <h2>User 1</h2>
      <div class="messages">
        <div
          v-for="(msg, index) in messages1"
          :key="index"
          class="message"
          :class="[msg.user === user1 ? 'user1' : 'user2']"
        >
          {{ msg.message }}
        </div>
      </div>
      <div class="input-block">
        <input
          v-model="newMessage1"
          @keyup.enter="sendMessage1"
          placeholder="Введите сообщение..."
        />
        <button @click="sendMessage1" class="button">Отправить</button>
      </div>
    </div>

    <div class="chat-window right-chat">
      <h2>User 2</h2>
      <div class="messages">
        <div
          v-for="(msg, index) in messages2"
          :key="index"
          class="message"
          :class="[msg.user === user1 ? 'user2' : 'user1']"
        >
          {{ msg.message }}
        </div>
      </div>
      <div class="input-block">
        <input
          v-model="newMessage2"
          @keyup.enter="sendMessage2"
          placeholder="Введите сообщение..."
        />
        <button @click="sendMessage2" class="button">Отправить</button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const messages1 = ref([]);
    const messages2 = ref([]);
    const newMessage1 = ref("");
    const newMessage2 = ref("");
    const user1 = "user1";
    const user2 = "user2";

    const sendMessage1 = () => {
      if (newMessage1.value.trim()) {
        messages1.value.push({ message: newMessage1.value, user: user1 });
        messages2.value.push({ message: newMessage1.value, user: user1 }); // Отправляем сообщение в оба чата
        newMessage1.value = "";
      }
    };

    const sendMessage2 = () => {
      if (newMessage2.value.trim()) {
        messages2.value.push({ message: newMessage2.value, user: user2 });
        messages1.value.push({ message: newMessage2.value, user: user2 }); // Отправляем сообщение в оба чата
        newMessage2.value = "";
      }
    };

    return {
      messages1,
      messages2,
      newMessage1,
      newMessage2,
      user1,
      user2,
      sendMessage1,
      sendMessage2,
    };
  },
};
</script>

<style>
.chat-container {
  display: flex;
  justify-content: space-between;
  width: 100%;
  max-width: 800px;
  margin: auto;
}

.chat-window {
  border: 1px solid #ccc;
  padding: 10px;
  width: 45%;
  display: flex;
  flex-direction: column;
}

.messages {
  height: 300px;
  overflow-y: auto;
  margin-bottom: 10px;
  flex-grow: 1;
  border: 1px solid;
  display: flex;
  flex-direction: column;
  gap: 10px;
  padding: 20px;
}

.message {
  padding: 5px;
  border-radius: 5px;
  margin: 5px 0;
  display: flex;
  justify-content: flex-start;
}

.input-block {
    display: flex;
    justify-content: space-between;
}

.user1 {
  background-color: #e0f7fa; /* Цвет для сообщений первого пользователя */
  display: flex;
  justify-content: end; /* Сообщения первого пользователя слева */
}

.user2 {
  background-color: #ffe0b2; /* Цвет для сообщений второго пользователя */
  display: flex;
  justify-content: start;/* Сообщения второго пользователя справа */
}
</style>
