<template>
  <section class="section has-text-centered">
    <div class="container">
      <h1 class="title"> {{ systemMessage }} </h1>
      <figure class="image is-3by5">
        <img :src="'/images/'+treeImage" alt="縦長画像">
      </figure>
      <p>
        優しい言葉を投げかけると木が育って、
        優しくない言葉を投げかけると退化する。
      </p>
      <br>
      <b-field class="input-group">
        <b-input class="message-box" placeholder="テキストを入力" v-model="newMessage"></b-input>
        <b-button class="send-button" type="is-primary" @click="sendMessage">送信</b-button>
      </b-field>
      <div class="chat-history">
        <div v-for="(message, index) in messages" :key="index" class="message">
          {{ message }}
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      messages: [],
      newMessage: '',
    }
  },
  methods: {
    sendMessage() {
      if (this.newMessage.trim() !== '') {
        this.messages.unshift(this.newMessage);
        this.newMessage = '';
      }
    }
  },
  computed: {
    treeImage: function() {
      if (this.messages.length === 0) return "7.png";
      if (this.messages.length < 7) return `${7 - this.messages.length}.png`;
      return "1.png";
    },

    systemMessage:function() {
      if (this.messages.length >= 6) return "あなただけが好き💕";
      return [
        "優しい言葉で育てよう！",
        "うれしいな、うふふ",
        "もっと優しくして！",
        "もっと褒めてよ！？",
        "他の人のとこいくよ！？",
        "もっとかまって！！！",
      ][this.messages.length];
    }
  }
}
</script>

<style scoped>
.section {
  display: flex;
  align-items: center;
  justify-content: center;
}
.image {
  margin: 20px auto;
}
.title {
  font-size: 24px;
}
.chat-history {
  max-height: 200px;
  overflow-y: auto;
  margin-top: 20px;
}
.input-group {
  margin-bottom: 20px;
}
.message-box {
  flex: 1;
  margin-right: 90px;
}
.send-button {
  flex-shrink: 0;
}
.message {
  background-color: #f5f5f5;
  padding: 10px;
  margin: 5px 0;
  border-radius: 5px;
}
</style>
