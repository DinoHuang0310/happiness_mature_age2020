<template>
    <div v-if="agencysList.list.length > 0">
      <div class="title">
        <h2><span>{{ agencysList.title }}</span></h2>
      </div>
      <ul :class="agencysList.list.length < 3 ? 'center' : null">
        <li
          v-for="list in agencysList.list"
          :key="list.index"
        >
          <a v-if="list.url" :href="list.url" target="_blank">
            <img :src="list.image" :alt="list.title" />
          </a>
          <img v-else :src="list.image" :alt="list.title" />
        </li>
      </ul>
    </div>
</template>

<script>
export default {
  props: {
    agencysList: {
      type: Object,
      required: true
    }
  }
}
</script>