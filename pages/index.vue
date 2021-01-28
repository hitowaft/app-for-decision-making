<template>
  <div>
    <title>{{ title }}</title>
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
    <button type="button" @click="addSubject">追加</button>
  </div>
</template>

<script>
export default {
  data(app) {
    return {
      title: '決断支援アプリ',
      subjects: [],
      val: '',
      newSub: '',
      selectSubject() {
        if (!app.val) {
          return ''
        }
        return `/subject/${this.val}`
      },
      addSubject(newSub) {
        if (!app.newSub) {
          return ''
        }
        const size = app.subjects.length + 1
        app.$set(app.subjects, size - 1, { id: size, theme: app.newSub })
        app.newSub = ''
      },
      deleteSubject() {
        app.subjects.splice(app.val - 1, 1)
      },
    }
  },
}
</script>
