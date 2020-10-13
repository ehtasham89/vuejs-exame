<template>
  <div>
      <v-row>
          <v-col>
            <v-card>
                {{this.question.text}}
            </v-card>
        </v-col>
      </v-row>
      <v-row>
          <v-col>
            <v-radio-group v-model="answer">
                <v-radio
                    v-for="n in question.options"
                    :key="n.id"
                    :label="`${n.text}`"
                    :value="n.score"
                ></v-radio>
            </v-radio-group>
        </v-col>
      </v-row>

      <action :qid="question.id" :answer="answer"  />
  </div>

</template>

<script>
import Action from '~/components/Action.vue'

export default {
    props:['question'],
    
    data(){
        return {
            currentId: 0,
            answer: 0,
        }
    },
    mounted() {
        this.$nuxt.$on('update-action', () => {
            this.answer = 0;
        })
    },
    components: {
        Action
    }
}

</script>