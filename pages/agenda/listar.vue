<script setup>
import { ref, defineProps } from "vue";
import axios from "axios";
import { HttpTransportType, HubConnection, HubConnectionBuilder } from "@aspnet/signalr";

const listAgenda = ref([]);

const getAgenda = async () => {
  try {
    const response = await axios.get("https://api-vacinacao.onrender.com/agenda", {
      headers: {
        Authorization: "Bearer " + localStorage.getItem("token"),
      },
    });
    listAgenda.value = response.data;
  } catch (error) {
    if (error.response.status === 401) {
      window.location.href = "/logout";
    }
  }
};

onMounted(() => {
  getAgenda();
});

</script>

<template>
  <div>
    <menu-flyout />
    <div
      class="bg-gray-900 min-h-screen p-8 md:p-24 items-center justify-center min-w-screen"
    >
      <listar-agendas :agendas="listAgenda" />
    </div>
  </div>
</template>
