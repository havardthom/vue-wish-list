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
          text: "Mitt ønske",
          href: "Link til mitt ønske"
        },
        {
          text: "Mitt ønske2",
          href: "Link til mitt ønske2"
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