<template>
  <topic-list :topicList="jobList" />
</template>

<script>
import { sortByDate } from '~/utils'
import TopicList from '~/components/TopicList'

export default {
  async asyncData ({ app }) {
    const [jobs, cv, career, outsourcing] = await Promise.all([
      app.$axios.get(`topics/show.json?node_name=jobs`).then(res => res.data),
      app.$axios.get(`topics/show.json?node_name=cv`).then(res => res.data),
      app.$axios.get(`topics/show.json?node_name=career`).then(res => res.data),
      app.$axios.get(`topics/show.json?node_name=outsourcing`).then(res => res.data)
    ])

    const jobList = sortByDate([...jobs, ...cv, ...career, ...outsourcing])

    return {
      jobList
    }
  },
  components: {
    TopicList
  }
}
</script>
