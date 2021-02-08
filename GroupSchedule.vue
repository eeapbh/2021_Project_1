<template>
  <div class="pa-5">
    <v-row>
      <v-col cols="12" md="6" class="mb-4">
        <v-row>
          <v-col cols="6">
            <v-menu
              ref="dateOpen"
              v-model="dateOpen"
              :close-on-content-click="false"
              :return-value.sync="start"
              offset-y
            >
              <template v-slot:activator="{ on }">
                <v-text-field
                  v-model="start"
                  label="Start Date"
                  prepend-icon="mdi-calendar"
                  dense
                  readonly
                  outlined
                  hide-details
                  v-on="on"
                ></v-text-field>
              </template>

              <v-date-picker v-model="start" no-title>
                <v-spacer />
                <v-btn text color="primary" @click="dateOpen = false"
                  >Cancel</v-btn
                >
                <v-btn text color="primary" @click="$refs.dateOpen.save(start)"
                  >OK</v-btn
                >
              </v-date-picker>
            </v-menu>
          </v-col>
          <v-col cols="6">
            <v-select
              v-model="type"
              :items="typeOptions"
              label="Type"
              class="my-auto"
              hide-details
              outlined
              dense
            ></v-select>
          </v-col>
        </v-row>
        <v-sheet height="500">
          <v-calendar
            :event-color="getEventColor"
            :events="events"
            :start="start"
            :type="type"
            @click:date="open"
            @click:event="showEvent"
            @click:more="moreEvent"
            @click:time="open"
            ref="calendar"
            v-model="start"
          ></v-calendar>
        </v-sheet>
      </v-col>
    </v-row>
    <Dialog />
  </div>
</template>

<script>
import Dialog from "@/components/group/Dialog.vue";
export default {
  components: {
    Dialog,
    },
  computed: {
    vuexGno() {
      return this.$store.getters.getGno;
    },
    vuexUno() {
      return this.$store.getters.getUno;
    },
    vuexBno() {
      return this.$store.getters.getBno;
    },
    vuexMemberStatus() {
      return this.$store.getters.getMemberStatus;
    },
  },
  watch: {
    vuexGno(val) {
      this.gno = val;
    },
    vuexUno(val) {
      this.uno = val;
    },
    vuexBno(val) {
      this.bno = val;
    },
    vuexMemberStatus(val) {
      this.memberStatus = val;
    },
  },
  created() {
    const today = new Date();
    console.log(today);
    const year = today.getFullYear();
    const month = today.getMonth();
    const date = today.getDate();
    const startDate = `${year}-${month}-${date}`;
    console.log(month);
    console.log(startDate);
  },

  data() {
    return {
      memberStatus: this.$store.getters.getMemberStatus,
      gno: this.$store.getters.getGno,
      bno: this.$store.getters.getBno,
      uno: this.$store.getters.getUno,
      dateOpen: false,
      start: this.startDate,
      type: "month",
      typeOptions: [
        { text: "Day", value: "day" },
        { text: "Week", value: "week" },
        { text: "Month", value: "month" },
      ],
    };
  },
  methods: {
    open(date) {
      console.log(date);
      this.$store.commit("OPEN_CALENDAR_DIALOG", date);
    },
  },
};
</script>
