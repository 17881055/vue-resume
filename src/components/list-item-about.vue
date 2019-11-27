<template>
  <ListItem>
    <p contenteditable="true" ref="text">
      11Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris blandit
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
  name: "ListItemAbout",
  components: {
    ListItem
  },
  methods: {
    toJson() {
      var json = Object.create(null);
      json.text = this.$refs["text"].innerHTML;
      return json;
    }
  }
};
</script>
