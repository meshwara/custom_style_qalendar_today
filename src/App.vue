<template>
  <Qalendar :events="events" @updated-mode="updatedMode" />
</template>

<script setup>
import { Qalendar } from 'qalendar';
import { onMounted, ref, watch } from 'vue';

const events = [
  {
    title: 'Advanced algebra',
    with: 'Chandler Bing',
    time: { start: '2022-12-24 02:05', end: '2022-12-24 06:35' },
    color: 'yellow',
    isEditable: true,
    id: '753944708f0f',
    description:
      'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores assumenda corporis doloremque et expedita molestias necessitatibus quam quas temporibus veritatis. Deserunt excepturi illum nobis perferendis praesentium repudiandae saepe sapiente voluptatem!',
  },
  {
    title: 'Basis Data',
    with: 'Chandler Bing',
    time: { start: '2022-12-23 07:05', end: '2022-12-23 10:35' },
    color: 'yellow',
    isEditable: true,
    id: '753944708f0f',
    description:
      'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores assumenda corporis doloremque et expedita molestias necessitatibus quam quas temporibus veritatis. Deserunt excepturi illum nobis perferendis praesentium repudiandae saepe sapiente voluptatem!',
  },
  {
    title: 'Ralph on holiday',
    with: 'Rachel Greene',
    time: { start: '2022-12-19', end: '2022-12-23' },
    color: 'green',
    isEditable: true,
    id: '5602b6f589fc',
  },
];

const currentDate = ref(null);
onMounted(() => {
  currentDate.value = 'day-' + new Date().toISOString().split('T')[0];
});
const updateBackground = () => {
  if (!currentDate.value) return;
  var link = document.getElementById('datestyle');
  if (!link) {
    link = document.createElement('style');
    link.id = 'datestyle';
    document.head.appendChild(link);
  }
  // setiap kali nilai current date berubah, maka lebih aman jika style di rewrite
  link.innerHTML = `
    #${currentDate.value} {
      border: 1px solid #73ffc2;
      background-color: #d6ffed;
    }

    #${currentDate.value} span.calendar-month__day-date{
      font-weight: bold;
      background-color: #00baff;
      border-radius: 50%;
      padding: 5px;
      color: white      
    }
  `;
};

const updatedMode = () => {
  updateBackground();
};

watch(currentDate, () => {
  updateBackground();
});
</script>

<style>
@import '../node_modules/qalendar/dist/style.css';
</style>
