<template>
  <v-container>
    <v-card color="basil">
      <v-tabs v-model="tab" background-color="transparent" color="basil" grow>
        <v-tab>NetWork</v-tab>
        <v-tab>Address</v-tab>
        <v-tab>Native</v-tab>
        <v-tab>Euro</v-tab>
      </v-tabs>
      <v-app v-if="tab == 0">
        <v-row
          class="d-flex justify-end mb-6"
          style="margin-top: 0px; margin-right: 15px; max-height: 0px"
        >
          <v-dialog v-model="dialog" persistent max-width="600px">
            <template v-slot:activator="{ on, attrs }">
              <v-btn color="primary" dark v-bind="attrs" v-on="on">ADD</v-btn>
            </template>
            <v-card>
              <v-card-title>
                <span class="text-h5">Add</span>
              </v-card-title>
              <v-card-text>
                <v-container>
                  <v-row>
                    <v-col cols="12">
                      <v-text-field
                        v-model="chainName"
                        label="Name*"
                        required
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12">
                      <v-text-field
                        v-model="chainID"
                        label="IP*"
                        required
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12">
                      <v-text-field
                        v-model="chainRPC"
                        label="RPC*"
                        required
                      ></v-text-field>
                    </v-col>
                  </v-row>
                </v-container>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="dialog = false"
                  >Close</v-btn
                >
                <v-btn color="blue darken-1" text @click="addNetwork"
                  >Save</v-btn
                >
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-row>
        <v-simple-table>
          <template v-slot:default>
            <thead>
              <tr>
                <th class="text-left">Name</th>
                <th class="text-left">IP</th>
                <th class="text-left">RPC</th>
                <th class="text-left">ACTION</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="item in networks" :key="item.id">
                <td>{{ item.name }}</td>
                <td>{{ item.chainID }}</td>
                <td>{{ item.RPC }}</td>
                <td>
                  <v-btn @click="deleteNetwork(item.chainID)" depressed color="error"
                    >Delete</v-btn
                  >
                </td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
      </v-app>
      <v-app v-if="tab == 1">

      </v-app>
    </v-card>
  </v-container>
</template>

<script>
import axios from "axios";
export default {
  name: "NetWork",

  data() {
    return {
      tab: 0,
      dialog: false,
      networks: null,
      chainID: null,
      chainName: null,
      chainRPC: null,
    };
  },
  created() {
    axios
      .get("http://localhost:3300/wallet/network/list")
      .then((response) => (this.networks = response.data));
  },
  methods: {
    addNetwork() {
      this.dialog = false;
      axios
        .post("http://localhost:3300/wallet/network/create", {
          chainID: this.chainID,
          chainName: this.chainName,
          chainRPC: this.chainRPC,
        })
        .then(function (response) {
          console.log(response);
          axios
            .get("http://localhost:3300/wallet/network/list")
            .then((response) => (this.networks = response.data));
        });
    },
    deleteNetwork(id) {
      axios.delete('http://localhost:3300/wallet/network/delete/'+ id)
      .then(response => {
        console.log(response),
        axios
            .get("http://localhost:3300/wallet/network/list")
            .then((response) => (this.networks = response.data));
        });
    },
  },
};
</script>
