<template>
  <div>
    <v-simple-table :dense="dense" :fixed-header="fixedHeader" :height="height">
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left" v-for="head in headers" :key="head.title">{{ head.title }}</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in desserts" :key="item.name">
            <td class="sticky-col first-col">{{ item.name }}</td>
            <td class="sticky-col second-col">{{ item.ID }}</td>
            <!-- <td>{{ item.status }}</td> -->
            <td
              v-for="stats in item.status"
              :key="stats.id"
              v-bind:style="{ backgroundColor: newCol(stats[0]) }"
              v-if="!isEditing"
            >{{ stats[0] }}</td>
            <td v-else>
              <v-select
                v-model="stats[0]"
                :items="items"
                required
              >
              {{stats[0]}}
              </v-select>
            </td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>

    <v-row>
      <!-- <v-col cols="12" md="6">
        <v-text-field
          v-model="height"
          class="mx-4"
          label="Height - px"
          max="500"
          min="1"
          step="1"
          style="width: 125px"
          type="number"
          @keydown="false"
        ></v-text-field>
      </v-col>
      <v-col cols="6" md="3">
        <v-switch v-model="dense" label="Toggle dense" class="mx-4"></v-switch>
      </v-col>
      <v-col cols="6" md="3">
        <v-switch v-model="fixedHeader" label="Toggle fixed-header" class="mx-4"></v-switch>
      </v-col>-->
      <v-col cols="6" md="3" v-show="!isEditing">
        <v-btn @click="addNewEmp()">Add new Employee</v-btn>
      </v-col>
      <v-col cols="6" md="3">
        <v-btn 
          @click="editRoster()"
          v-if="!isEditing"
          :loading="loading"
          :disabled="loading"
        >
          Edit Roster
          <template v-slot:loader>
            <span>Loading...</span>
          </template>
        </v-btn>
        <v-btn 
          @click="updateRoster()" 
          v-else
          :loading="loading"
          :disabled="loading"
        >
          Update Roster
          <template v-slot:loader>
            <span>Loading...</span>
          </template>
        </v-btn>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  methods: {
    newCol(thing) {
      var col = "";
      switch (thing) {
        case "O":
          col = "PURPLE";
          break;
        case "G":
          col = "WHITE";
          break;
        case "B":
          col = "PINK";
          break;
        case "L":
        case "CO":
          col = "ORANGE";
          break;
        case "C":
          col = "GREEN";
          break;
        case "S":
          col = "RED";
          break;
        case "A":
          col = "BLUE";
          break;
        default:
          col = "WHITE";
          break;
      }
      return col;
    },
    addNewEmp() {
      this.desserts.push(this.desserts[this.desserts.length - 1]);
    },
    editRoster() {
      this.isEditing = true
      this.loader = 'loading'
    },
    updateRoster() {
      this.isEditing = false
    }
  },
  watch: {
    loader() {
      const l = this.loader
      this[l] = !this[l]

      setTimeout(() => (this[l] = false), 3000)
      this.loader = null
    }
  },
  data: () => ({
    select: null,
      items: [
        'G',
        'CO',
        'C',
        'S',
        'A',
        'B',
        'L',
        'O'
      ],
      loader: null,
        loading: false,
    isEditing: false,
    currStat: "O",
    dense: false,
    fixedHeader: true,
    height: 500,
    headers: [
      {
        title: "name"
      },
      {
        title: "ID"
      },
      {
        title: "1",
        day: "Friday"
      },
      {
        title: "2",
        day: "Saturday"
      },
      {
        title: "3",
        day: "Sunday"
      },
      {
        title: "4",
        day: "Monday"
      },
      {
        title: "5",
        day: "Tuesday"
      },
      {
        title: "6",
        day: "Wednesday"
      },
      {
        title: "7",
        day: "Thursday"
      },
      {
        title: "8",
        day: "Friday"
      },
      {
        title: "9",
        day: "Saturday"
      },
      {
        title: "10",
        day: "Sunday"
      },
      {
        title: "11",
        day: "Monday"
      },
      {
        title: "12",
        day: "Tuesday"
      },
      {
        title: "13",
        day: "Wednesday"
      },
      {
        title: "14",
        day: "Thursday"
      },
      {
        title: "15",
        day: "Friday"
      },
      {
        title: "16",
        day: "Saturday"
      },
      {
        title: "17",
        day: "Sunday"
      },
      {
        title: "18",
        day: "Monday"
      },
      {
        title: "19",
        day: "Tuesday"
      },
      {
        title: "20",
        day: "Wednesday"
      },
      {
        title: "21",
        day: "Thursday"
      },
      {
        title: "22",
        day: "Friday"
      },
      {
        title: "23",
        day: "Saturday"
      },
      {
        title: "24",
        day: "Sunday"
      },
      {
        title: "25",
        day: "Monday"
      },
      {
        title: "26",
        day: "Tuesday"
      },
      {
        title: "27",
        day: "Wednesday"
      },
      {
        title: "28",
        day: "Thursday"
      },
      {
        title: "29",
        day: "Friday"
      },
      {
        title: "30",
        day: "Saturday"
      }
    ],
    desserts: [
      {
        name: "Frozen Yogurt",
        ID: 159,
        status: {
          date_1: ["A", 1, "Friday", "Weekday"],
          date_2: ["G", 2, "Saturday", "Weekend"],
          date_3: ["B", 3, "Sunday", "Weekend"],
          date_4: ["B", 4, "Monday", "Weekday"],
          date_5: ["C", 5, "Tuesday", "Weekday"],
          date_6: ["L", 6, "Wednesday", "Weekday"],
          date_7: ["O", 7, "Thursday", "Weekday"],
          date_8: ["L", 8, "Friday", "Weekday"],
          date_9: ["S", 9, "Saturday", "Weekend"],
          date_10: ["O", 10, "Sunday", "Weekend"],
          date_11: ["A", 11, "Monday", "Weekday"],
          date_12: ["L", 12, "Tuesday", "Weekday"],
          date_13: ["S", 13, "Wednesday", "Weekday"],
          date_14: ["S", 14, "Thursday", "Weekday"],
          date_15: ["L", 15, "Friday", "Weekday"],
          date_16: ["A", 16, "Saturday", "Weekend"],
          date_17: ["O", 17, "Sunday", "Weekend"],
          date_18: ["B", 18, "Monday", "Weekday"],
          date_19: ["C", 19, "Tuesday", "Weekday"],
          date_20: ["C", 20, "Wednesday", "Weekday"],
          date_21: ["B", 21, "Thursday", "Weekday"],
          date_22: ["O", , 22, "Friday", "Weekday"],
          date_23: ["CO", 23, "Saturday", "Weekend"],
          date_24: ["S", 24, "Sunday", "Weekend"],
          date_25: ["B", 25, "Monday", "Weekday"],
          date_26: ["C", 26, "Tuesday", "Weekday"],
          date_27: ["S", 27, "Wednesday", "Weekday"],
          date_28: ["O", 28, "Thursday", "Weekday"],
          date_29: ["O", 29, "Friday", "Weekday"],
          date_30: ["L", 30, "Saturday", "Weekend"]
        }
      },
      {
        name: "Ice cream sandwich",
        ID: 237,
        status: {
          date_1: ["A", 1, "Friday", "Weekday"],
          date_2: ["G", 2, "Saturday", "Weekend"],
          date_3: ["B", 3, "Sunday", "Weekend"],
          date_4: ["B", 4, "Monday", "Weekday"],
          date_5: ["C", 5, "Tuesday", "Weekday"],
          date_6: ["L", 6, "Wednesday", "Weekday"],
          date_7: ["O", 7, "Thursday", "Weekday"],
          date_8: ["L", 8, "Friday", "Weekday"],
          date_9: ["S", 9, "Saturday", "Weekend"],
          date_10: ["O", 10, "Sunday", "Weekend"],
          date_11: ["A", 11, "Monday", "Weekday"],
          date_12: ["L", 12, "Tuesday", "Weekday"],
          date_13: ["S", 13, "Wednesday", "Weekday"],
          date_14: ["S", 14, "Thursday", "Weekday"],
          date_15: ["L", 15, "Friday", "Weekday"],
          date_16: ["A", 16, "Saturday", "Weekend"],
          date_17: ["O", 17, "Sunday", "Weekend"],
          date_18: ["B", 18, "Monday", "Weekday"],
          date_19: ["C", 19, "Tuesday", "Weekday"],
          date_20: ["C", 20, "Wednesday", "Weekday"],
          date_21: ["B", 21, "Thursday", "Weekday"],
          date_22: ["O", , 22, "Friday", "Weekday"],
          date_23: ["CO", 23, "Saturday", "Weekend"],
          date_24: ["S", 24, "Sunday", "Weekend"],
          date_25: ["B", 25, "Monday", "Weekday"],
          date_26: ["C", 26, "Tuesday", "Weekday"],
          date_27: ["S", 27, "Wednesday", "Weekday"],
          date_28: ["O", 28, "Thursday", "Weekday"],
          date_29: ["O", 29, "Friday", "Weekday"],
          date_30: ["L", 30, "Saturday", "Weekend"]
        }
      },
      {
        name: "Eclair",
        ID: 262,
        status: {
          date_1: ["A", 1, "Friday", "Weekday"],
          date_2: ["G", 2, "Saturday", "Weekend"],
          date_3: ["B", 3, "Sunday", "Weekend"],
          date_4: ["B", 4, "Monday", "Weekday"],
          date_5: ["C", 5, "Tuesday", "Weekday"],
          date_6: ["L", 6, "Wednesday", "Weekday"],
          date_7: ["O", 7, "Thursday", "Weekday"],
          date_8: ["L", 8, "Friday", "Weekday"],
          date_9: ["S", 9, "Saturday", "Weekend"],
          date_10: ["O", 10, "Sunday", "Weekend"],
          date_11: ["A", 11, "Monday", "Weekday"],
          date_12: ["L", 12, "Tuesday", "Weekday"],
          date_13: ["S", 13, "Wednesday", "Weekday"],
          date_14: ["S", 14, "Thursday", "Weekday"],
          date_15: ["L", 15, "Friday", "Weekday"],
          date_16: ["A", 16, "Saturday", "Weekend"],
          date_17: ["O", 17, "Sunday", "Weekend"],
          date_18: ["B", 18, "Monday", "Weekday"],
          date_19: ["C", 19, "Tuesday", "Weekday"],
          date_20: ["C", 20, "Wednesday", "Weekday"],
          date_21: ["B", 21, "Thursday", "Weekday"],
          date_22: ["O", , 22, "Friday", "Weekday"],
          date_23: ["CO", 23, "Saturday", "Weekend"],
          date_24: ["S", 24, "Sunday", "Weekend"],
          date_25: ["B", 25, "Monday", "Weekday"],
          date_26: ["C", 26, "Tuesday", "Weekday"],
          date_27: ["S", 27, "Wednesday", "Weekday"],
          date_28: ["O", 28, "Thursday", "Weekday"],
          date_29: ["O", 29, "Friday", "Weekday"],
          date_30: ["L", 30, "Saturday", "Weekend"]
        }
      },
      {
        name: "Cupcake",
        ID: 305,
        status: {
          date_1: ["A", 1, "Friday", "Weekday"],
          date_2: ["G", 2, "Saturday", "Weekend"],
          date_3: ["B", 3, "Sunday", "Weekend"],
          date_4: ["B", 4, "Monday", "Weekday"],
          date_5: ["C", 5, "Tuesday", "Weekday"],
          date_6: ["L", 6, "Wednesday", "Weekday"],
          date_7: ["O", 7, "Thursday", "Weekday"],
          date_8: ["L", 8, "Friday", "Weekday"],
          date_9: ["S", 9, "Saturday", "Weekend"],
          date_10: ["O", 10, "Sunday", "Weekend"],
          date_11: ["A", 11, "Monday", "Weekday"],
          date_12: ["L", 12, "Tuesday", "Weekday"],
          date_13: ["S", 13, "Wednesday", "Weekday"],
          date_14: ["S", 14, "Thursday", "Weekday"],
          date_15: ["L", 15, "Friday", "Weekday"],
          date_16: ["A", 16, "Saturday", "Weekend"],
          date_17: ["O", 17, "Sunday", "Weekend"],
          date_18: ["B", 18, "Monday", "Weekday"],
          date_19: ["C", 19, "Tuesday", "Weekday"],
          date_20: ["C", 20, "Wednesday", "Weekday"],
          date_21: ["B", 21, "Thursday", "Weekday"],
          date_22: ["O", , 22, "Friday", "Weekday"],
          date_23: ["CO", 23, "Saturday", "Weekend"],
          date_24: ["S", 24, "Sunday", "Weekend"],
          date_25: ["B", 25, "Monday", "Weekday"],
          date_26: ["C", 26, "Tuesday", "Weekday"],
          date_27: ["S", 27, "Wednesday", "Weekday"],
          date_28: ["O", 28, "Thursday", "Weekday"],
          date_29: ["O", 29, "Friday", "Weekday"],
          date_30: ["L", 30, "Saturday", "Weekend"]
        }
      },
      {
        name: "Gingerbread",
        ID: 356,
        status: {
          date_1: ["A", 1, "Friday", "Weekday"],
          date_2: ["G", 2, "Saturday", "Weekend"],
          date_3: ["B", 3, "Sunday", "Weekend"],
          date_4: ["B", 4, "Monday", "Weekday"],
          date_5: ["C", 5, "Tuesday", "Weekday"],
          date_6: ["L", 6, "Wednesday", "Weekday"],
          date_7: ["O", 7, "Thursday", "Weekday"],
          date_8: ["L", 8, "Friday", "Weekday"],
          date_9: ["S", 9, "Saturday", "Weekend"],
          date_10: ["O", 10, "Sunday", "Weekend"],
          date_11: ["A", 11, "Monday", "Weekday"],
          date_12: ["L", 12, "Tuesday", "Weekday"],
          date_13: ["S", 13, "Wednesday", "Weekday"],
          date_14: ["S", 14, "Thursday", "Weekday"],
          date_15: ["L", 15, "Friday", "Weekday"],
          date_16: ["A", 16, "Saturday", "Weekend"],
          date_17: ["O", 17, "Sunday", "Weekend"],
          date_18: ["B", 18, "Monday", "Weekday"],
          date_19: ["C", 19, "Tuesday", "Weekday"],
          date_20: ["C", 20, "Wednesday", "Weekday"],
          date_21: ["B", 21, "Thursday", "Weekday"],
          date_22: ["O", , 22, "Friday", "Weekday"],
          date_23: ["CO", 23, "Saturday", "Weekend"],
          date_24: ["S", 24, "Sunday", "Weekend"],
          date_25: ["B", 25, "Monday", "Weekday"],
          date_26: ["C", 26, "Tuesday", "Weekday"],
          date_27: ["S", 27, "Wednesday", "Weekday"],
          date_28: ["O", 28, "Thursday", "Weekday"],
          date_29: ["O", 29, "Friday", "Weekday"],
          date_30: ["L", 30, "Saturday", "Weekend"]
        }
      }
    ]
  })
};
</script>

<style lang="css" scoped>
/* .sticky-col {
    position: sticky;
    position: -webkit-sticky;    
    background-color: white;
}
  
.first-col {
	width: 100px;
    min-width: 100px;
    max-width: 100px;
	left: 0px;    
}

.second-col {
	width: 150px;
    min-width: 150px;
    max-width: 150px;
	left: 100px;    
} */
</style>