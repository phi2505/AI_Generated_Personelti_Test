<script>
import { Configuration, OpenAIApi } from "openai";

export default {
  data() {
    return {
      questions: [],
    };
  },
  methods: {
    async generateQuestions() {
      const configuration = new Configuration({
        apiKey: process.env.VUE_APP_OPENAI_API_KEY,
      });
      const openai = new OpenAIApi(configuration);
      const response = await openai.createCompletion({
        model: "text-davinci-003",
        temperature: 0.7,
        max_tokens: 2000,
        top_p: 1,
        frequency_penalty: 0,
        presence_penalty: 0,
      });
      const rawQuestions = response.choices[0].text.split('\n').filter(q => q.trim() !== '');
      this.questions = rawQuestions.map(q => q.trim());
    },
  },
};
</script>