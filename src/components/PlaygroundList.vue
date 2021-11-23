<template>
    <h1>Playgrounds on AWS Amplify</h1>
    <div class="card-wrapper">
      <playground-card v-for="playground in playgrounds" :key="playground.id" :playground="playground" />
    </div>
</template>

<script>
import PlaygroundCard from "./PlaygroundCard.vue"
export default {
  name: "PlaygroundList",
  components: {
      PlaygroundCard
  },
  data() {
    return {
      playgrounds: [],
    };
  },
  mounted() {
    const options = {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        query: `
                    query {
                        allPlaygrounds {
                        id
                        name
                        rating
                        equipment {
                        name
                        equipmentType
                        }
                        location {
                        city
                        street
                        zip
                        }
                        heroImage
                        }
                    }
               `,
      }),
    };
    fetch(`http://localhost:9002/graphql`, options)
      .then((response) => response.json())
      .then((data) => {
        this.playgrounds = data.data.allPlaygrounds;
      });
  },
};
</script>

<style>
.card-wrapper {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
}
</style>