<template>
  <div class="data">
    <div class="line">
      <h3>weather:</h3> <div class="hContainer">
        <h3 v-if="catched" className="number">{{ data.weather }}</h3>
        <h3 v-else className="load"></h3>
      </div>
    </div>
    <div class="line">
      <h3>temperature:</h3> <div class="hContainer">
        <h3 v-if="catched" className="number">{{ data.temp }}</h3>
        <h3 v-else className="load"></h3>
      </div>
    </div>
    <div class="line">
      <h3>feels like:</h3> <div class="hContainer">
        <h3 v-if="catched" className="number">{{ data.feelsLike }}</h3>
        <h3 v-else className="load"></h3>
      </div>
    </div>
    <div class="line">
      <h3>pressure:</h3> <div class="hContainer">
        <h3 v-if="catched" className="number">{{ data.pressure }}</h3>
        <h3 v-else className="load"></h3>
      </div>
    </div>
    <div class="line">
      <h3>maximum temperature:</h3> <div class="hContainer">
        <h3 v-if="catched" className="number">{{ data.tempMax }}</h3>
        <h3 v-else className="load"></h3>
      </div>
    </div>
    <div class="line">
      <h3>minimum temperature:</h3> <div class="hContainer">
        <h3 v-if="catched" className="number">{{ data.tempMin }}</h3>
        <h3 v-else className="load"></h3>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['data', 'catched'],
}
</script>

<style lang="scss" scoped>
$data-color:black;

.data {
  margin-top: 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 15px;
  height: 300px;
  color: $data-color;

  .line {
    display: flex;
    flex-direction: row;
    gap: 10px;
    padding: 5px 10px;
    border-bottom: 2px solid black;

    h3 {
      font-weight: lighter;
    }

    .hContainer {
      min-width: 50px;
      height: 100%;
      overflow: hidden;

      .number {
        font-weight: bold;
        font-size: 20px;
      }

      .load {
        width: 100%;
        height: 100%;
        background: rgb(255,192,203);
        background: linear-gradient(90deg, rgba(255,192,203,0) 13%, rgba(255,192,203,0) 29%, $data-color 41%, rgba(0,0,0,1) 42%, rgba(255,192,203,0) 52%, rgba(255,192,203,0) 94%);
        min-width: 40px;
  
        @keyframes requestAnimation {
          0% { transform: translateX(-50px); }
          50% { transform: translateX(50px); }
          100% { transform: translateX(-50px); }
        }
  
        animation: requestAnimation linear 1s infinite;
      }
    }
  }
}
</style>