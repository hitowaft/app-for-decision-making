<template>
  <div>
    <title>{{ title }}</title>
    <pre>{{ $data }}</pre>
    <h1>{{ title }}</h1>
    <p>テーマを選ぶ</p>
    <ul>
      <li v-for="subject in subjects" :key="subject.id">
        {{ subject.theme }}
        <input type="radio" :value="subject.id" v-model="val" />
      </li>
    </ul>
    <button type="button" @click="$router.push(selectSubject())">決定</button>
    <button type="button" @click="deleteSubject()">削除</button>

    <p>テーマを追加する</p>
    <input type="text" v-model="newSub" />
    <button type="button" @click="addSubject()">追加</button>
  </div>
</template>

<script>
export default {
  data(app) {
    return {
      title: 'タイトル',
      subjects: [],
      val: '',
      newSub: '',
      subId: 0,
    }
  },
  methods: {
    selectSubject() {
      if (this.val === '') {
        return ''
      }
      return `/subject/${this.val}`
    },
    addSubject() {
      if (!this.newSub) {
        return ''
      }
      this.$set(this.subjects, this.subjects.length, { id: this.subId, theme: this.newSub })
      this.newSub = ''
      this.subId++
    },
    deleteSubject() {
      const target = this.subjects.findIndex((x) => x.id === this.val)
      this.subjects.splice(target, 1)
      this.val = ''
    },
  },
}
</script>
