<template>
  <div class="main-content container-fluid" :style="backgroundStyle">
    <div class="background-overlay"></div>
    <div class="row">
      <div class="col-md-3 poster-section">
        <img :src="movie.Poster" alt="Movie Poster" class="img-fluid rounded" v-if="movie.Poster" />
        <div class="streaming-info mt-3 text-center">
          <span>Now Streaming</span><br />
          <a href="#" class="watch-now-link">Watch Now</a>
        </div>
      </div>

      <div class="col-md-9 details-section">
        <h2 class="movie-title">{{ movie.Title }} ({{ movie.Year }})</h2>
        <div class="movie-info">
          <span>{{ movie.Released }}</span> •
          <span>{{ movie.Genre }}</span> •
          <span>{{ movie.Runtime }}</span>
        </div>

        <div class="d-flex align-items-center mt-3">
          <div class="score-circle me-3">
            <span>{{ movie.Metascore }}%</span>
          </div>
          <span class="user-score-text">User Score</span>
          <button class="btn btn-outline-light btn-sm ms-3 play-trailer-btn">
            <i class="bi bi-play-fill"></i> Play Trailer
          </button>
        </div>

        <p class="tagline mt-4">{{ movie.Tagline || 'Obviously.' }}</p>

        <h5 class="overview-title">Overview</h5>
        <p class="overview-text">{{ movie.Plot }}</p>

        <div class="row credits mt-4">
          <div v-for="(credit, index) in credits" :key="index" class="col-6 col-md-4 col-lg-3 credit-item">
            <p class="credit-name">{{ credit.name }}</p>
            <p class="credit-role">{{ credit.roles.join(', ') }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      movie: {},
      credits: []
    };
  },
  computed: {
    backgroundStyle() {
      return {
        backgroundImage: window.innerWidth >= 768 && this.movie.Poster
            ? `url(${this.movie.Poster})`
            : '#1e3a63',
        backgroundSize: 'cover',
        backgroundPosition: 'center',
        backgroundRepeat: 'no-repeat'
      };
    }
  },
  mounted() {
    this.fetchMovieData();
    window.addEventListener('resize', this.updateBackground);
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.updateBackground);
  },
  methods: {
    async fetchMovieData() {
      try {
        const response = await fetch(
            'https://www.omdbapi.com/?i=tt3896198&apikey=d2132124'
        );
        const data = await response.json();
        if (data.Response === 'True') {
          this.movie = data;

          const creditsMap = {};

          data.Director.split(', ').forEach((name) => {
            if (creditsMap[name]) {
              creditsMap[name].roles.push("Director");
            } else {
              creditsMap[name] = { name, roles: ["Director"] };
            }
          });

          data.Writer.split(', ').forEach((name) => {
            if (creditsMap[name]) {
              creditsMap[name].roles.push("Writer");
            } else {
              creditsMap[name] = { name, roles: ["Writer"] };
            }
          });

          data.Actors.split(', ').forEach((name) => {
            if (creditsMap[name]) {
              creditsMap[name].roles.push("Actor");
            } else {
              creditsMap[name] = { name, roles: ["Actor"] };
            }
          });

          this.credits = Object.values(creditsMap);
        } else {
          console.error('Error fetching movie:', data.Error);
        }
      } catch (error) {
        console.error('Error fetching movie:', error);
      }
    },
    updateBackground() {
      this.$forceUpdate();
    }
  }
};
</script>

<style scoped>
.main-content {
  color: white;
  position: relative;
  padding: 20px;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.background-overlay {
  background-color: rgba(0, 0, 0, 0.7);
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 1;
}

.row {
  position: relative;
  z-index: 2;
}

.poster-section {
  text-align: center;
  z-index: 3;
}

.streaming-info {
  font-size: 0.9rem;
  color: #cccccc;
}

.watch-now-link {
  color: #01b4e4;
  font-weight: bold;
}

.movie-title {
  font-size: 2rem;
  font-weight: bold;
}

.movie-info {
  color: #cccccc;
  font-size: 0.9rem;
}

.score-circle {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background-color: #28a745;
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: bold;
  font-size: 1.2rem;
}

.user-score-text {
  font-size: 1rem;
}

.play-trailer-btn {
  color: #01b4e4;
  border-color: #01b4e4;
}

.tagline {
  font-style: italic;
  color: #cccccc;
}

.overview-title {
  font-size: 1.3rem;
  margin-top: 1rem;
}

.overview-text {
  font-size: 1rem;
  color: #cccccc;
}

.credits {
  display: flex;
  flex-wrap: wrap;
}

.credit-item {
  margin-bottom: 10px;
}

.credit-name {
  font-weight: bold;
}

.credit-role {
  font-size: 0.9rem;
  color: gray;
}
</style>
