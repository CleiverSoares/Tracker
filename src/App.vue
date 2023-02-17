<template>
  <main class="columns is-gapless is-multiline" :class="{ 'modo-escuro': modoEscuroAtivo }">
    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="trocarTema" />
    </div>
    <div class="column is-three-quarter conteudo">
      
      <Formulario @aoSalvarTarefa="salvatTarefa" />
      <div class="lista">
        <TarefaVue
          v-for="(tarefa, index) in tarefas"
          :key="index"
          :tarefa="tarefa"
        />
        <Box v-if="listaEstaVazia"> Você não está muito produtivo hoje 😢 </Box>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import BarraLateral from "./components/BarraLateral.vue";
import Box from "./components/Box.vue";
import Formulario from "./components/Formulario.vue";
import TarefaVue from "./components/Tarefa.vue";
import ITarefa from "./interfaces/ITarefa";
export default defineComponent({
  name: "App",
  components: {
    BarraLateral,
    Formulario,
    TarefaVue,
    Box,
  },

  data() {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo : false,
    };
  },

  computed: {
    listaEstaVazia(): boolean {
      return this.tarefas.length === 0;
    },
  },

  methods: {
    salvatTarefa(tarefa: ITarefa) {
      this.tarefas.push(tarefa);
    },
    trocarTema(modoEscuroAtivo : boolean)  {
      this.modoEscuroAtivo = modoEscuroAtivo;
    },
  },
});
</script>

<style>
.lista {
  padding: 1.25rem;
}
main {
  --bg-primario: #fff;
  --texto-primario: #000;
}

main.modo-escuro {
  --bg-primario: #2b2d41;
  --texto-primario: #ddd;
}
.conteudo {
  background-color: var(--bg-primario);
}
</style>
