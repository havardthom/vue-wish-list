<template>
  <v-row>
    <v-col cols="6">
      <v-form
        v-model="valid"
      >
        <v-text-field
          v-model="wish"
          label="My wish"
          :rules="wishRules"
          required
        /> 
        <v-text-field
          v-model="wishLink"
          label="Link to wish"
        /> 
        <v-btn
          :disabled="!valid"
          @click="addWish"
        >
          Add wish
        </v-btn>
      </v-form>
    </v-col>
    <v-col cols="6">
      <v-list>
        <v-subheader>Wish List</v-subheader>
        <v-list-item
          v-for="(wish, idx) in wishes"
          :key="idx"
          two-line
        > 
          <v-list-item-content>
            <v-list-item-title>{{ wish.text }}</v-list-item-title>
            <v-list-item-subtitle>
              <a
                :href="wish.href"
                target="_blank"  
              >
                {{ wish.href }}
              </a>    
            </v-list-item-subtitle>
          </v-list-item-content>
          <v-list-item-action v-if="idx > 1">
            <v-btn 
              @click="removeWish(idx)"
              icon
            >
              <v-icon color="grey lighten-1">mdi-delete</v-icon>
            </v-btn>
          </v-list-item-action>
        </v-list-item>
      </v-list>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: "WishList",
  data () {
    return {
      valid: false,
      wish: '',
      wishRules: [
        v => !!v || 'Wish is required'
      ],
      wishLink: '',
      wishes: [
        {
          text: "Girlfriend",
          href: "https://www.google.com/search?q=girlfriend&oq=girlfriend&aqs=chrome..69i57j0l5.2978j0j9&sourceid=chrome&ie=UTF-8"
        },
        {
          text: "Cool friends",
          href: "https://www.google.com/search?ei=FYjJXbOVIeHQxgPEsbaADQ&q=cool+friends+for+sale&oq=cool+friends+for+sale&gs_l=psy-ab.3..33i22i29i30.4980.6297..6386...0.2..0.114.805.5j3......0....1..gws-wiz.......0i71j0i67j0j0i22i30j0i13i30.Q_VQmDL9CCM&ved=0ahUKEwjz8-qFxuLlAhVhqHEKHcSYDdAQ4dUDCAs&uact=5"
        }
      ]
    }
  },
  methods: {
    addWish () {
      this.wishes.push({
        text: this.wish,
        href: this.wishLink
      })
      this.wish = ''
      this.wishLink = ''
    },
    removeWish (idx) {
      this.wishes.splice(idx, 1)
    }
  },
  mounted () {
    if (localStorage.wishes) {
      this.wishes = JSON.parse(localStorage.wishes)
    }
  },
  watch: {
    wishes (newWishes) {
      localStorage.wishes = JSON.stringify(newWishes)
    }
  }
}
</script>