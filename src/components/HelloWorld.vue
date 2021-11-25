<template>
  <v-container>
    <v-card>
      <v-toolbar color="cyan" dark flat>
        <template v-slot:extension>
          <v-tabs v-model="model" centered slider-color="yellow">
            <v-tab v-for="i in 3" :key="i" :href="`#tab-${i}`">
              Item {{ i }}
            </v-tab>
          </v-tabs>
        </template>
      </v-toolbar>
      <v-tabs-items v-model="model">
        <v-tab-item v-for="i in 3" :key="i" :value="`tab-${i}`">
          <v-card flat>
            <div v-if="i === 1">
              <v-row
                class="text-center"
                justify="center"
                style="padding-top: 20px"
              >
                <v-col cols="6" sm="6" md="3">
                  <div class="text-center">
                    <v-menu top :close-on-content-click="closeOnContentClick">
                      <template v-slot:activator="{ on, attrs }">
                        <v-btn color="primary" dark v-bind="attrs" v-on="on">
                          Departure City
                        </v-btn>
                      </template>

                      <v-list>
                        <v-list-item v-for="(item, index) in city" :key="index">
                          <v-list-item-title>{{
                            item.title
                          }}</v-list-item-title>
                        </v-list-item>
                      </v-list>
                    </v-menu>
                  </div>
                </v-col>
                <v-col cols="6" sm="6" md="3">
                  <div class="text-center">
                    <v-menu top :close-on-content-click="closeOnContentClick">
                      <template v-slot:activator="{ on, attrs }">
                        <v-btn color="primary" dark v-bind="attrs" v-on="on">
                          Arrival City
                        </v-btn>
                      </template>

                      <v-list>
                        <v-list-item v-for="(item, index) in city" :key="index">
                          <v-list-item-title>{{
                            item.title
                          }}</v-list-item-title>
                        </v-list-item>
                      </v-list>
                    </v-menu>
                  </div>
                </v-col>
              </v-row>

              <v-row class="text-center" justify="center">
                <v-col cols="6" sm="6" md="3">
                  <div class="text-center">
                    <v-menu top :close-on-content-click="closeOnContentClick">
                      <template v-slot:activator="{ on, attrs }">
                        <v-btn color="primary" dark v-bind="attrs" v-on="on">
                          Departure Airport
                        </v-btn>
                      </template>

                      <v-list>
                        <v-list-item v-for="(item, index) in city" :key="index">
                          <v-list-item-title>{{
                            item.title
                          }}</v-list-item-title>
                        </v-list-item>
                      </v-list>
                    </v-menu>
                  </div>
                </v-col>
                <v-col cols="6" sm="6" md="3">
                  <div class="text-center">
                    <v-menu top :close-on-content-click="closeOnContentClick">
                      <template v-slot:activator="{ on, attrs }">
                        <v-btn color="primary" dark v-bind="attrs" v-on="on">
                          Arrival Airport
                        </v-btn>
                      </template>

                      <v-list>
                        <v-list-item v-for="(item, index) in city" :key="index">
                          <v-list-item-title>{{
                            item.title
                          }}</v-list-item-title>
                        </v-list-item>
                      </v-list>
                    </v-menu>
                  </div>
                </v-col>
              </v-row>

              <v-row class="text-center" justify="center">
                <v-col>
                  <div class="text-center" style="padding-bottom: 20px">
                    <v-menu top :close-on-content-click="closeOnContentClick">
                      <template v-slot:activator="{ on, attrs }">
                        <v-btn color="primary" dark v-bind="attrs" v-on="on">
                          Shipping company
                        </v-btn>
                      </template>

                      <v-list>
                        <v-list-item v-for="(item, index) in city" :key="index">
                          <v-list-item-title>{{
                            item.title
                          }}</v-list-item-title>
                        </v-list-item>
                      </v-list>
                    </v-menu>
                  </div>
                </v-col>
              </v-row>
            </div>
            <div v-if="i === 2">
              <v-row
                ><v-col cols="12" sm="6" md="4">
                  <v-dialog
                    ref="dialog"
                    v-model="modal"
                    :return-value.sync="date"
                    persistent
                    width="290px"
                  >
                    <template v-slot:activator="{ on, attrs }">
                      <v-text-field
                        v-model="date"
                        label="Picker in dialog"
                        prepend-icon="mdi-calendar"
                        readonly
                        v-bind="attrs"
                        v-on="on"
                      ></v-text-field>
                    </template>
                    <v-date-picker v-model="date" scrollable>
                      <v-spacer></v-spacer>
                      <v-btn text color="primary" @click="modal = false">
                        Cancel
                      </v-btn>
                      <v-btn
                        text
                        color="primary"
                        @click="$refs.dialog.save(date)"
                      >
                        OK
                      </v-btn>
                    </v-date-picker>
                  </v-dialog>
                </v-col>
                <v-spacer></v-spacer>
              </v-row>
            </div>
            <div v-if="i === 3">
              <validation-observer ref="observer" v-slot="{ invalid }">
                <form @submit.prevent="submit">
                  <validation-provider
                    v-slot="{ errors }"
                    name="Name"
                    rules="required|max:10"
                  >
                    <v-text-field
                      v-model="name"
                      :counter="10"
                      :error-messages="errors"
                      label="Name"
                      required
                    ></v-text-field>
                  </validation-provider>
                  <validation-provider
                    v-slot="{ errors }"
                    name="phoneNumber"
                    :rules="{
                      required: true,
                      digits: 7,
                      regex: '^(71|72|74|76|81|82|84|85|86|87|88|89)\\d{5}$',
                    }"
                  >
                    <v-text-field
                      v-model="phoneNumber"
                      :counter="7"
                      :error-messages="errors"
                      label="Phone Number"
                      required
                    ></v-text-field>
                  </validation-provider>
                  <validation-provider
                    v-slot="{ errors }"
                    name="email"
                    rules="required|email"
                  >
                    <v-text-field
                      v-model="email"
                      :error-messages="errors"
                      label="E-mail"
                      required
                    ></v-text-field>
                  </validation-provider>
                  <validation-provider
                    v-slot="{ errors }"
                    name="select"
                    rules="required"
                  >
                    <v-select
                      v-model="select"
                      :items="items"
                      :error-messages="errors"
                      label="Select"
                      data-vv-name="select"
                      required
                    ></v-select>
                  </validation-provider>
                  <validation-provider
                    v-slot="{ errors }"
                    rules="required"
                    name="checkbox"
                  >
                    <v-checkbox
                      v-model="checkbox"
                      :error-messages="errors"
                      value="1"
                      label="Option"
                      type="checkbox"
                      required
                    ></v-checkbox>
                  </validation-provider>

                  <v-btn class="mr-4" type="submit" :disabled="invalid">
                    submit
                  </v-btn>
                  <v-btn @click="clear"> clear </v-btn>
                </form>
              </validation-observer>
            </div>
          </v-card>
        </v-tab-item>
      </v-tabs-items>
    </v-card>
  </v-container>
</template>

<script>
import { required, digits, email, max, regex } from "vee-validate/dist/rules";
import {
  extend,
  ValidationObserver,
  ValidationProvider,
  setInteractionMode,
} from "vee-validate";

setInteractionMode("eager");

extend("digits", {
  ...digits,
  message: "{_field_} needs to be {length} digits. ({_value_})",
});

extend("required", {
  ...required,
  message: "{_field_} can not be empty",
});

extend("max", {
  ...max,
  message: "{_field_} may not be greater than {length} characters",
});

extend("regex", {
  ...regex,
  message: "{_field_} {_value_} does not match {regex}",
});

extend("email", {
  ...email,
  message: "Email must be valid",
});

export default {
  name: "HelloWorld",
  components: {
    ValidationProvider,
    ValidationObserver,
  },
  data: () => ({
    name: "",
    phoneNumber: "",
    email: "",
    select: null,
    items: ["Item 1", "Item 2", "Item 3", "Item 4"],
    checkbox: null,
    city: [
      { title: "Moscow" },
      { title: "Paris" },
      { title: "London" },
      { title: "Tokio" },
    ],
    closeOnContentClick: true,
    model: "tab-2",
    date: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
      .toISOString()
      .substr(0, 10),
    menu: false,
    modal: false,
    menu2: false,
  }),
  methods: {
    submit() {
      this.$refs.observer.validate();
    },
    clear() {
      this.name = "";
      this.phoneNumber = "";
      this.email = "";
      this.select = null;
      this.checkbox = null;
      this.$refs.observer.reset();
    },
  },
};
</script>
