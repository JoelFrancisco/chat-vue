<script setup lang="ts">
import { ref } from "vue";
import { v4 as uuidv4 } from "uuid";

type Message = {
  id: ReturnType<typeof uuidv4>
  text: string;
  userType: "client" | "clerk"
}

let newMessageText = ref("");
const messages = ref<Message[]>([{
  id: uuidv4(),
  text: "bla bla",
  userType: "clerk"
}]);

function addMessage() {
  if (newMessageText.value === "") return;

  messages.value.push({
    id: uuidv4(),
    text: newMessageText.value,
    userType: "client"
  });
}
</script>

<template>
  <header>
    <h2 class="title">Atendimento on-line</h2>
  </header>

  <main>
    <div v-for="message in messages" :key="message.id">
      <div v-if="message.userType === 'clerk'" class="user1-message">
        <div>Atendente diz:</div>
        <div class="message-item">
          {{ message.text }}
        </div>
      </div>
      <div v-else class="user2-message">
        <div class="user2-message-wrapper">
          <div>Você diz:</div>
          <div class="message-item">
            {{ message.text }}
          </div>
        </div>
      </div>
    </div>
  </main>

  <footer>
    <form @submit.prevent="addMessage" action="post">
      <input v-model="newMessageText" placeholder="Digite sua mensagem..." type="text" class="textbox">
      <button type="submit" class="send-button">
        ENVIAR
      </button>
    </form>
  </footer>
</template>

<style scoped>
header {
    font-family: 'Shantell Sans', cursive;
    min-width: 85%;
    min-height: 5%;
    border: 1px solid #000;
    padding: 10px;
}

footer {
    font-family: 'Shantell Sans', cursive;
    min-width: 85%;
    min-height: 20%;

    padding: 10px;

    position: -webkit-sticky;
    position: sticky;
    left: 0;
    bottom: 0;    
}

main {
    min-height: 60vh;
    max-height: 60vh;
    min-width: 85%;

    padding: 10px;
    border: 1px solid #000;

    display: flex;
    flex-direction: column;

    justify-content:flex-start;
    gap: 10px;

    overflow-y: auto;
    overflow-x: hidden;
}

form {
    width: 100%;
    height: 100%;

    display: flex;
    justify-content: space-between;
}

.textbox {
    border: 1px solid #000;
    width: 75%;
    height: 8vh;
    font-family: 'Shantell Sans', cursive;
    display: flex;
    align-items: center;
    padding-left: 1%;
}

.send-button {
    height: 8vh;
    width: 23%;

    font-family: 'Shantell Sans', cursive;
    font-size: 1em;
    color: rgb(4, 112, 37);
    border: 1px solid #000;
}

.user1-message {
    width: 100%;
    margin-left: 10px;
}

.user2-message {
    display: flex;
    width: 100%;
    justify-content: flex-end;
    margin-right: 10px;
}

.message-item {
    border: 1px solid #000;
    min-width: 30vw;
    max-width: 30vw;
    padding: 10px;
}

.user2-message-wrapper {
    display: flex;
    flex-direction: column;
}

.title {
    font-family: 'Shantell Sans', cursive;
    color: rgb(51, 51, 241);
    font-size: 2.25rem;
    line-height: 2.5rem;
}
</style>