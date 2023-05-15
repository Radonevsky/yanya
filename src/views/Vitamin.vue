<template>
  <ion-page>
    <ion-header >
      <ion-toolbar>
        <ion-title>Витамины</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content  class="ion-padding">
      <ion-datetime
        locale="ru-RU"
        :first-day-of-week="1"
        presentation="date"
      ></ion-datetime>
      <ion-button expand="block" id="open-modal">
        Настроить
        <ion-icon aria-hidden="true" icon='alarm.svg' class="drop-icon" style="margin-left: 10px;"/>
      </ion-button>
      <ion-modal ref="modal" trigger="open-modal">
        <ion-content>
          <ion-toolbar>
            <ion-title>Modal</ion-title>
            <ion-buttons slot="end">
              <ion-button color="light" @click="save()">Close</ion-button>
            </ion-buttons>
          </ion-toolbar>
          <ion-list>
            <ion-item>
              <ion-avatar slot="start">
                <ion-img src="https://i.pravatar.cc/300?u=b"></ion-img>
              </ion-avatar>
              <ion-label>
                <h2>Connor Smith</h2>
                <p>Sales Rep</p>
              </ion-label>
            </ion-item>
            <ion-item>
              <ion-avatar slot="start">
                <ion-img src="https://i.pravatar.cc/300?u=a"></ion-img>
              </ion-avatar>
              <ion-label>
                <h2>Daniel Smith</h2>
                <p>Product Designer</p>
              </ion-label>
            </ion-item>
            <ion-item>
              <ion-avatar slot="start">
                <ion-img src="https://i.pravatar.cc/300?u=d"></ion-img>
              </ion-avatar>
              <ion-label>
                <h2>Greg Smith</h2>
                <p>Director of Operations</p>
              </ion-label>
            </ion-item>
            <ion-item>
              <ion-avatar slot="start">
                <ion-img src="https://i.pravatar.cc/300?u=e"></ion-img>
              </ion-avatar>
              <ion-label>
                <h2>Zoey Smith</h2>
                <p>CEO</p>
              </ion-label>
            </ion-item>
          </ion-list>
        </ion-content>
      </ion-modal>
        <ion-row>
          <ion-text>
            <h4 class="justify-self-center">Оповещения:</h4>
          </ion-text>
        </ion-row>
        <ion-row>
          <div>
            <span>Кальций:</span>
            <ion-select interface="popover">
              <ion-select-option value="true">{{ time }}</ion-select-option>
              <ion-select-option value="false">Откл</ion-select-option>
            </ion-select>
          </div>
          <div>
            <span>Ежедневно в:</span>
            <ion-datetime interface="popover"
                          locale="ru-RU"
                          presentation="time"
            ></ion-datetime>
          </div>
        </ion-row>
    </ion-content>
  </ion-page>
</template>

<!--<script setup lang="ts">-->
<!--import {IonDatetime, IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonIcon} from '@ionic/vue';-->
<!--const settingsToggle = false-->
<!--function save() {-->

<!--}-->
<!--</script>-->

<script>
import {
  IonButtons,
  IonButton,
  IonModal,
  IonHeader,
  IonContent,
  IonToolbar,
  IonTitle,
  IonItem,
  IonList,
  IonAvatar,
  IonImg,
  IonLabel,
  IonPage,
  IonIcon,
} from '@ionic/vue';
import { defineComponent } from 'vue';

export default defineComponent({
  components: {
    IonButtons,
    IonButton,
    IonModal,
    IonHeader,
    IonContent,
    IonToolbar,
    IonTitle,
    IonItem,
    IonList,
    IonAvatar,
    IonImg,
    IonLabel,
    IonPage,
    IonIcon,
  },
  data() {
    return {
      alertsToggle: [
        {
          label: 'Вкл',
          value: true,
        },
        {
          label: 'Откл',
          value: false,
        }
      ],
      vitamins: [
        {
          name: 'calcium',
          title: 'Кальций',
          everyDay: true,
        },
        {
          name: 'd3',
          title: 'D3',
          everyDay: false,
          
        }
      ]
    }
  },
  methods: {
    dismiss() {
      this.$refs.modal.$el.dismiss();
    },
  },
});
</script>

<style>
ion-datetime {
    margin: 0 auto;
}
ion-row {
  justify-content: center;
  gap: 10px;
}
ion-button {
  display: block;
  max-width: 300px;
  margin: 0 auto;
}

ion-modal {
  --height: 50%;
  --border-radius: 16px;
  --box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
}

ion-modal::part(backdrop) {
  background: rgba(209, 213, 219);
  opacity: 1;
}

ion-modal ion-toolbar {
  --background: rgb(14 116 144);
  --color: white;
}
</style>