<template>
  <Page>
    <ActionBar>
      <GridLayout width="100%" columns="auto, *">
        <Label text="Menu" @tap="$refs.drawer.nativeView.showDrawer()" col="0"/>
        <Label class="title" text="Bievenido al ap"  col="1"/>
      </GridLayout>
    </ActionBar>

    <RadSideDrawer ref="drawer">
      <Menu />
      <GridLayout ~mainContent columns="*" rows="*">
          <StackLayout verticalAlignment="center">

            <Label class="h1 text-center"  text="Bienvenido" />
            
          </StackLayout> 
      </GridLayout>
    </RadSideDrawer>
  </Page>
</template>

<script>
import Menu from './Menu'
export default {
  components: {
    Menu
  },
  methods: {
    
  },
}
</script>
