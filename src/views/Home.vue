<template>
  <div class="listing">
    <img src="@/assets/logo.png" alt="logo" class="listing__logo" />
    <Search :search="search" />
    <Loader v-if="loading" />

    <ul v-else class="listing__list">
      <li
        v-for="(record, key) in slicedRecords"
        :key="key"
        class="listing__listItem"
      >
        <Record
          :img="record.imagePath"
          :title="record.title"
          :description="record.description"
        />
      </li>
    </ul>
    <p class="listing__empty" v-if="!loading && slicedRecords == 0">
      There is not search results for '<span class="listing__searchValue">{{
        this.$route.query.search
      }}</span
      >'
    </p>
    <Pagination
      :numberOfPages="numberOfPages"
      v-model="page"
      v-if="!loading && numberOfPages > 1"
    />
  </div>
</template>

<script>
import axios from "axios";
import Loader from "../components/Loader";
import Search from "../components/Search";
import Pagination from "../components/Pagination";
import Record from "../components/Record";

export default {
  name: "Home",
  components: {
    Loader,
    Search,
    Pagination,
    Record,
  },
  data() {
    return {
      records: [],
      page: 0,
      perPage: 6,
      loading: false,
    };
  },
  async mounted() {
    this.loading = true;

    window.setTimeout(async () => {
      const response = await axios.get("/planday.json");
      this.records = response.data;

      this.loading = false;
    }, 1000);
  },
  methods: {
    recordMatchesSearches(record) {
      return (
        record.title.toLowerCase().includes(this.search.toLowerCase()) ||
        record.description.toLowerCase().includes(this.search.toLowerCase())
      );
    },
  },
  computed: {
    slicedRecords() {
      return this.filteredRecords.slice(
        this.page * this.perPage,
        (this.page + 1) * this.perPage
      );
    },
    numberOfPages() {
      return Math.floor((this.filteredRecords.length - 1) / this.perPage) + 1;
    },
    search() {
      return this.$route.query.search || "";
    },
    filteredRecords() {
      return this.records.filter(this.recordMatchesSearches);
    },
  },
};
</script>
<style lang="scss" scoped>
.listing {
  &__logo {
    display: block;
    width: 120px;
    margin: 10px auto;
  }
  &__list {
    list-style: none;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    max-width: 1100px;
    margin: 0 auto;
  }
  &__listItem {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    flex-direction: column;
    width: fit-content;
    margin: 30px 0;
  }
  &__empty {
    font-size: 16px;
    color: #787878;
  }
  &__searchValue {
    font-weight: 700;
    color: #189bd6;
  }
}
</style>
