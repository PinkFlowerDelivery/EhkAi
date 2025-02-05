<template>
  <ModelSelector @selectModel="selectModel" />
  <Chat :messages="messages" :name="modelType" />
  <SearchBar
  :link="AiLink"
  :selectedModel="modelType"
  :messages="messages"
  @updateMessages="updateMessages"
  />
</template>
<script setup>
import SearchBar from './components/SearchBar.vue';
import Chat from './components/Chat.vue';
import ModelSelector from './components/SelectModel.vue';
import { ref } from 'vue';

const modelType = ref('GPT3.5')
const AiLink = ref('https://api.onlysq.ru/ai/v1');
const messages = ref([]);

function selectModel(model) {
  modelType.value = model;

  const modelSettings = {
    "GPT-4o Mini": {link: "https://api.onlysq.ru/ai/v2", name: "GPT-4o Mini"},
    "GPT-4": { link: "https://api.onlysq.ru/ai/v2", name: "GPT-4" },
    "SearchGPT": { link: "https::/api.onlysq.ru/ai/v2", name: "SearchGPT" },
    "GPT-3.5 Turbo" : { link: "https::/api.onlysq.ru/ai/v2", name: "GPT-3.5 Turbo" },
    "Claude 3 Haiku" : { link: "https::/api.onlysq.ru/ai/v2", name: "Claude 3 Haiku" },
    "Gemini": { link: "https://api.onlysq.ru/ai/v2", name: "Gemini"},
    "Gemini Flash": { link: "https://api.onlysq.ru/ai/v2", name: "Gemini Flash"},
    "Llama 3.1": { link: "https://api.onlysq.ru/ai/v2", name: "Llama 3.1"},
    "Copilot": { link: "https://api.onlysq.ru/ai/v2", name: "Copilot"},
    "Command-R+": { link: "https://api.onlysq.ru/ai/v2", name: "Command-R+"},
    "Qwen": { link: "https://api.onlysq.ru/ai/v2", name: "Qwen"},
    "Blackbox": { link: "https://api.onlysq.ru/ai/v2", name: "Blackbox AI"},
    "Mixtral 8x7B": { link: "https://api.onlysq.ru/ai/v2", name: "Mixtral 8x7B"},
    "evil": { link: "https://api.onlysq.ru/ai/v2", name: "evil"},
    "Claude 3.5 Sonnet": { link: "https://api.onlysq.ru/ai/v2", name: "Claude 3.5 Sonnet"},
    "Flux": { link: "https://api.onlysq.ru/ai/v2", name: "Flux"},
    "Kandinsky": { link: "https://api.onlysq.ru/ai/v2", name: "Kandinsky"},
    "NSFW-XL": { link: "https://api.onlysq.ru/ai/v2", name: "NSFW-XL"},
  };

  if (modelSettings[model]) {
    modelType.value = modelSettings[model].name;
    AiLink.value = modelSettings[model].link;
  } else {
    modelType.value = "Artificial Intelligence";
    AiLink.value = "https://api.onlysq.ru/ai/v1";
  }
}

function updateMessages(newMessage) {
  messages.value.push({
    ...newMessage,
    modelName: modelType.value,
  });
}
</script>
