<template>
    <div class="questions-ctr">
        <div class="progress">
            <div 
                class="bar"
                :style="{width: `${(questionsAnswered / questions.length)*100}%`}"
            ></div>
            <div class="status">{{questionsAnswered}} out of {{questions.length}} questions answered</div>
        </div>
        <transition-group name="fade">
            <div 
            class="single-question" 
            v-for="(question, qi) in questions" 
            :key="question.q"
            v-show="questionsAnswered===qi"
            >
                <div class="question">{{question.q}}</div>
                <div class="answers">
                    <div 
                        class="answer" 
                        v-for="ans in question.answers" 
                        :key="ans.text"
                        @click.prevent="selectAns(ans.is_correct)"
                    >
                        {{ans.text}}
                    </div>
                </div>
            </div>
        </transition-group>
    </div>
</template>

<script>
export default {
    name: 'Questions',
    props: {
        questions: {
            type: Array
        },
        questionsAnswered: {
            type: Number
        }
    },
    emits: ['selectAns'],
    methods: {
        selectAns(isCorrect) {
            this.$emit('selectAns', isCorrect)
        }
    }
}
</script>

<style>

</style>