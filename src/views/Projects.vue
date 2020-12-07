<template>
    <div>
     <v-card color="grey lighten-4"
                    flat
                    tile
                    class="pa-0 fill-height">
         <v-toolbar dense class="pa-0">
          <v-toolbar-title>
                        <v-btn icon>
                            <v-icon color="blue" circle>mdi-file-document-outline</v-icon>
                        </v-btn>
                        Projects
           </v-toolbar-title>
               <v-row>
                    <v-spacer></v-spacer>
                        <v-col class="d-flex pt-11 pl-10" cols="2">
                            <v-dialog v-model="dialog"
                                      width="600">
                                <template v-slot:activator="{ on, attrs }">
                                    <v-btn small
                                           color="success"
                                           dark
                                           v-bind="attrs"
                                           v-on="on">
                                        Create Project
                                    </v-btn>
                                </template>
                                <v-card>
                                    <v-card-actions>
                                        <v-spacer></v-spacer>
                                        <v-btn icon color="grey"
                                               @click="dialog = false">
                                            X
                                        </v-btn>
                                    </v-card-actions>
                                    
                                    <v-divider></v-divider>
                                    <div>
                                        <v-carousel v-model="model" :show-arrows="false">
                                            <v-carousel-item v-for="card in carousel"
                                                             :key="card.text">
                                                <v-sheet color=white
                                                         height="100%"
                                                         tile>
                                                         <v-card>
                                                            <v-img
                                                              src="https://picsum.photos/350/165?random"
                                                              height="350"
                                                              class="grey darken-4"
                                                            ></v-img>
                                                         </v-card>
                                                    <v-spacer></v-spacer>
                                                    <v-row denseclass="fill-height" align="center"
                                                            justify="center" single-line> 
                                                        <h3>{{card.text}}</h3>
                                                        <h4>{{card.subt}}</h4>
                                                    </v-row>
                                                    <v-row align="center"
                                                            justify="center">
                                                        <v-btn text outlined color="grey">Back</v-btn>
                                                        <v-btn text color="blue" outlined>Next</v-btn>
                                                    </v-row>
                                                </v-sheet>
                                                
                                            </v-carousel-item>
                                        </v-carousel>
                                    </div>
                                </v-card>
                            </v-dialog><!-- Carousel  -->
                        </v-col>
                        <v-col class="d-flex pt-10" cols="2">
                            <v-select :items="items"
                                      label="Bulk Actions"
                                      outlined
                                      dense></v-select>
                        </v-col>
                        <v-col class="d-flex pt-10" cols="3">
                            <v-text-field dense
                                          placeholder="Search"
                                          solo
                                          append-icon="mdi-magnify">
                            </v-text-field>
                        </v-col>
                        <v-col class="d-flex pt-10" cols="2">
                            <v-select :items="filter"
                                      icon
                                      label="Filters"
                                      outlined
                                      dense
                                      append-icon="mdi-filter"></v-select>
                        </v-col>
                        <v-col class="d-flex pt-11 mr-6" cols="1">

                            <v-btn class="ma-1" small outlined color="grey">
                                <v-icon>mdi-apps</v-icon>
                            </v-btn>
                            <v-btn class="ma-1" small outlined color="grey">
                                <v-icon>mdi-tune-vertical</v-icon>
                            </v-btn>
                        </v-col>
                    </v-row>   
                </v-toolbar>
                <v-toolbar>
                    <template>
                        <v-tabs v-model="tab"
                                centered
                                dense
                                active-class="highlighted">

                            <v-tab v-for="item in items" :key="item">
                                {{ item }}
                            </v-tab>
                        </v-tabs>
                    </template>
                </v-toolbar>
            </v-card>
            <v-spacer></v-spacer>
            
          <v-tabs-items v-model="tab">
          <v-tab-item>
            <v-card fluid>
                <v-row dense>
                    <v-col v-for="card in projects"
                           :key="card.name" sm="12" lg="3">
                        <v-card>
                            <v-row dense>
                                <v-col cols="1" class="pt-3 pl-2">
                                    <v-btn icon  class="pt-5">
                                        <v-icon color="blue">mdi-folder</v-icon>
                                    </v-btn>
                                </v-col>
                                <v-col cols="9">
                                    <v-card-title >
                                        <div class="headerClass">
                                            {{card.name}}
                                        </div>
                                    </v-card-title>
                                    <v-card-subtitle>Span: {{card.span}}</v-card-subtitle>
                                </v-col>
                                <v-col cols="2">
                                    <v-row>
                                        <v-checkbox v-model="checkbox"></v-checkbox>
                                        <v-icon>mdi-dots-vertical</v-icon>
                                    </v-row>
                                </v-col>
                            </v-row>
                            <v-divider></v-divider>
                            <v-spacer></v-spacer>
                            <v-card-actions>
                                <v-row>
                                    <v-col cols="8" class="pa-2">
                                        <v-list nav
                                                dense>
                                            <v-list-item>
                                                <v-list-item-icon>
                                                    <v-icon color="grey darken-2">mdi-tag-multiple</v-icon>
                                                </v-list-item-icon>
                                                <v-list-item-content>
                                                    <v-list-item-title></v-list-item-title>
                                                    <v-list-item-subtitle>Tag: {{card.tags}}</v-list-item-subtitle>
                                                </v-list-item-content>
                                            </v-list-item>
                                            <v-list-item>
                                                <v-list-item-icon>
                                                    <v-icon color="grey darken-2">mdi-account</v-icon>
                                                </v-list-item-icon>
                                                <v-list-item-content>
                                                    <v-list-item-title></v-list-item-title>
                                                    <v-list-item-subtitle>Team:</v-list-item-subtitle>
                                                </v-list-item-content>
                                            </v-list-item>
                                            <v-list-item>
                                                <v-list-item-icon>
                                                    <v-icon color="grey darken-2">mdi-wallet</v-icon>
                                                </v-list-item-icon>
                                                <v-list-item-content>
                                                    <v-list-item-title></v-list-item-title>
                                                    <v-list-item-subtitle>Budget: ${{card.budget}}</v-list-item-subtitle>
                                                </v-list-item-content>
                                            </v-list-item>
                                        </v-list>
                                    </v-col>
                                    <v-col cols="4" class="pa-1">
                                        <div class="text-center">
                                            <v-spacer></v-spacer>
                                            <v-progress-circular :rotate="270"
                                                                 :size="100"
                                                                 :width="5"
                                                                 :value="card.progres"
                                                                 color="teal"
                                                                 class="mt-6 mr-7">
                                                {{ card.progres }}% Progress
                                            </v-progress-circular>
                                        </div>
                                    </v-col>
                                </v-row>
                            </v-card-actions>
                        </v-card>
                    </v-col>
                </v-row>
            </v-card>
          </v-tab-item>
        <v-tab-item>
            <v-card flat>
             <v-card-title class="headline">
                 An awesome title
             </v-card-title>
            <v-card-text>
                <p>
                  Duis lobortis massa imperdiet quam. Donec vitae orci sed dolor rutrum auctor. Vestibulum facilisis, purus nec pulvinar iaculis, ligula mi congue nunc, vitae euismod ligula urna in dolor. Praesent congue erat at massa.
                </p>

                <p>
                  Aenean posuere, tortor sed cursus feugiat, nunc augue blandit nunc, eu sollicitudin urna dolor sagittis lacus. Pellentesque egestas, neque sit amet convallis pulvinar, justo nulla eleifend augue, ac auctor orci leo non est. Etiam sit amet orci eget eros faucibus tincidunt. Donec sodales sagittis magna.
                </p>

                <p class="mb-0">
                  Ut leo. Suspendisse potenti. Duis vel nibh at velit scelerisque suscipit. Fusce pharetra convallis urna.
                </p>
            </v-card-text>
            </v-card>
        </v-tab-item>
        <v-tab-item>
        <v-card flat>
          <v-card-title class="headline">
            An even better title
          </v-card-title>
          <v-card-text>
            <p>
              Maecenas ullamcorper, dui et placerat feugiat, eros pede varius nisi, condimentum viverra felis nunc et lorem. Sed hendrerit. Maecenas malesuada. Vestibulum ullamcorper mauris at ligula. Proin faucibus arcu quis ante.
            </p>

            <p class="mb-0">
              Etiam vitae tortor. Curabitur ullamcorper ultricies nisi. Sed magna purus, fermentum eu, tincidunt eu, varius ut, felis. Aliquam lobortis. Suspendisse potenti.
            </p>
          </v-card-text>
        </v-card>
        </v-tab-item>
    </v-tabs-items>
      
    </div>
</template>



<script>
    export default {
        data: () => ({
            
            tab: null,
            items: [
                'Draft', 'Deployed', 'Completed', 'Archived',
            ],
            projects: [
                { name: "Mahila Kisan Sasha", tags: 'Sample', budget: 40000, progres: 70,span:"10-08-20 to 20-08-21" },
                { name: "Teach Each", tags: 'Hospital', budget: 20000, progres: 25, span: "11-08-20 to 21-08-21" },
                { name: "Mission Home", tags: 'Hospital', budget: 30000, progres: 90, span: "12-08-20 to 22-08-21" },
                { name: "Fund Raiser Events", tags: 'Hospital', budget: 60000, progres: 50, span: "13-08-20 to 23-08-21" },
            ],
            dialog: false,
            carousel: [
                {text:'Welcome to ImWorks',subt:'Lorem ipsum dolor sit amet, consectetur adipiscing elit.  Duis vel nibh at.'},
                {text:'Manage Multiple Workspaces with Ease ',subt:'Lorem ipsum dolor sit amet, consectetur adipiscing elit.'},
                {text:'Easy Collaboration with Team Members',subt:'Lorem ipsum dolor sit amet, consectetur adipiscing elit.'},
                {text:'Welcome to ImWorks',subt:'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis vel nibh at velit scelerisque suscipit.'},
                {text:'Welcome to ImWorks',subt:'Lorem ipsum dolor sit amet, consectetur adipiscing elit.  Duis vel nibh at velit scelerisque suscipit.'},
            ],
            model: 0,
         })
}
</script>

<style>
    .headerClass {
        white-space: nowrap;
        word-break: normal;
        overflow: hidden;
        text-overflow: ellipsis;
    }
    h3{
        color: black;
    }
    h4{
        color:black;
        font-weight:normal;
    }
</style>