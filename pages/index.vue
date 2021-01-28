<template>
  <div>
    <title>{{ title }}</title>
    <h1>{{ title }}</h1>
    <p>テーマを選ぶ</p>
    <ul>
      <li v-for="subject in subjects" :key="subject.id">
        {{ subject.theme }}
        <input type="radio" :value="subject.theme" v-model="val" />
      </li>
    </ul>
    <button type="button" @click="$router.push(selectSubject())">決定</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: '決断支援アプリ',
      subjects: [
        {
          id: 1,
          theme: 'subject1',
        },
        {
          id: 2,
          theme: 'subject2',
        },
      ],
      val: '',
      selectSubject() {
        return `/topics/${this.val}`
      },
    }
  },
}
</script>
