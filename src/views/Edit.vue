<template>
  <div>
    <div id="addActivitySection">
      <div class="inputSection">
        <input
          type="text"
          placeholder="Activity name..."
          v-model.number="activityName"
        /><span>Activity Name</span>
      </div>
      <div class="inputSection">
        <input
          type="number"
          min="0"
          placeholder="hh"
          v-model.number="avgHours"
        /><span>Avg Hours</span>
      </div>
      <div class="inputSection">
        <input
          type="number"
          min="0"
          placeholder="mm"
          v-model.number="avgMinutes"
        /><span>Avg Minutes</span>
      </div>
      <div class="inputSection">
        <input
          type="number"
          min="0"
          placeholder="ss"
          v-model.number="avgSeconds"
        /><span>Avg Seconds</span>
      </div>
    </div>

    <button
      type="button"
      @click="addAction(activityName, getTotalSeconds())"
      :disabled="isAddDisabled()"
    >
      Add
    </button>

    <b-list-group>
      <b-list-group-item
        v-for="(option, index) in activityOptions"
        :key="index"
        class="d-flex align-items-center"
      >
        <span class="flex-grow-1">{{ option.action }}</span>
        <b-button variant="danger" @click="deleteAction(index)"> X </b-button>
      </b-list-group-item>
    </b-list-group>
  </div>
</template>

<script>
export default {
  name: "Edit",
  props: {
    activityOptions: Array,
    deleteAction: Function,
    addAction: Function
  },
  data: function() {
    return {
      activityName: "",
      avgHours: 0,
      avgMinutes: 0,
      avgSeconds: 0
    };
  },
  methods: {
    isAddDisabled() {
      return !(
        this.activityName !== "" &&
        (this.avgHours || this.avgMinutes || this.avgSeconds)
      );
    },
    getTotalSeconds() {
      return this.avgHours * 60 * 60 + this.avgMinutes * 60 + this.avgSeconds;
    }
  }
};
</script>

<style scoped>
#addActivitySection {
  margin: 0 25%;
}

button.btn.btn-danger {
  float: right;
}
</style>
