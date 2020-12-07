<template>
  <div class="dashboard">
    <v-card class="fill-height"> 
        <v-toolbar dense class="pa-0">
          <v-toolbar-title>
                        <v-btn icon>
                            <v-icon color="blue" circle>mdi-file-document-outline</v-icon>
                        </v-btn>
                        Dashboard
           </v-toolbar-title>
        </v-toolbar>
        <v-card fluid>
          <v-row dense>
            <v-col v-for="card in tasks"
                   :key="card.name" xs="12" sm="12" md="12" lg="4" xl="4">
                    <v-card>
                      <v-row dense>
                        <v-col cols="8">
                          <v-card-title class="pa-3" >
                            <div class="headerClass">
                              {{card.name}}
                            </div>
                          </v-card-title>
                          <v-card-title class="pl-3 pt-0">{{card.progres}}%</v-card-title>
                          <v-card-subtitle class="pa-0 pl-3">Tasks {{card.sub1}}</v-card-subtitle>
                          <v-card-subtitle class="pa-3">Tasks {{card.sub2}}</v-card-subtitle>
                        </v-col>
                        <v-col cols="4">
                          <v-card-actions>
                            <v-row>
                              <v-col>
                                <div class="text-center">
                                  <v-spacer></v-spacer>
                                    <v-progress-circular :rotate="270"
                                                 :size="110"
                                                 :width="9"
                                                 :value="card.progres"
                                                 :color="card.color"
                                                 rounded
                                                 class="mt-6 mr-7">
                                                {{ card.progres }}%
                                    </v-progress-circular>
                                </div>
                              </v-col>
                            </v-row>
                          </v-card-actions>
                        </v-col>
                      </v-row>
                      <v-divider></v-divider>
                      <v-spacer></v-spacer>
                      
                    </v-card>
            </v-col>
          </v-row>
          <v-row><!-- second row-->
            <v-col class="notification" xs="12" sm="12" md="12" lg="4" xl="4"><!--notifcation -->
              <v-card style="overflow-y: auto; height:400px" >
                <v-row dense>
                  <v-col cols="6">
                    <h2 class="pt-2 pl-2"> Notifications</h2>
                  </v-col>
                  <v-col cols="6">
                    <v-select
                      :items="items"
                      label="Today"
                      solo
                      class="pr-2"></v-select>
                  </v-col>  
                </v-row>
                 <v-list three-line>
                  <v-list-item-group
                    v-model="selected"
                    active-class="blue--text"
                    multiple>
                    <template v-for="item in notifications">
                      <v-list-item :key="item.name" >
                        <template v-slot:default="{ active }">
                          <v-list-item-content >
                            <v-card>
                              <v-row class="pa-1">
                                <v-col sm="2" class="pa-1 pl-4">
                                <v-list-item-avatar color="blue lighten-2">
                                    <v-icon color="blue"
                                              dark outline>{{item.icon}}</v-icon>
                                </v-list-item-avatar>
                                </v-col>
                                <v-col sm="10" class="pa-1">
                                <v-row>
                                  <h3 class="pa-1">{{item.name}}</h3>
                                  {{item.date}}
                                </v-row>
                                <v-list-item-subtitle class="pa-1"
                                >{{item.text}}</v-list-item-subtitle>
                                </v-col>
                                
                              </v-row>
                            </v-card>
                          </v-list-item-content>
                        </template>
                      </v-list-item>
                    </template>
                  </v-list-item-group>
                </v-list>
    
              </v-card>
            </v-col><!-- end of notifcation -->
            <v-col class="tasks" xs="12" sm="12" md="12" lg="8" xl="8"><!--my tasks -->
              <v-card style="overflow-y: auto; height:400px">
                <v-row dense>
                  <v-col sm="8" lg="8">
                    <h2 class="pt-2 pl-2">My Tasks</h2>
                  </v-col>
                  <v-col cols="4">
                    <v-select
                      :items="items"
                      label="Overdue"
                      solo
                      class="pr-2"></v-select>
                  </v-col>  
                </v-row>
                 <v-list three-line>
                  <v-list-item-group
                    v-model="selected"
                    active-class="blue--text"
                    multiple>
                    <template v-for="item in mytasks">
                      <v-list-item :key="item.title">
                        <template v-slot:default="{ active }">
                          <v-list-item-content >
                            <v-card :class="item.border">
                                <v-row>
                                  <v-col sm="12" class="pl-5">
                                    <v-row>
                                      <h3 class="pr-3 pt-1 pl-3">{{item.title}}</h3>
                                      <v-btn small :color="item.colour">{{item.tag}}</v-btn>
                                      <v-spacer></v-spacer>
                                      {{item.date}}
                                      <v-btn icon class="pb-5" ><v-icon>mdi-dots-vertical</v-icon></v-btn>
                                    </v-row>
                                    <v-list-item-subtitle
                                    >{{item.desc}}</v-list-item-subtitle>
                                  </v-col> 
                                </v-row>
                            </v-card>
                          </v-list-item-content>
                        </template>
                      </v-list-item>
                    </template>
                  </v-list-item-group>
                </v-list>
    
              </v-card>
            </v-col> <!-- end of my tasks -->
          </v-row><!-- second row ends-->
          <v-row><!-- third row-->
            <v-col class="help"  xs="12" sm="12" md="12" lg="4" xl="4"><!-- help -->
              <v-card style="overflow-y: auto; height:450px">
                <v-row>
                  <v-col cols="12">
                    <h2 class="pt-2 pl-2"> Help Documentation</h2>
                  </v-col> 
                </v-row >
                 <v-list three-line >
                  <v-list-item-group
                    v-model="selected"
                    multiple >
                    <template v-for="item in help">
                      <v-list-item :key="item.name" >
                        <template v-slot:default="{ active }">
                          <v-list-item-content >
                            <v-card>
                                <v-row>
                                  <v-col sm="2" class="pa-1 pl-5">
                                  <v-list-item-avatar color="blue lighten-2">
                                      <v-icon color="blue"
                                                dark outline>{{item.icon}}</v-icon>
                                  </v-list-item-avatar>
                                  </v-col>
                                  <v-col sm="10" class="pa-1" >
                                  <v-row>
                                    <v-list-item-title v-text="item.name" class="pa-1"></v-list-item-title>
                                  </v-row>
                                  <v-list-item-subtitle class="pa-1"
                                  >{{item.desc}}</v-list-item-subtitle>
                                  </v-col> 
                            </v-row>
                            </v-card>
                          </v-list-item-content>
                        </template>
                      </v-list-item>
                    </template>
                  </v-list-item-group>
                </v-list>
    
              </v-card>
            </v-col><!-- end of help -->
            <v-col class="team" xs="12" sm="12" md="12" lg="8" xl="8"><!-- my team -->
              <v-card style="overflow-y: auto hidden; height:450px">
                <v-row dense>
                  <v-col cols="8">
                    <h2 class="pt-2 pl-2">My Team</h2>
                  </v-col>
                  <v-col cols="4">
                    <v-select
                      :items="items"
                      label="Sort Status"
                      solo
                      class="pr-2"
                      ></v-select>
                  </v-col>  
                </v-row>
                <v-data-table
                  :headers="headers"
                  :items="myteam"
                  :items-per-page="5"
                  :single-expand="singleExpand"
                  :expanded.sync="expanded"
                  item-key="name"
                  show-expand
                  class="elevation-1">
                  <template v-slot:item.name="{ item }">
                    <v-avatar color="grey" size="20px"></v-avatar> {{ item.name }}
                  </template>
                  <template v-slot:item.progress="{ item }">
                    <v-row  v-if= " item.progress === 100 ">
                    
                      <v-progress-linear
                                  color="red darken-2"
                                  rounded
                                  :value="item.progress"
                                  size=""
                                ></v-progress-linear>{{item.progress}}%
                    </v-row>
                    <v-row  v-else>
                    
                      <v-progress-linear
                                  color="purple lighten-2"
                                  rounded
                                  :value="item.progress"
                                  size=""
                                ></v-progress-linear>{{item.progress}}%
                    </v-row>
                  </template>
                  <template v-slot:expanded-item="{ headers, item }">
                    <td :colspan="headers.length">
                      More info about {{ item.name }}
                    </td>
                  </template>
                </v-data-table>
                 
                 <!-- <v-avatar color="grey" size="20px"></v-avatar>{{ item.name }}</td>
                  <v-progress-linear
                                  color="red darken-2"
                                  rounded
                                  :value="item.progress"
                                  size=""
                                ></v-progress-linear>{{item.progress}}%
                                
                                <v-col
                                    class="d-flex"
                                    cols="12"
                                    sm="3"
                                  >
                              <v-select></v-select></v-col> -->
              </v-card>
            </v-col> <!-- end of my teams -->
          </v-row><!-- third row ends-->
          
        </v-card>
    </v-card>
  </div>
</template>

<script>
    export default {
        data: () => ({
            
            tab: null,
            
            tasks: [
                { name: "Completed Tasks", progres: 70, color:'green', sub1:'Tasks Completed', sub2:"The tasks completion progress is increased to 70% out of 100%" },
                { name: "Active Taks", progres: 40, color:'orange', sub1:'Tasks Active', sub2:"The active tasks progress is decreased to 40% out of 100%" },
                { name: "Assigned Tasks", progres: 90, color:'blue', sub1:'Tasks Assigned', sub2:"The tasks assigned progress is increased to 90% out of 100%" },
            ],
            dialog: false,
            notifications:[
                { name:'Teach Each',text:'Neha Shekhar has assigned a task against this project', time:'8:03AM',icon:'mdi-folder-outline'},
                { name:'Subscriptions',text:'Your subscription is about to expire in 3 days', time:'8:03AM',icon:'mdi-cog'},
                { name:'IN- Southern Region',text:'Ben John have been invited to manage this workspace', time:'8:22AM',icon:'mdi-account-tie'},
                { name:'Event Planning Checklist',text:'Neha Shekhar has invited you to this initiative', time:'5:03AM',icon:'mdi-hexagon-multiple-outline'},
                { name:'Mission Home',text:'Your subscription is about to expire in 3 days', time:'7:38AM',icon:'mdi-folder-open-outline'},
            ],
            mytasks: [
                { title: 'Student Attendance', tag: 'Surveys',colour:'blue lighten-3',text:'blue--text ',date:'30/03/2019',desc:'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus condimentum leo est, in bibendum nisi dignissim nec.',border:'blueborder'},
                { title: 'Percentage of Plantation Cost', tag: 'Outcomes',colour:'red lighten-3',text:'red--text',date:'30/03/2019 ',desc:'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus condimentum leo est, in bibendum nisi dignissim nec.',border:'redborder'},
                { title: 'School Checkin', tag: 'Outcomes',colour:'red lighten-3',text:'red--text',date:'30/03/2019',desc:'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus condimentum leo est, in bibendum nisi dignissim nec.',border:'redborder'},
                { title: 'Reimbursement Form', tag: 'Surveys',colour:'blue lighten-3',text:'blue--text',date:'30/03/2019',desc:'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus condimentum leo est, in bibendum nisi dignissim nec.',border:'blueborder'},
                { title: 'Reimbursement Form', tag: 'Outputs',colour:'blue lighten-3',text:'blue--text',date:'30/03/2019',desc:'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus condimentum leo est, in bibendum nisi dignissim nec.',border:'blueborder'},
                { title: 'Reimbursement Form', tag: 'Outputs',colour:'green lighten-3',text:'green--text',date:'30/03/2019',desc:'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus condimentum leo est, in bibendum nisi dignissim nec.',border:'greenborder'},
            ],
            help:[
              {name:'Getting Started',icon:'mdi-format-list-bulleted-square',desc:'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus condimentum leo est, in bibendum nisi dignissim nec.'},
              {name:'Getting Started',icon:'mdi-format-list-bulleted-square',desc:'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus condimentum leo est, in bibendum nisi dignissim nec.'},
              {name:'Getting Started',icon:'mdi-format-list-bulleted-square',desc:'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus condimentum leo est, in bibendum nisi dignissim nec.'},
              {name:'Getting Started',icon:'mdi-format-list-bulleted-square',desc:'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus condimentum leo est, in bibendum nisi dignissim nec.'},
              {name:'Getting Started',icon:'mdi-format-list-bulleted-square',desc:'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus condimentum leo est, in bibendum nisi dignissim nec.'},
            ],
            model: 0,
            headers: [
              {
                text: 'Name',
                align: 'start',
                
                value: 'name',
              },
              { text: 'User Role', value: 'role',sortable: false, },
              { text: 'Task Counts', value: 'tcount',sortable: false, },
              { text: 'Progress', value: 'progress',sortable: false, },
              { text: 'Actions', value: 'data-table-expand' },
            ],
            myteam: [
              {name: 'Varun Mittal',role:'Admin',tcount:1,progress:92},
              {name: 'Ben John',role:'Volunteer',tcount:4,progress:50},
              {name: 'Neha Shekhar',role:'Finance Manager',tcount:6,progress:100},
              {name: 'Nadeem V',role:'Donor',tcount:1,progress:92},
              {name: 'Shivani Kumar',role:'Volunteer',tcount:4,progress:50},
              {name: 'Sneha Bansal',role:'Regional Manager',tcount:6,progress:100},
              {name: 'Varun Mittal',role:'Admin',tcount:1,progress:92},
              {name: 'Ben John',role:'Volunteer',tcount:4,progress:50},
              {name: 'Neha Shekhar',role:'Finance Manager',tcount:6,progress:100},
              {name: 'Nadeem V',role:'Donor',tcount:1,progress:92},
              {name: 'Shivani Kumar',role:'Volunteer',tcount:4,progress:50},
              {name: 'Sneha Bansal',role:'Regional Manager',tcount:6,progress:100},
            ],
            expanded: [],
            singleExpand: false,
         })
}
</script>

<style>
    .v-progress-circular {
        font-size:19px;
        font-weight:bold;
        color:black;
    }
    .v-list-item-title  {
        font-weight:bold;
    }
    div.v-card.v-sheet.theme--light.blueborder {
      background-color: #ffffff;
      border-left: 5px solid blue;
    }
    div.v-card.v-sheet.theme--light.redborder {
      background-color: #ffffff;
      border-left: 5px solid red;
    }
    div.v-card.v-sheet.theme--light.greenborder {
      background-color: #ffffff;
      border-left: 5px solid green;
    }
</style>