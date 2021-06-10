<template>
  <v-container>
    <v-card color="basil">
      <v-tabs v-model="tab" background-color="transparent" color="basil" grow>
        <v-tab>NetWork</v-tab>
        <v-tab>Address</v-tab>
        <v-tab>Native</v-tab>
        <v-tab>Euro</v-tab>
      </v-tabs>
      <v-app v-if="tab==0">
        <v-row class="d-flex justify-end mb-6" style="    margin-top: 0px;margin-right: 15px;">
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
                      <v-text-field label="Name*" required></v-text-field>
                    </v-col>
                    <v-col cols="12">
                      <v-text-field label="IP*" required></v-text-field>
                    </v-col>
                    <v-col cols="12">
                      <v-text-field label="RPC*" required></v-text-field>
                    </v-col>
                  </v-row>
                </v-container>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="dialog = false">Close</v-btn>
                <v-btn color="blue darken-1" text @click="dialog = false">Save</v-btn>
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
              <tr v-for="item in desserts" :key="item.name">
                <td>{{ item.name }}</td>
                <td>{{ item.calories }}</td>
                <td>{{ item.calories }}</td>
                <td>
                  <v-btn depressed color="error">Delete</v-btn>
                </td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
      </v-app>
      <v-app v-if="tab==1">he</v-app>
    </v-card>
  </v-container>
</template>

<script>
export default {
  name: "NetWork",

  data() {
    return {
      tab: 0,
      dialog: false,
      desserts: [
        {
          name: "Frozen Yogurt",
          calories: 159
        },
        {
          name: "Ice cream sandwich",
          calories: 237
        },
        {
          name: "Eclair",
          calories: 262
        },
        {
          name: "Cupcake",
          calories: 305
        },
        {
          name: "Gingerbread",
          calories: 356
        },
        {
          name: "Jelly bean",
          calories: 375
        },
        {
          name: "Lollipop",
          calories: 392
        },
        {
          name: "Honeycomb",
          calories: 408
        },
        {
          name: "Donut",
          calories: 452
        },
        {
          name: "KitKat",
          calories: 518
        }
      ]
    };
  }
};
</script>
