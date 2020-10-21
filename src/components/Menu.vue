<template>
  <StackLayout ~drawerContent backgroundColor="#ffffff">
      <Label class="drawer-header" text="Drawer"/>
      <Label class="drawer-item" text="Contactos"/>
      <Label class="drawer-item" text="Formulario"/>
      <Label class="drawer-item" text="Acerca de" @tap="$navigator.navigate('/home')"/>
  </StackLayout>
</template>

<script>

export default {
  methods: {
    onAppTap(){
      this.$navigator.navigate('/home')
    }
    
  },
}
</script>