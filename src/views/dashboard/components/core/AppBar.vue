<template>
  <v-app-bar
    absolute
    elevation="4"
    color="white"
    fixed
  >
    <v-container>
      <v-row>
        <v-col
          class="d-md-none"
          align-self="center"
        >
          <v-app-bar-nav-icon />
        </v-col>
        <v-col
          class="col"
          align-self="center"
        >
          <v-toolbar-title>
            <a
              href="/"
              class="black--text"
              style="text-decoration: none"
            >
              <img
                width="170"
                src="../../../../assets/nearLogo.png"
              >
            </a>
          </v-toolbar-title>
        </v-col>
        <v-col
          class="col d-none d-md-flex"
          align-self="center"
        >
          <a
            href="/app"
            style="text-decoration: none"
            class="black--text"
          >
            <span>Home &nbsp;&nbsp;</span>
          </a>
          <a
            href="/app#/pages/market"
            style="text-decoration: none"
            class="black--text"
          >
            <span>Libros &nbsp;&nbsp;</span>
          </a>
        </v-col>
        <v-spacer />
        <v-col
          class="col d-none d-sm-flex"
          align-self="center"
        >
          <div
            v-show="!sesion"
            class="my-2"
          >
            <v-btn
              color="#6868ac"
              large
              class="white--text"
              @click="signIn()"
            >
              Inicia Sesion Con Near
            </v-btn>
          </div>
          <div
            v-show="sesion"
            class="my-2"
          >
            <v-menu transition="slide-x-transition">
              <template v-slot:activator="{ on, attrs }">
                <v-btn
                  color="#6868ac"
                  class="ma-2 white--text"
                  v-bind="attrs"
                  v-on="on"
                >
                  {{ accountId }}
                </v-btn>
              </template>
              <v-list>
                <v-list-itemlink>
                  <v-list-item-title>
                    <router-link
                      class="black--text"
                      to="pages/user/"
                    >
                      Perfil
                    </router-link>
                  </v-list-item-title>
                  <v-list-item-title>
                    <router-link
                      class="black--text"
                      to="pages/user/"
                    >
                      Mis Libros
                    </router-link>
                  </v-list-item-title>
                  <v-list-item-title>
                    <router-link
                      class="black--text"
                      to="pages/product/registration/"
                    >
                      Publicar libro
                    </router-link>
                  </v-list-item-title>
                  <v-list-item-title @click="signOut()">
                    Cerrar Sesion
                  </v-list-item-title>
                </v-list-itemlink>
              </v-list>
            </v-menu>
          </div>
        </v-col>
      </v-row>
    </v-container>
  </v-app-bar>
</template>

<script>
  // Utilities
  import { mapState, mapMutations } from 'vuex'
  import * as nearAPI from 'near-api-js'
  import { CONFIG } from '@/services/api'
  const { connect, keyStores, WalletConnection } = nearAPI

  export default {
    name: 'DashboardCoreAppBar',
    data () {
      return {
        sesion: false,
        accountId: '',
      }
    },
    computed: {
      ...mapState(['drawer']),
    },
    mounted () {
      this.isSigned()
    },
    methods: {
      ...mapMutations({
        setDrawer: 'SET_DRAWER',
      }),
      async signIn () {
        // connect to NEAR
        const near = await connect(CONFIG(new keyStores.BrowserLocalStorageKeyStore()))
        // create wallet connection
        const wallet1 = new WalletConnection(near)
        wallet1.requestSignIn(
          'jochando.testnet', // contract requesting access
          'Near-BookShop', // optional
          'http://localhost:8080/app/#/', // optional
          'http://YOUR-URL.com/failure', // optional
        )
      },
      async isSigned () {
        // connect to NEAR
        const near = await connect(CONFIG(new keyStores.BrowserLocalStorageKeyStore()))
        // create wallet connection
        const wallet1 = new WalletConnection(near)
        if (wallet1.isSignedIn()) {
          this.sesion = true
          // returns account Id as string
          const walletAccountId = wallet1.getAccountId()
          this.accountId = walletAccountId
        }
      },
      async signOut () {
        // connect to NEAR
        const near = await connect(CONFIG(new keyStores.BrowserLocalStorageKeyStore()))
        // create wallet connection
        const wallet1 = new WalletConnection(near)

<<<<<<< HEAD
        wallet1.signOut()
=======
        wallet.signOut()
        this.sesion = false
>>>>>>> 27135c6d6d78f4de959c9c9523fd8bddb47e1262
        this.$router.go()
      },
    },
  }
</script>
