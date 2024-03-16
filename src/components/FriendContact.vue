<template>
  <li>
    <h2>{{ name }} {{ isFav ? "*" : "" }}</h2>
    <button @click="toggleDetails">
      {{ detailsAreVisible ? "Hide" : "Show" }} Details
    </button>
    <button @click="toggleFav">fav</button>
    <ul v-if="detailsAreVisible">
      <li><strong>Phone:</strong> {{ phoneNumber }}</li>
      <li><strong>Email:</strong> {{ emailAddress }}</li>
    </ul>
    <button @click="$emit('delete', id)">Delete</button>
  </li>
</template>

<script>
export default {
  // props: ['name', 'phone-number', 'email-address', 'isFav'],
  props: {
    id: {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    phoneNumber: String,
    emailAddress: String,
    isFav: {
      type: Boolean,
      required: false,
      default: false,
      // validator: function (value){
      //     return value === '1' || value === '0'
      // }
    },
  },
  emits: ["toggle-favorite", "delete"],
  // emits: {
  //     'toggle-favorite': (id)=> {
  //         if(id){
  //             return true
  //         }else{
  //             console.log('Id is missing');
  //             return false
  //         }
  //     }
  // },
  data() {
    return {
      detailsAreVisible: false,
    };
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    toggleFav() {
      this.$emit("toggle-favorite", this.id);
    },
  },
};
</script>
