<template>
  <div class="context-list" :class="{ 'icon-margin-bottom': iIcon }">
    <div class="list-heading" :class="{ 'icon-class': iIcon }">
      <div class="title">
        <EditImage
          v-if="iIcon"
          :src="iIcon"
          height="36"
          width="36"
          class="img"
        />
        <h2 class="title" contenteditable="true">{{ iTitle }}</h2>
      </div>
      <div
        class="button add"
        @click="add"
        :class="{ 'icon-margin-right': iIcon }"
      >
        +
      </div>
    </div>
    <ul ref="contextComponent">
      <ListItemAbout
        v-if="title === 'About me'"
        v-for="item in arry"
        :key="item.id"
      />
      <ListItemSkill
        v-if="title === 'Skill'"
        v-for="item in arry"
        :key="item.id"
      />
      <ListItemEducation
        v-if="title == 'Education'"
        v-for="item in arry"
        :key="item.id"
      />
      <ListItemExperience
        v-if="title == 'Working Experience'"
        v-for="item in arry"
        :key="item.id"
      />
      <ListItemInfo v-if="icon" v-for="item in arry" :key="item.id" />
      <slot name="listItem"></slot>
    </ul>
  </div>
</template>
<script>
import EditImage from "@/components/edit-image";
import ListItemAbout from "@/components/list-item-about";
import ListItemSkill from "@/components/list-item-skill";
import ListItemEducation from "@/components/list-item-education";
import ListItemExperience from "@/components/list-item-experience";
import ListItemInfo from "@/components/list-item-info";
export default {
  name: "ContextList",
  components: {
    EditImage,
    ListItemAbout,
    ListItemSkill,
    ListItemEducation,
    ListItemExperience,
    ListItemInfo
  },
  props: {
    title: {
      type: String,
      default: "Title"
    },
    icon: {
      type: String,
      default: ""
    }
  },
  data() {
    return {
      iTitle: this.title,
      iIcon: this.icon,
      arry: []
    };
  },
  methods: {
    parseFromJson(json, moduleName) {
      var _this = this;
      this.iTitle = this.iIcon = "";
      console.log(json);
      var length = this.$children.length;
      switch (moduleName) {
        case "social":
        case "contact":
          length--;
          break;
        default:
          break;
      }
      json.children.map((item, index) => {
        console.log(index, length);
        if (index >= length) {
          _this.add();
        }
      });

      this.$nextTick(() => {
        this.iTitle = json.title;
        this.iIcon = json.icon;

        this.$children.map((item, index) => {
          console.log(json.children[index], index, this.$children.length);
          if (item["parseFromJson"]) {
            item.parseFromJson(json.children[index]);
          }
        });
      });
    },
    toJson() {
      var json = Object.create(null);
      json.title = this.iTitle;
      json.icon = this.iIcon;
      json.c_name = "ContextList";
      var arr = [];
      this.$children.map((item, index) => {
        if (item["toJson"]) {
          if (item.toJson().c_name !== "EditImage") arr.push(item.toJson());
        }
      });
      json.children = arr;
      return json;
    },
    getData() {
      return this.arry;
    },
    showAdd() {
      this.add = true;
    },
    add() {
      this.arry.push(1);
    }
  }
};
</script>
<style lang="less">
.context-list {
  width: 100%;
  margin-bottom: 30px;

  .list-heading {
    display: flex;
    justify-content: space-between;
    align-items: center;

    .title {
      display: flex;
      align-items: center;

      .img {
        margin: 0 20px 0 50px;
      }
    }

    &:hover .add {
      display: block;
    }

    .add {
      display: none;
    }

    .button {
      width: 30px;
      height: 30px;
      line-height: 30px;
      text-align: center;
      font-size: 24px;
      border-radius: 50%;
      background: none;
      border: 1px solid #dad8d7;
      cursor: pointer;

      &:hover {
        background: #f2f2f2;
      }
    }
  }
}

.icon-class {
  background-color: #f6f7f7;
  border-bottom: 1px solid #e9e8e8;
}

.icon-margin-bottom {
  margin-bottom: 0;
}

.icon-margin-right {
  margin-right: 15px;
}
</style>
