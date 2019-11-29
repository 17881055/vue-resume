<template>
  <ListItem class="list-item-education">
    <div class="school">
      <span contenteditable="true">{{ dataSchool }}</span>
    </div>
    <div class="major">
      <span contenteditable="true">{{ dataMajor }}</span>
    </div>
    <div class="date">
      <span contenteditable="true">{{ dataTime }}</span>
    </div>
  </ListItem>
</template>
<script>
import ListItem from "@/components/list-item";
export default {
  name: "ListItemEducation",
  components: {
    ListItem
  },
  props: {
    school: {
      type: String,
      default: "Minjiang University"
    },
    major: {
      type: String,
      default: "Design"
    },
    date: {
      type: String,
      default: "2011.9 - 2015.6"
    }
  },
  data() {
    return {
      dataSchool: this.school,
      dataTime: this.date,
      dataMajor: this.major
    };
  },
  methods: {
    parseFromJson(json) {
      this.dataSchool = json.school;
      this.dataMajor = json.major;
      this.dataTime = json.date;
    },
    toJson() {
      var json = Object.create(null);
      json.c_name = "ListItemEducation";
      json.school = this.dataSchool;
      json.major = this.dataMajor;
      json.date = this.dataTime;
      return json;
    }
  }
};
</script>
<style lang="less">
.list-item-education {
  font-size: 18px;
  font-weight: bold;
  display: flex;
  justify-content: space-between;
  margin-bottom: 16px;

  .school {
    width: 40%;
  }

  .major {
    width: 35%;
  }

  .date {
    width: 25%;
    text-align: right;
    padding: 0 10px 0 0;
  }
}
</style>
