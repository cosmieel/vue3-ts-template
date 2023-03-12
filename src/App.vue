<template>
  <div class="app">
    <header class="header">
      <div class="header__title">
        <h1>Jobs</h1>
      </div>
      <div class="header__sort-buttons">
        <button class="header__sort-button" @click="sortJobsItems('title')">
            Sort by title
        </button>
        <button class="header__sort-button" @click="sortJobsItems('salary')">
            Sort by salary
        </button>
        <button class="header__sort-button" @click="sortJobsItems('location')">
            Sort by location
        </button>
      </div>
    </header>

    <JobList :jobs="jobs" :sort-order="sortOrder" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import Job from '@/types/Job';
import JobsOrderTerm from '@/types/JobsOrderTerm';
import JobList from './components/JobList.vue';

export default defineComponent({
  name: 'App',
  components: { JobList },
  setup() {
    const jobs = ref<Job[]>([
      {
        title: 'Intern Frontend Developer', location: 'Moscow', salary: 100000, id: '1',
      },
      {
        title: 'Junior Frontend Developer', location: 'Chelyabinsk', salary: 200000, id: '2',
      },
      {
        title: 'Middle Frontend Developer', location: 'Saint Petersburg', salary: 300000, id: '3',
      },
      {
        title: 'Senior Frontend Developer', location: 'Ekaterinburg', salary: 400000, id: '4',
      },
      {
        title: 'Lead Frontend Developer', location: 'Kazan', salary: 500000, id: '5',
      },
    ]);
    const sortOrder = ref<JobsOrderTerm>('title');

    const sortJobsItems = (term: JobsOrderTerm) => {
      sortOrder.value = term;
    };

    return { jobs, sortOrder, sortJobsItems };
  },
});
</script>

<style lang="scss">
    .header {
        text-align: center;

        &__title {
            display: flex;
            justify-content: center;

            h1 {
                font-size: 3em;
            }
        }

        &__sort-buttons {
            margin-top: 20px;
        }

        &__sort-button {
            margin: 0 10px;
            color: #1195c9;
            border: 3px solid #1195c9;
            background: #d5f0ff;
            padding: 8px 16px;
            border-radius: 4px;
            cursor: pointer;
            font-weight: bold;
        }
    }
</style>
