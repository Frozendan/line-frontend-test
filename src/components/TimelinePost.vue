<template>
    <v-row
        align="center"
        justify="center"
    >
        <v-toolbar>
            <v-spacer></v-spacer>
            <v-btn rounded color="normal" class="mr-2">Save draft</v-btn>
            <v-menu
                    v-model="menu"
                    :close-on-content-click="false"
                    :nudge-width="200"
                    offset-x
            >
                <template v-slot:activator="{ on }">
                    <v-btn
                        rounded
                        color="success"
                        v-on="on"
                    >
                       Schedule
                    </v-btn>
                </template>

                <v-card width="500">
                    <v-list>
                        <v-list-item>
                            <v-list-item-content class="d-flex flex-column align-items-start">
                                <v-list-item-title class="subheading">Publish date:</v-list-item-title>
                                <v-radio-group v-model="publishSchedule" :mandatory="true">
                                    <v-radio label="Publish Now" value="radio-1"></v-radio>
                                    <v-radio label="Radio 2" value="radio-2">
                                        <template v-slot:label>
                                            <v-form v-model="valid" class="w-100">
                                                <v-row>
                                                    <v-col
                                                        cols="12"
                                                        md="6"
                                                    >
                                                        <v-menu
                                                            v-model="publishDateMenu"
                                                            :close-on-content-click="false"
                                                            :nudge-right="40"
                                                            transition="scale-transition"
                                                            offset-y
                                                            min-width="290px"
                                                        >
                                                            <template v-slot:activator="{ on }">
                                                                <v-text-field
                                                                    v-model="publishDate"
                                                                    label="Date Publishing"
                                                                    readonly
                                                                    v-on="on"
                                                                ></v-text-field>
                                                            </template>
                                                            <v-date-picker v-model="publishDate" @input="publishDateMenu = false"></v-date-picker>
                                                        </v-menu>
                                                    </v-col>
                                                    <v-col
                                                        cols="12"
                                                        md="6"
                                                    >
                                                        <v-menu
                                                            ref="menu"
                                                            v-model="publishTimeMenu"
                                                            :close-on-content-click="false"
                                                            :nudge-right="40"
                                                            :return-value.sync="publishTime"
                                                            transition="scale-transition"
                                                            offset-y
                                                            max-width="290px"
                                                            min-width="290px"
                                                        >
                                                            <template v-slot:activator="{ on }">
                                                                <v-text-field
                                                                    v-model="publishTime"
                                                                    label="Time publishing"
                                                                    readonly
                                                                    v-on="on"
                                                                ></v-text-field>
                                                            </template>
                                                            <v-time-picker
                                                                v-if="publishTimeMenu"
                                                                v-model="publishTime"
                                                                full-width
                                                                @click:minute="$refs.menu.save(publishTime)"
                                                            ></v-time-picker>
                                                        </v-menu>
                                                    </v-col>
                                                </v-row>
                                            </v-form>
                                        </template>

                                    </v-radio>
                                </v-radio-group>
                            </v-list-item-content>
                        </v-list-item>
                    </v-list>

                    <v-card-actions>
                        <v-spacer></v-spacer>

                        <v-btn text @click="menu = false">Cancel</v-btn>
                        <v-btn color="primary" text @click="menu = false">Save</v-btn>
                    </v-card-actions>
                </v-card>
            </v-menu>
        </v-toolbar>
    </v-row>
</template>

<script>
    export default {
        name: "TimelinePost",
        data: () => ({
            menu: false,
            publishSchedule: '',
            valid: false,
            publishDateMenu: false,
            publishTimeMenu: false,
            publishDate: null,
            publishTime: null,
            nameRules: [
                v => !!v || 'Name is required',
                v => v.length <= 10 || 'Name must be less than 10 characters',
            ],
            email: '',
            emailRules: [
                v => !!v || 'E-mail is required',
                v => /.+@.+/.test(v) || 'E-mail must be valid',
            ],
        })
    }
</script>

<style scoped>

</style>