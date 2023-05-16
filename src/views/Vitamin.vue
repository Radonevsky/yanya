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
        Изменить
        <ion-icon aria-hidden="true" icon='alarm.svg' style="margin-left: 10px;"/>
      </ion-button>
      <ion-modal ref="modal" trigger="open-modal" @trata="setCalciumFreq">
        <ion-content>
          <ion-toolbar>
            <ion-title>Оповещения</ion-title>
            <ion-buttons slot="end">
              <ion-button color="light" @click="dismiss">
                <ion-icon aria-hidden="true" icon='close.svg' class="ali"/>
              </ion-button>
            </ion-buttons>
          </ion-toolbar>
          <ion-list>
            <ion-item>
              <ion-avatar slot="start">
                <ion-img src="calcium.jpeg"></ion-img>
              </ion-avatar>
              <ion-label>
                <h2>Кальций</h2>
              </ion-label>
              
              <ion-select
                justify="end"
                value="twice"
                id="calciumFreq"
                interface="action-sheet"
                slot="end"
                aria-label="Кальций"
                style="min-width: 140px;"
                v-model="calciumFreq">
                <ion-select-option value="once">Один раз в день</ion-select-option>
                <ion-select-option value="twice">Два раза в день</ion-select-option>
                <ion-select-option value="off">Откл</ion-select-option>
              </ion-select>
              
              <ion-datetime-button datetime="time" presentation="time"></ion-datetime-button>
              
              <ion-modal :keep-contents-mounted="true">
                <ion-datetime
                  id="time"
                  interface="action-sheet"
                  locale="ru-RU"
                  presentation="time"></ion-datetime>
              </ion-modal>
            </ion-item>
          </ion-list>
        </ion-content>
      </ion-modal>
        <ion-row>
        
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
  IonSelect,
  IonSelectOption,
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
    IonSelect,
    IonSelectOption,
  },
  data() {
    return {
      calciumFreq: 'twice',
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
    setCalciumFreq(val) {
      console.log('da')
      console.log(val)
      this.calciumFreq = val
    },
  },
})
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

ion-modal ion-toolbar {
  --background: rgb(56, 128, 255);
  --color: white;
}

ion-modal ion-toolbar ion-button {
  background-color: rgb(47, 116, 236);
  border-radius: 6px;
  padding: 0 8px;
}

ion-avatar {
  width: 70px;
  height: 70px;
}
</style>