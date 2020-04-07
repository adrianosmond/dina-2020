<template>
  <div id="app">
    <h1>Guess the words</h1>
    <p>Can you spot the common theme/pattern?</p>
    <div class="form">
      <input
        v-model="attempt"
        type="text"
        placeholder="Your guess here..."
        @keypress.enter="checkWord"
      />
      <button @click="checkWord">Guess</button>
    </div>
    <div class="drawings">
      <drawing
        v-for="drawing in drawings"
        :key="drawing.id"
        :drawing="drawing"
      />
      <hint v-if="unsolvedWords.length === 0" />
      <teaser v-else />
    </div>
  </div>
</template>

<script>
import Drawing from './components/Drawing.vue';
import Hint from './components/Hint.vue';
import Teaser from './components/Teaser.vue';

export default {
  name: 'App',
  components: {
    Drawing,
    Hint,
    Teaser,
  },
  data() {
    return {
      attempt: '',
      drawings: [
        {
          id: 'drawing-4',
          words: [
            {
              word: 'ill',
              solved: false,
            },
            {
              word: 'ex',
              solved: true,
            },
            {
              word: 'in',
              solved: true,
            },
            {
              word: 'bathrobe',
              solved: false,
            },
          ],
        },
        {
          id: 'drawing-5',
          words: [
            {
              word: 'teal',
              solved: false,
            },
            {
              word: 'ribbon',
              solved: false,
            },
            {
              word: 'helix',
              solved: false,
            },
          ],
        },
        {
          id: 'drawing-1',
          words: [
            {
              word: 'ibex',
              solved: false,
            },
            {
              word: 'rhino',
              solved: false,
            },
            {
              word: 'ballet',
              solved: false,
            },
          ],
        },
        {
          id: 'drawing-2',
          words: [
            {
              word: 'rabbi',
              solved: false,
            },
            {
              word: 'lex',
              solved: false,
            },
            {
              word: 'hotline',
              solved: false,
            },
          ],
        },
        {
          id: 'drawing-3',
          words: [
            {
              word: 'bean',
              solved: false,
            },
            {
              word: 'roll',
              solved: false,
            },
            {
              word: 'exhibit',
              solved: false,
            },
          ],
        },
      ],
    };
  },
  computed: {
    unsolvedWords() {
      return this.drawings
        .map(d => d.words)
        .flat()
        .filter(w => !w.solved)
        .map(w => w.word);
    },
  },
  methods: {
    checkWord() {
      if (this.unsolvedWords.includes(this.attempt)) {
        this.setSolved(this.attempt);
      }

      this.attempt = '';
    },
    setSolved(solvedWord) {
      this.drawings = this.drawings.map(drawing => ({
        ...drawing,
        words: drawing.words.map(word => ({
          ...word,
          solved: word.word === solvedWord ? true : word.solved,
        })),
      }));
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  font-size: 20px;
}

*,
*::before,
*::after {
  box-sizing: border-box;
}

h1 {
  line-height: 1;
  margin: 1rem 0;
}

p {
  margin: 1rem 0;
}

.form {
  display: flex;
  position: sticky;
  top: 0;
  padding: 0.5rem;
  justify-content: center;
  margin-bottom: 1rem;
  background-color: white;
}

input {
  font: inherit;
  padding: 0.25rem 0.5rem;
}

button {
  font: inherit;
  background-color: dodgerblue;
  color: white;
  padding: 0.25rem 1rem;
  border: none;
}

input + button {
  margin-left: 1rem;
}

.drawings {
  max-width: 800px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 2rem;
  margin: 4rem auto;
}
</style>
