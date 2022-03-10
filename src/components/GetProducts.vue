<template>
  <v-card class="mx-auto" max-width="1250">
    <v-card-header>
      <v-card-title>Mechanical Switches Table</v-card-title>
    </v-card-header> 
    <v-card-text>
      <v-table fixed-header>
        <template v-slot:default>
          <thead>
            <tr>
              <th class="text-left">Switch Name</th>
              <th class="text-left">Manufacturer</th>
              <th class="text-left">Color</th>
              <th class="text-left">Behavior</th>
              <th class="text-left">Actuation Force</th>
              <th class="text-left">Travel Distance</th>
              <th></th>
            </tr>
            
          </thead>
          <tbody>
            <tr v-for="row in switches" :key="row.id">
              <td>{{ row.switchName }}</td>
              <td>{{ row.manufacturer }}</td>
              <td>
                <div v-if="row.color === 'Red'">
                  <v-chip color="red">
                    {{ row.color }}
                  </v-chip>
                </div>
                <div v-else-if="row.color === 'Black'">
                  <v-chip color="black">
                    {{ row.color }}
                  </v-chip>
                </div>    
                <div v-else-if="row.color === 'Yellow' || row.color === 'Orange'">
                  <v-chip color="orange">
                    {{ row.color }}
                  </v-chip>
                </div>       
                <div v-else-if="row.color === 'Brown'">
                  <v-chip color="brown">
                    {{ row.color }}
                  </v-chip>
                </div>  
                <div v-else-if="row.color === 'Blue' || row.color === 'Navy'">
                  <v-chip color="blue">
                    {{ row.color }}
                  </v-chip>
                </div>      
                <div v-else-if="row.color === 'Green' || row.color === 'Jade'">
                  <v-chip color="green">
                    {{ row.color }}
                  </v-chip>
                </div>                                                                           
                <div v-else>
                  <v-chip color="indigo">
                    {{ row.color }}
                  </v-chip>
                </div>
              </td>
              <td>{{ row.behavior }}</td>
              <td>{{ row.actuationForce }}</td>
              <td>{{ row.travelDistance }}</td>
              <td>
                <v-btn size="small" color="indigo" @click="dialog = true">
                  Details
                </v-btn>
              </td>
            </tr>
          </tbody>
        </template>
      </v-table>
    </v-card-text> 
  </v-card>

  <v-dialog v-model="dialog">
    <v-card>
    <template>
      <v-tabs
        fixed-tabs
        background-color="indigo"
        dark
      >
        <v-tab>
          Option
        </v-tab>
        <v-tab>
          Another Selection
        </v-tab>
        <v-tab>
          Items
        </v-tab>
        <v-tab>
          Another Screen
        </v-tab>
      </v-tabs>
    </template>    
      <v-card-text>
        Coming Soon...
      </v-card-text>
      <v-card-actions>
        <v-btn color="indigo" block @click="dialog = false">
          Close Dialog
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>  
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      headers: [
        { text: "Switch Name", value: "switchName" },
        { text: "Manufacturer", value: "manufacturer" },
        { text: "Color", value: "color" },
        { text: "Behavior", value: "behavior" },
        { text: "ActuationForce", value: "actuationForce" },
        { text: "TravelDistance", value: "travelDistance" },
      ],
      switches: [],
      dialog: false,
    };
  },

  async created() {
    await axios
      .get("http://localhost:3100/api/products")
      .then((res) => {
        this.switches = res.data;
        console.log(res.data)
      })
      .catch((err) => {
        this.error.push(err);
      });
  },
};
</script>