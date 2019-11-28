<template>
  <ListItem class="list-item-info">
    <EditImage :src="dataImage" class="img"></EditImage>
    <span contenteditable="true">{{ dataTitle }}</span>
  </ListItem>
</template>
<script>
import ListItem from "@/components/list-item";
import EditImage from "@/components/edit-image";
export default {
  name: "ListItemInfo",
  components: {
    ListItem,
    EditImage
  },
  props: {
    image: {
      type: String,
      default: require("@/assets/social-github.png")
    },
    title: {
      type: String,
      default: "github.com/luosijie"
    }
  },
  data() {
    return {
      dataTitle: this.title,
      dataImage: this.image
    };
  },
  methods: {
    parseFromJson(json) {
      console.log(json);
      this.dataTitle = this.dataImage = "";
      this.$nextTick(() => {
        this.dataImage = json.image;
        this.dataTitle = json.title;
      });
    },
    toJson() {
      var json = Object.create(null);
      json.c_name = "ListItemInfo";
      json.image = this.dataImage;
      json.title = this.dataTitle;
      return json;
    }
  }
};
</script>
<style lang="less">
.list-item-info {
  display: flex;
  align-items: center;
  border-bottom: 1px solid #e9e8e8;
  height: 80px;

  .img {
    margin: 0 20px 0 50px;
  }

  span {
    font-size: 20px;
    color: #555;
  }
}
</style>
