<template>
  <v-layout child-flex>
      <!-- buttons + เพื่อเพิ่มข้อมูลและdetails ในการทำงาน timesheet -->
    <v-btn bottom color="red lighten-2" dark fab fixed right buttom @click="dialog = !dialog">
      <v-icon>mdi-plus</v-icon>
    </v-btn>
    <!-- หัวขอแบบฟอร์ม-->
    <v-dialog v-model="dialog" width="800px">
      <v-card>
        <v-card-title color="white--text" class="orange lighten-5">Save my Rank</v-card-title>
        <v-container>
          <v-row class="mx-2">
            <v-col class="align-center justify-space-between" cols="12">
              <v-row align="center" class="mr-0">
                <v-avatar size="40px" class="mx-3">
                  <img src="//ssl.gstatic.com/s2/oz/images/sge/grey_silhouette.png" alt />
                </v-avatar>
                <v-text-field v-model="editedItem.name" placeholder="Name" />
              </v-row>
            </v-col>
            <v-col cols="6">
              <v-text-field v-model="editedItem.rank" placeholder="Rank" />
            </v-col>
            <v-col cols="6">
              <v-text-field
                v-model="editedItem.hero" prepend-icon="mdi-account-card-details-outline" placeholder="Hreo"/>
            </v-col>
            <v-col cols="6">
              <v-text-field v-model="editedItem.winrate" placeholder="WIN rate" />
            </v-col>
            <v-menu
              class="orange lighten-3"
              ref="menu"
              v-model="menu"
              :close-on-content-click="false"
              :return-value.sync="editedItem.date"
              transition="scale-transition"
              offset-y
              min-width="290px"
            >
              <template v-slot:activator="{ on }">
                <v-text-field
                  v-model="computedDateFormattedMomentjs"
                  label="Day / month / year"
                  prepend-icon="mdi-calendar"
                  readonly
                  v-on="on"
                ></v-text-field>
              </template>
              <v-date-picker v-model="editedItem.date" no-title scrollable>
                <v-spacer></v-spacer>
                <v-btn text color="red lighten-3" @click="menu = false">Cancel</v-btn>
                <v-btn color="green accent-1" @click="$refs.menu.save(editedItem.date)">Confirmed</v-btn>
              </v-date-picker>
            </v-menu>
            <v-col cols="12">
              <v-text-field v-model="editedItem.notes" prepend-icon="mdi-text" placeholder="Notes" />
            </v-col>
          </v-row>
        </v-container>
        <v-card-actions>
          <v-btn text color="blue-grey lighten-1">More</v-btn>
          <v-spacer />
          <v-btn color="red lighten-3" @click="close">Cancel</v-btn>
          <v-btn color="green accent-1" @click="save">Confirmed Save</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-data-table :headers="headers" :items="desserts" sort-by="calories" class="elevation-1">
      <template v-slot:top>
        <v-toolbar flat color="indigo lighten-3">
          <v-toolbar-title class="white--text">Information Level Rank</v-toolbar-title>
          <v-spacer />
        </v-toolbar>
      </template>
      <template v-slot:item.date="{ item }">{{item.date | formatDate }}</template>
      <template v-slot:item.action="{ item }">
        <v-icon small class="mr-2" @click="editItem(item)">mdi-pencil</v-icon>
        <v-icon small @click="deleteItem(item)">mdi-delete</v-icon>
      </template>
      <template v-slot:no-data>
        <v-btn color="orange lighten-4" @click="initialize">Refresh</v-btn>
      </template>
    </v-data-table>
  </v-layout>
</template>
<script>
import axios from "axios";
import * as moment from "moment";
export default {
  filters: {
    cuttext: function(val) {
      if (val && val.length > 60) {
        return val.substring(0, 60) + "...";
      } else return val;
    },
    formatDate: function(val) {
      if (val) {
        return moment(String(val)).format("DD-MMM-YYYY");
      }
    }
  },
  data: () => ({
    dialog: false,
    menu: false,
    modal: false,
    menu2: false,
    headers: [
      {
        text: "No.( )",
        align: "start",
        sortable: false,
        value: "id"
      },
      { text: "Name", value: "name" },
      { text: "Rank", value: "rank" },
      { text: "Hero", value: "hero" },
      { text: "Win rate", value: "winrate" },
      { text: "Date", value: "date" },
      { text: "Notes", value: "notes" },
      { text: "Actions", value: "action", sortable: false }
    ],
    desserts: [],
    editedIndex: -1,
    editedItem: {
      id: null,
      name: "",
      rank: "",
      hero: "",
      winrate: "",
      date: new Date().toISOString(),
      notes: ""
    },
    defaultItem: {
      id: null,
      name: "",
      rank: "",
      hero: "",
      winrate: "",
      date: new Date().toISOString(),
      notes: ""
    }
  }),
  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "Save my Rank" : "Edit Item";
    },
    computedDateFormattedMomentjs() {
      return this.editedItem.date
        ? moment(this.editedItem.date).format("DD-MM-YY")
        : "";
    }
  },
  watch: {
    dialog(val) {
      val || this.close();
    }
  },
  created() {
    this.initialize();
  },
  methods: {
    initialize: async function() {
      let res = await axios({
        method: "get",
        url: "http://localhost:3000/mane"
      });
      this.desserts = res.data;
    },
    editItem(item) {
      console.log(item);
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },
    deleteItem: async function(item) {
      const index = this.desserts.indexOf(item);
      let xurl = "http://localhost:3000/mane/" + item.id;
      confirm("Are you sure you want to delete this item?") &&
        (await axios({ method: "delete", url: xurl }));
      this.initialize();
    },
    close() {
      this.dialog = false;
      setTimeout(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      }, 300);
    },
    save: async function() {
      if (this.editedIndex > -1) {
        let xurl = "http://localhost:3000/mane/" + this.editedItem.id;
        await axios({
          method: "put",
          url: xurl,
          data: this.editedItem
        });
        this.initialize();
      } else {
        await axios({
          method: "post",
          url: "http://localhost:3000/mane",
          data: this.editedItem
        });
        this.initialize();
      }
      this.close();
    }
  }
};
</script>