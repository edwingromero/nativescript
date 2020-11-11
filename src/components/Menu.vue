<template>
  <StackLayout ~drawerContent  backgroundColor="#ffffff">
    <Label class="drawer-item fa">{{'fa-address-book' | fonticon}} Contactos</Label>
    <Label class="drawer-item fa" @tap="$navigator.navigate('/home')">{{'fa-file-picture-o' | fonticon}} Galeria</Label>
    <Label class="drawer-item fa" @tap="$navigator.navigate('/home')">{{'fa-paper-plane' | fonticon}} Mensajes</Label>
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
