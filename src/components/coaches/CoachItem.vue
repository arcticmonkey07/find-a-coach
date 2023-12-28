<template>
  <li>
    <h3>{{ fullName }}</h3>
    <h4>${{ rate }}/час</h4>
    <div>
      <base-badge
        v-for="area in areas"
        :key="area"
        :type="area"
        :title="area"
      ></base-badge>
    </div>
    <div class="actions">
      <base-button mode="outline" link :to="coachContactLink"
        >Связаться</base-button
      >
      <base-button link :to="coachDetailsLink">Посмотреть детали</base-button>
    </div>
    <button class="close" @click="delCoach">X</button>
  </li>
</template>

<script>
export default {
  props: ['id', 'firstName', 'lastName', 'rate', 'areas'],
  computed: {
    fullName() {
      return this.firstName + ' ' + this.lastName;
    },
    coachContactLink() {
      return this.$route.path + '/' + this.id + '/contact';
    },
    coachDetailsLink() {
      return this.$route.path + '/' + this.id;
    },
  },
  methods: {
    delCoach() {
      this.$store.dispatch('coaches/delCoach', this.id);
    },
  },
};
</script>

<style scoped>
li {
  position: relative;
  margin: 1rem 0;
  border: 1px solid #424242;
  border-radius: 12px;
  padding: 1rem;
}

h3 {
  font-size: 1.5rem;
}

h3,
h4 {
  margin: 0.5rem 0;
}

div {
  margin: 0.5rem 0;
}

.actions {
  display: flex;
  justify-content: flex-end;
}

.close {
  position: absolute;
  top: 15px;
  right: 15px;
  padding: 5px 8px;
  font-size: 10px;
  color: #c0bebe;
  border: none;
  border-radius: 7px;
  background-color: rgb(160, 65, 65);
  cursor: pointer;
}
</style>
