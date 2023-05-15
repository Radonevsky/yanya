<template>
  <ion-page>
    <ion-tabs>
      <ion-router-outlet></ion-router-outlet>
      <ion-tab-bar slot="bottom">
        <ion-tab-button tab="vitamins" href="/tabs/vitamin">
          <ion-icon aria-hidden="true" icon='capsule.svg' />
          <ion-label>Витамины</ion-label>
        </ion-tab-button>

        <ion-tab-button tab="periods" href="/tabs/periods">
          <ion-icon aria-hidden="true" icon='droplet.svg' class="drop-icon" />
          <ion-label>Периоды</ion-label>
        </ion-tab-button>

      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</template>

<script setup lang="ts">
import { IonTabBar, IonTabButton, IonTabs, IonLabel, IonIcon, IonPage, IonRouterOutlet } from '@ionic/vue';
</script>

<style scoped lang="scss">
ion-tab-button.tab-selected .drop-icon {
    color: #c00d0d;
}
</style>