<template>
    <v-app id="inspire">
        <v-navigation-drawer v-model="drawer"
                             app
                             class="mx"
                             color="grey lighten-3"
                             mini-variant
                             permanent>
            <div>
                <v-app-bar-nav-icon class="pl-5"></v-app-bar-nav-icon>
            </div>
            <v-spacer></v-spacer>
            <template>
                <v-list nav
                        dense>
                    <v-list-item v-for="item in navbarIcons"
                             :key="item.id"
                                 active-class="highlighted">
                        <v-list-item-icon >
                            <v-btn icon color="grey darken-2" class="pr-3" :to="item.to">
                                <v-icon>{{item.ico}}</v-icon>
                            </v-btn>
                        </v-list-item-icon>
                    </v-list-item>
                </v-list>
            </template>
            <v-spacer></v-spacer>
            <template v-slot:append>
                <v-list nav
                        dense>
                    <v-list-item>
                        <v-list-item-icon>
                            <v-btn icon color="grey darken-2" class="pr-3">
                                <v-icon>mdi-help-circle</v-icon>
                            </v-btn>
                        </v-list-item-icon>
                    </v-list-item>
                    <v-list-item>
                        <v-list-item-icon>
                            <v-btn icon color="grey darken-2" class="pr-3">
                                <v-icon>mdi-forum</v-icon>
                            </v-btn>
                        </v-list-item-icon>
                    </v-list-item>
                    <v-list-item>
                        <v-list-item-icon>
                            <v-btn icon color="grey darken-2" class="pr-3">
                                <v-icon>mdi-movie</v-icon>
                            </v-btn>
                        </v-list-item-icon>
                    </v-list-item>
                </v-list>
            </template>
        </v-navigation-drawer>

        <v-main>
            <v-card color="grey lighten-4"
                    flat
                    tile>
                <v-toolbar dense>
                    <v-row>
                        <v-toolbar-title class="pl-2 blue--text" >Im</v-toolbar-title>
                        <v-toolbar-title class="green--text">Works</v-toolbar-title>
                    </v-row>
                    

                    <v-spacer></v-spacer>

                    <v-btn icon>
                        <v-icon>mdi-home</v-icon>
                    </v-btn>

                    <v-btn icon>
                        <v-icon>mdi-bell</v-icon>
                    </v-btn>

                    <v-btn icon>
                        <v-icon>mdi-help-circle</v-icon>
                    </v-btn>

                    <v-btn icon>
                        <v-avatar color="grey" size=32></v-avatar>
                    </v-btn>
                </v-toolbar>
            </v-card>
            


        <router-view></router-view>


            
        </v-main>
        <v-footer >
            <v-spacer></v-spacer>Quick Access: <v-icon color="blue lighten-1">mdi-message</v-icon>Feedback |<v-icon color="blue lighten-1">mdi-help-circle</v-icon>Help Desk
        </v-footer>
    </v-app>
</template>

<script>
    export default {
        data: () => ({
            navbarIcons: [
                 
                { name: 'Dashboard', ico: 'mdi-monitor', id : 1,to:'/' },
                { name: 'Projects', ico: 'mdi-cash', id : 2 ,to:'/projects'},
                { name: 'Starred', ico: 'mdi-hand-heart', id: 3 },
                { name: 'Starred', ico: 'mdi-account-multiple', id: 4 },
                { name: 'Starred', ico: 'mdi-sitemap', id: 5 },
                { name: 'Starred', ico: 'mdi-chart-bar-stacked', id: 6 },
                { name: 'Starred', ico: 'mdi-file', id: 7 },
                { name: 'Starred', ico: 'mdi-progress-wrench', id: 8 },

            ],
            drawer: null,
            
            model: 0,
         })
}
</script>


