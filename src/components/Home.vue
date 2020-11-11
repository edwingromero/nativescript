<template>
  <Page>
    <ActionBar>
      <GridLayout width="100%" columns="auto, *">
        <Label class="fa fa-lg" :text="'fa-bars' | fonticon" @tap="$refs.drawer.nativeView.showDrawer()" col="0"/>
        <Label class="title" text="Agenda 2020"  col="1"/>
      </GridLayout>
    </ActionBar>

    <RadSideDrawer ref="drawer" >
      <Menu />
      <GridLayout ~mainContent columns="*" rows="*" backgroundColor="#eee">
        <ListView for="pokemon in pokemones" separatorColor="transparent" @loadMoreItems="loadMorePokemones">
          <v-template>
            <StackLayout  flexDirection="row" >
              <GridLayout rows="auto, auto" class="Pokemones" margin="10"
                borderRadius="20"
                androidElevation="12">
                <Image row="0" class="Pokemones_imagen" :src="pokemon.image"/>
                <Label row="1" class="Pokemones_titulo" :text="pokemon.name" />
              </GridLayout>

              
            </StackLayout >
          </v-template>
        </ListView>
      </GridLayout>
    </RadSideDrawer>
  </Page>
</template>

<script>
const POKEAPI = "https://pokeapi.co/api/v2";
import Menu from './Menu'
import axios from "axios/dist/axios";

export default {
  components: {
    Menu
  },
  mounted() {
    this.loadPokemones();
  },
  data() {
    return {
      pokemones:[],
      offset:0,
      limit:20
    }
  },
  methods: {
    loadMorePokemones(){
      this.offset += this.limit;
      this.loadPokemones();
    },
    loadPokemones(){
      let vue = this;
      axios.get(POKEAPI+`/pokemon?offset=${vue.offset}&limit=${vue.limit}`)
      .then(res => {
        res.data.results.map((item) => {
          const id = item.url.split("/")[6];
          let pokemon =  {
            id,
            name: item.name,
            image:`https://img.pokemondb.net/artwork/vector/large/${item.name}.png`
          };
          vue.pokemones.push(pokemon);
        });
      })
      .catch(err => {
        console.error(err); 
      })      
    }
  },
}
</script>


<style lang="scss">

  .Pokemones{
    padding:20;
    margin:20 20 0 20;
    background-color: white;
    &_imagen{
      padding: 10;
      width: 65%;
    }
    &_titulo{
      text-align: center;
      font-size: 25;
    }
  }
</style>