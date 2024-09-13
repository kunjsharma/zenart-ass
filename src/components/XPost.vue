<template>

  <div class="xpost-container">
    <div class="xpost-container_row">
      <textarea ref="xpost" placeholder="What is happening?!" @input="onPost" />
    </div>
    <div class="xpost-container_row">
      <button ref="postButton" :class="{'disabled' : !this.isPost}" @click="createPost" :disabled="!this.isPost" >Post</button>
    </div>
  </div>
  <div class="xposts-container">
    <div class="xposts-container_row" v-for="(item, index) in this.items" :key="item.index">

      <div :ref="'row-' + index" :id="['row-' + index]">{{ item }}</div>
      <textarea :ref="'xpost-' + index" :id="['xpost-' + index]" placeholder=""></textarea>
      <div :id="[index]" class="xposts-container_buttons">
        <button @click="likePost">Like</button>
        <button @click="editPost">Edit</button>
        <button @click="deletePost">Delete</button>
      </div>
    </div>
  </div>

</template>

<script>
export default {
  name: 'XPost',
  props: {
    msg: String,
  },
  data() {
    return {
      items: [],
      isPost: false,
    };
  },
  methods: {
    onPost() {
      this.$refs.xpost.value.length > 0 ? this.isPost = true : this.isPost = false;
    },
    createPost() {
      let post = this.$refs.xpost.value;
      this.items.push(post);
      this.$refs.xpost.value = '';
      this.isPost = false;
      console.log(this.items);
    },
    likePost(event) {
      let _target = event.target;
      _target.classList.contains('liked') ? _target.className = '' : _target.className = 'liked';
    },
    editPost(event) {
      let id = event.target.parentElement.id;
      let row = this.$refs['row-' + id][0];
      let xpost = this.$refs['xpost-' + id][0];

      let rowText = this.$refs['row-' + id][0].innerHTML;
      //let xpostText = this.$refs['xpost-' + id][0].value;

      if (event.target.innerHTML == "Save") {
        event.target.innerHTML = "Edit";
        row.className = 'visible';
        xpost.className = 'hidden';
        this.$refs['row-' + id][0].innerHTML = this.$refs['xpost-' + id][0].value;

      } else {
        event.target.innerHTML = "Save"
        row.className = 'hidden';
        xpost.className = 'visible';
        this.$refs['xpost-' + id][0].value = rowText;
      }
    },
    deletePost(event) {
      let id = event.target.parentElement.id;
      this.items.splice(id, 1);
    },
  },
  mounted() {
    this.isPost = this.$refs.xpost.value != '';
  },
}
</script>

<style lang="less">
//Theme configuration
@fontColor: #ffffff;
@primaryButtonColor: #2962ff;
@secondaryButtonColor: #575757;

.xpost-container {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  margin: 20px;

  &_row {
    width: 100%;
    text-align: right;
  }

  textarea {
    color: @fontColor;
    background-color: #202020;
    font-family: Avenir, Helvetica, Arial, sans-serif;
    border: 0;
    outline: none;
    height: auto;
    width: 100%;
    resize: none;
    box-sizing: border-box;
  }

  button {
    background-color: @primaryButtonColor;
    color: @fontColor;
    font-weight: bold;
    border: 0;
    border-radius: 20px;
    padding: 10px 20px;
    margin: 10px 0px 10px 10px;
    &.disabled {
      background-color: #3f4861;
    }
  }
}

.xposts-container {
  display: flex;
  flex-direction: row;
  align-items: flex-end;
  flex-wrap: wrap;
  margin: 20px;
  text-align: left;

  &_row {
    width: 100%;
  }

  &_buttons {
    text-align: right;
  }

  button {
    background-color: @secondaryButtonColor;
    color: @fontColor;
    font-weight: bold;
    border: 0;
    border-radius: 10px;
    padding: 5px 10px;
    margin: 10px 0px 10px 10px;

    &.liked {
      background-color: #e40072;
    }
  }

  textarea {
    display: none;
    color: @fontColor;
    background-color: #202020;
    font-family: Avenir, Helvetica, Arial, sans-serif;
    height: auto;
    width: 100%;
    margin: 5px;
    resize: none;
    border: 0;
    outline: none;
    box-sizing: border-box;
  }
  .hidden {
    display: none;
  }
  .visible {
    display: inherit;
  }
}
</style>