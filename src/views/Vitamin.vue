<template>
  <ion-page>
    <ion-header >
      <ion-toolbar>
        <ion-title>Витамины</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content  class="ion-padding">
      <div style="height: 30px; text-align: center; color: rgb(89, 89, 89)">
        <ion-label v-if="!D3start">
          Выберите день начала приема D3
        </ion-label>
      </div>
      <ion-datetime
        @ionChange="setStart"
        :highlighted-dates="highlightedDates"
        locale="ru-RU"
        :first-day-of-week="1"
        presentation="date"
      ></ion-datetime>
      <ion-button expand="block" id="open-modal">
        Изменить
        <ion-icon aria-hidden="true" icon='alarm.svg' style="margin-left: 10px;"/>
      </ion-button>
      <ion-modal ref="modal" trigger="open-modal">
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
            <ion-item v-for="item in vitaminsArray" :key="item.id" :style="`background-color: ${item.bgColor}`">
              <ion-avatar slot="start">
                <ion-img :src="item.avatar"></ion-img>
              </ion-avatar>
              <ion-label>
                <h2>{{ item.name }}</h2>
              </ion-label>
              
              <ion-datetime-button v-if="item.alarmCount === 2" datetime="time" presentation="time"></ion-datetime-button>
              <ion-modal :keep-contents-mounted="true">
                <ion-datetime
                  id="time"
                  interface="action-sheet"
                  locale="ru-RU"
                  presentation="time"></ion-datetime>
              </ion-modal>
              
              <ion-datetime-button v-if="item.alarmCount !== 0" datetime="time" presentation="time"></ion-datetime-button>
              <ion-modal :keep-contents-mounted="true">
                <ion-datetime
                  id="time"
                  interface="action-sheet"
                  locale="ru-RU"
                  presentation="time"></ion-datetime>
              </ion-modal>
              
              <ion-select
                justify="end"
                value="twice"
                id="calciumFreq"
                interface="action-sheet"
                slot="end"
                aria-label="Кальций"
                style="min-width: 140px;"
                v-model="item.alarmCount">
                <ion-select-option
                  v-for="option in item.alertOptions" :key="option.value"
                  :value="option.value">{{ option.label }}</ion-select-option>
              </ion-select>
            </ion-item>
          </ion-list>
          
          <ion-button expand="block" id="open-modal" style="margin-top: 40px;">
            Сохранить
            <ion-icon aria-hidden="true" icon='save.svg' style="margin-left: 10px;"/>
          </ion-button>
          
        </ion-content>
      </ion-modal>
    </ion-content>
  </ion-page>
</template>

<!--<script setup lang="ts">-->
<!--import {IonDatetime, IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonIcon} from '@ionic/vue';-->
<!--const settingsToggle = false-->
<!--function save() {-->

<!--}-->
<!--</script>-->

<script setup lang="ts">
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
  IonDatetime,
} from '@ionic/vue';
import {defineComponent, ref} from 'vue';
import {logIn} from "ionicons/icons";
import * as events from "events";
const modal = ref(null)
const vitaminsArray = ref([
  {
    id: 1,
    name: 'Кальций',
    alarmCount: 2,
    avatar: 'calcium.jpeg',
    bgColor: '#a4c8ff',
    alertOptions: [
      {
        label: 'Один раз в день',
        value: 1,
      },
      {
        label: 'Два раза в день',
        value: 2,
      },
      {
        label: 'Откл',
        value: 0,
      }
    ],
  },
  {
    id: 2,
    name: 'D3',
    alarmCount: 1,
    avatar: 'd3.jpeg',
    bgColor: '#efc18a',
    alertOptions: [
      {
        label: 'Раз в три дня',
        value: 1,
      },
      {
        label: 'Откл',
        value: 0,
      }
    ],
  },
])
const D3start = ref(null)

const highlightedDates = (isoString: string) => {
  if (!D3start.value) {
    return undefined
  }
  const date = new Date(isoString)
  const utcDay = date.getUTCDate()
  const D3startDay = new Date(D3start.value).getUTCDate()
  
  if ((D3startDay + utcDay) % 3 === 0) {
    return {
      textColor: 'var(--ion-color-secondary-contrast)',
      backgroundColor: 'var(--ion-color-secondary)',
    };
  }
  
  return undefined;
}
function dismiss() {
  modal.value.$el.dismiss()
}
function setStart(e: any) {
  D3start.value = e.detail.value
}
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