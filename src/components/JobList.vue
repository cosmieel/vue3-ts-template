<template>
  <div class="jobs">
    <p>Ordered by {{ sortOrder }}</p>

    <transition-group name="list" tag="ul" class="jobs__list">
      <li class="jobs__item" v-for="job in orderedJobs" :key="job.id">
        <h2 class="jobs__title">{{ job.title }} in {{ job.location }}</h2>

        <div class="jobs__salary">
          <p>{{ job.salary }} ₽</p>
        </div>

        <div class="jobs__description">
            <p>
                Lorem ipsum dolor sit amet consectetur, adipisicing elit.
                Rem omnis voluptatum eius doloremque optio iusto sequi dignissimos.
                Pariatur earum assumenda dolores possimus quidem quam,
                reprehenderit aliquid consequuntur amet non facere.
            </p>
        </div>
      </li>
    </transition-group>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType, computed } from 'vue';
import Job from '@/types/Job';
import JobsOrderTerm from '@/types/JobsOrderTerm';

export default defineComponent({
  props: {
    jobs: {
      type: Array as PropType<Job[]>,
      required: true,
    },
    sortOrder: {
      type: String as PropType<JobsOrderTerm>,
      required: true,
    },
  },
  setup(props) {
    function sortJobs(jobs: Job[], order: JobsOrderTerm) {
      return [...jobs].sort((a: Job, b: Job) => (a[order] > b[order] ? 1 : -1));
    }
    const orderedJobs = computed(() => sortJobs(props.jobs, props.sortOrder));

    return { orderedJobs };
  },
});
</script>

<style lang="scss" scoped>
  .jobs {
    max-width: 960px;
    margin: 40px auto;

    &__list {
        padding: 0
    }

    &__item {
        list-style-type: none;
        background: white;
        padding: 16px;
        margin: 16px 0;
        border-radius: 4px;
    }

    &__title {
        margin: 0 0 10px;
        text-transform: capitalize;
    }

    &__salary {
        display: flex;

        p {
            color: #17bf66;
            font-weight: bold;
            margin: 10px 4px;
        }
    }
  }

  .list-move {
    transition: all 1s;
  }
</style>
