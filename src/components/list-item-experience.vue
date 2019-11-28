<template>
  <ListItem class="list-item-experience">
    <div class="heading">
      <div class="company">
        <span contenteditable="true">{{ dataCompany }}</span>
      </div>
      <div class="job">
        <span contenteditable="true">{{ dataJob }}</span>
      </div>
      <div class="date">
        <span contenteditable="true">{{ dataTime }}</span>
      </div>
    </div>
    <p contenteditable="true" ref="text">
      Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris blandit
      metus in libero rutrum congue aliquam eu libero. Donec tristique est
      pharetra fringilla sollicitudin. Etiam eu ipsum vitae nulla tincidunt
      scelerisque semper id arcu. Phasellus quam tellus, laoreet id felis a,
      dignissim facilisis orci. Mauris feugiat vulputate quam quis tincidunt. In
      eleifend augue eu tristique bibendum. Donec gravida, eros sed iaculis
      iaculis, magna est finibus tortor, ultricies accumsan diam lorem non
      neque.
    </p>
  </ListItem>
</template>
<script>
import ListItem from "@/components/list-item";
export default {
  name: "ListItemExperience",
  components: {
    ListItem
  },
  props: {
    company: {
      type: String,
      default: "Google"
    },
    job: {
      type: String,
      default: "UI Desgner"
    },
    date: {
      type: String,
      default: "2011.9 - 2015.6"
    }
  },
  data() {
    return {
      dataCompany: this.company,
      dataTime: this.date,
      dataJob: this.job
    };
  },
  methods: {
    parseFromJson(json) {
      this.dataJob = json.job;
      this.dataCompany = json.company;
      this.dataTime = json.date;
      this.$refs["text"].innerHTML = json.text;
    },
    toJson() {
      var json = Object.create(null);
      json.c_name = "ListItemExperience";
      json.company = this.dataCompany;
      json.job = this.dataJob;
      json.date = this.dataTime;
      json.text = this.$refs["text"].innerHTML;
      return json;
    }
  }
};
</script>
<style lang="less">
.list-item-experience {
  .heading {
    font-size: 18px;
    font-weight: bold;
    display: flex;
    justify-content: space-between;
    margin-bottom: 12px;

    .company {
      width: 40%;
    }

    .job {
      width: 35%;
    }

    .date {
      width: 25%;
      text-align: right;
    }
  }
}
</style>
