<template>
  <div class="card-outer">
    <div class="title">Are you ready to take the challenge?</div>
    <div class="download">Download Harlem Wizards App</div>
    <div class="store">
      <div class="store-logo">
        <img src="../assets/goolge-store.png" alt="Google Play Store" />
      </div>
      <div class="store-logo">
        <img src="../assets/apple-store.png" alt="Apple Store" />
      </div>
    </div>
    <div class="signUp">or you can sign up right now</div>
    <div class="search">
      <input
        class="search-input"
        type="text"
        placeholder="Search schools..."
        v-model="searchTerm"
        @input="handleSearch"
      />
      <div class="school-list-container">
        <VueSpinner v-if="loading" size="50" color="red" />
        <div v-else-if="schoolList.length === 0" class="no-results">
          No results found
        </div>
        <div v-else class="school-list">
          <div
            v-for="school in schoolList"
            :key="school.id"
            class="school-card"
          >
            <div class="school-image">
              <img :src="school.logo_url" alt="school logo" />
            </div>
            <div class="school-info">
              <h3 class="school-name">{{ school.school_name }}</h3>
              <button class="join-button">Join campaign</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { VueSpinner } from 'vue3-spinners'
export default {
  components: {
    VueSpinner,
  },
  data() {
    return {
      schoolList: [],
      searchTerm: '',
      loading: false,
    }
  },

  methods: {
    async fetchSchoolList(searchTerm = '') {
      this.loading = true
      try {
        const response = await fetch(
          `http://api.devharlemwizardsinabox.com/campaign/campaign_school_list/?search=${searchTerm}`
        )
        const data = await response.json()
        this.schoolList = data.school_list
      } catch (error) {
        console.error('Error fetching school list:', error)
      } finally {
        this.loading = false
      }
    },
    handleSearch() {
      this.fetchSchoolList(this.searchTerm)
    },
  },
  mounted() {
    this.fetchSchoolList()
  },
}
</script>

<style scoped>
.card-outer {
  max-width: 810px;
  padding: 20px;
  margin: 0 auto;
  border: 1px solid #bdbaba;
  border-radius: 10px;
  margin-bottom: 40px;
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.1), 0 8px 20px rgba(0, 0, 0, 0.08);
  background-color: white;
  text-align: center;
  height: 650px;
}
.download {
  font-weight: bold;
}
.school-list-container {
  max-height: 300px;
  overflow-y: auto;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 10px;
  position: relative;
}
.title {
  font-family: cursive;
  font-size: 38px;
  font-weight: bold;
  margin-bottom: 15px;
}

.store {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin: 20px 0;
}

.store-logo img {
  height: 40px;
  width: 120px;
  object-fit: contain;
}

.signUp {
  font-family: sans-serif;
  font-size: 15px;
  position: relative;
  margin: 20px 0;
  display: inline-block;
}

.signUp:before,
.signUp:after {
  content: '';
  width: 100px;
  height: 1px;
  background: #bdbaba;
  position: absolute;
  top: 50%;
}

.signUp:before {
  left: -110px;
}

.signUp:after {
  right: -110px;
}
.no-results {
  width: 100%;
  text-align: center;
  color: #888;
  font-size: 16px;
  margin-top: 20px;
}
.search {
  max-width: 600px;
  margin: 0 auto;
}

.search-input {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ddd;
  border-radius: 8px;
  margin-bottom: 20px;
  box-sizing: border-box;
}

.school-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
}

.school-card {
  display: flex;
  align-items: center;
  gap: 25px;
  border: 1px solid #ddd;
  padding: 6px 20px;
  border-radius: 10px;
  background-color: #f9f9f9;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
}

.school-image img {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  object-fit: cover;
  margin-right: 15px;
}

.school-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}

.school-name {
  font-size: 18px;
  font-weight: 600;
  margin: 0;
  flex-grow: 1;
  text-align: left;
}

.join-button {
  color: rgb(207, 30, 104);
  border: 1px solid rgb(207, 30, 104);
  border-radius: 5px;
  padding: 8px 15px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.join-button:hover {
  background-color: rgb(207, 30, 104);
  color: white;
}

@media (max-width: 480px) {
  .title {
    font-size: 20px;
  }

  .school-list {
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  }

  .school-card {
    flex-direction: column;
    text-align: center;
  }
  .signUp:before,
  .signUp:after {
    width: 25px;
  }
  .signUp:before {
    left: -50px;
  }

  .signUp:after {
    right: -50px;
  }

  .school-info {
    flex-direction: column;
    justify-content: center;
  }

  .join-button {
    margin-top: 10px;
  }
}
</style>
