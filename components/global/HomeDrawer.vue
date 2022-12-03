<template>
  <v-navigation-drawer permanent class="primary" dark app>
    <v-list v-for="(link, i) in items" :key="i">
      <v-list-item :to="link.to">
        <v-list-item-icon>
          <v-icon v-text="link.icon"></v-icon>
        </v-list-item-icon>
        <v-list-item-title>{{ link.text }} </v-list-item-title>
      </v-list-item>
    </v-list>
  </v-navigation-drawer>
</template>

<script>
export default {
  data() {
    return {
      mini: false,
      selectedItem: 0,
      items: [
        {
          text: 'Home',
          to: '/',
          icon: 'mdi-home',
        },
        {
          text: 'Eventos',
          to: '/event',
          icon: 'mdi-calendar',
        },
        {
          text: 'Sala',
          to: '/room',
          icon: 'mdi-sofa-single-outline',
        },
        {
          text: 'Sensores',
          to: '/sensor',
          icon: 'mdi-information',
        },
        {
          text: 'sensor data',
          to: '/sensordata',
          icon: 'mdi-information',
        },
      ],
    }
  },
}
</script>
