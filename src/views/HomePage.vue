<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Inbox</ion-title>
      </ion-toolbar>
    </ion-header>
    
    <ion-content :fullscreen="true">
      <ion-refresher slot="fixed" @ionRefresh="refresh($event)">
        <ion-refresher-content></ion-refresher-content>
      </ion-refresher>
      
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Inbox</ion-title>
        </ion-toolbar>
      </ion-header>
      
      <ion-list>
        <ion-label>
          Use href elements
        </ion-label>
        <ion-toggle v-model="useHrefElements"></ion-toggle>
      </ion-list>

      <ion-list v-if="useHrefElements">
        <MessageListItemHref v-for="message in messages" :key="message.id" :message="message" />
        </ion-list><ion-list>
        <MessageListItem v-for="message in messages" :key="message.id" :message="message" />
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonContent, IonHeader, IonList, IonPage, IonRefresher, IonRefresherContent, IonTitle, IonToolbar, IonLabel, IonToggle } from '@ionic/vue';
import MessageListItem from '@/components/MessageListItem.vue';
import MessageListItemHref from '@/components/MessageListItemHref.vue';
import { defineComponent } from 'vue';
import { getMessages } from '@/data/messages';

export default defineComponent({
  name: 'HomePage',
  data() {
    return {
      messages: getMessages(),
      useHrefElements: false
    }
  },
  methods: {
    refresh: (ev: CustomEvent) => {
      setTimeout(() => {
        ev.detail.complete();
      }, 3000);
    }
  },
  components: {
    IonContent,
    IonHeader,
    IonList,
    IonPage,
    IonRefresher,
    IonRefresherContent,
    IonTitle,
    IonToolbar,
    MessageListItemHref,
    MessageListItem,IonLabel, IonToggle
  },
});
</script>
