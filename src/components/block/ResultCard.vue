<template>
  <div class="result__card">
    <header>
      <div class="circle">
        <img :src="image" alt="" />
      </div>
    </header>
    <div class="content">
      <h3>{{ title }}</h3>
      <p>
        {{ mainText }}
      </p>
    </div>
    <footer v-if="hasTips">
      <h4>Pour l'éviter</h4>
      <div class="tips">
        <img :src="LightBulb" alt="" />
        <p>
          {{ tipsText }}
        </p>
      </div>
    </footer>
  </div>
</template>

<script>
import LightBulb from '@/assets/images/results/lightbulb.png'

export default {
  name: 'ResultsCard',
  components: {},
  props: {
    image: {
      type: String,
      default: null
    },
    title: {
      type: String,
      default: null
    },
    mainText: {
      type: String,
      default: null
    },
    hasTips: {
      type: Boolean,
      default: null
    },
    tipsText: {
      type: String,
      default: null
    }
  },
  data() {
    return {
      LightBulb
    }
  }
}
</script>

<style lang="scss" scoped>
.result__card {
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  height: 100%;
  padding: 0 32px;
  padding-bottom: 20px;
  margin: 0 20px;
  background-color: var(--color-whiteDimmed);
  border: 5px solid var(--color-black);
  border-radius: var(--box-rounded-radius);
  box-shadow: 6px 6px 0 var(--color-black);

  @include mobile {
    font-size: 14px;
  }
}

.result__card.no-tips {
  justify-content: flex-start;

  & h3 {
    padding: 30px;
  }
}

.result__card header {
  width: 170px;
  height: 170px;
  margin-top: -100px;
  background-color: var(--color-primary);
  border: var(--color-black) solid 4px;
  border-radius: 50%;

  & img {
    width: auto;
    height: 100px;
  }
}

.result__card .content h3 {
  padding: 0 0 10px 0 !important;
  margin: 0;
  font-size: 1.875em;
  font-weight: var(--weight-bold);
  text-align: center;
}

.result__card .content {
  text-align: center;
}

.result__card .content p {
  margin: 15px 0;
  font-size: 1.125em;
  font-weight: var(--weight-regular);
}

footer h4 {
  margin-top: 0.5em;
  margin-bottom: 1em;
  text-align: left;
}

footer p {
  font-weight: var(--weight-regular);
}

.tips {
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
}

.tips img {
  width: fit-content;
  max-width: 3.5em;
}

.tips p {
  margin-top: 0;
  margin-left: 1.25em;
  font-size: 1.125em;
  text-align: left;
}

.circle {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 160px;
  height: 160px;

  @include mobile {
    width: 140px;
    height: 140px;
  }
}

@media screen and (max-width: 767px) {
  .results {
    padding: 0;
  }

  .result__card {
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    max-width: 95vw;
    // height: 625px;
    // padding: 0 20px;
    margin: 1.25em;
    background-color: var(--color-whiteDimmed);
    border-radius: var(--box-rounded-radius);
    box-shadow: 6px 6px 0 var(--color-black);
  }

  header {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 200px;
    height: 200px;
    margin-top: -100px;
    border: var(--color-black) solid 4px;
    border-radius: 50%;
  }

  .result__card .content h3 {
    padding: 1.25em 0;
    font-size: 1.875em;
    font-weight: var(--weight-bold);
    text-align: center;
  }
}

@media screen and (min-width: 992px) {
  .result__card {
    // height: 670px;
    margin: 0 10px;
  }
}
</style>
