<script>
import { ref } from "vue";
export default {
  setup() {
    const randoms = (t) => {
      const el = ref(['el0', 'el1', 'el2', 'el3']);
      const randomIndex = Math.floor(Math.random() * el.value.length);
      t.value.push(el.value[randomIndex])
    };
    const asd = ref([]);
    const add = ref([]);
    const proverca = () => {
      const ke = Object.keys(asd.value);
      return ke.every(key => asd.value[key] === add.value[key]);
    };

    const fal = ref();
    const win = ref("Winner!!");

    const shet = ref(0);
    const raund = ref(0);
    const times = ref(0);
    const botClick = (time) => {
      for (let i = 0; i < asd.value.length; i++) {
        const el = document.getElementById(asd.value[i]);
        setTimeout(() => {
          el.classList.add("active");
          setTimeout(() => {
            el.classList.remove("active");

          }, 500);
        }, i * time);
      };
    };
    const addClick = () => {
      raund.value = 0;
      times.value = 0;
      asd.value = [];
      add.value = [];
      randoms(asd);
      times.value += 1000;
      raund.value +=1;
      botClick(times.value);

    };
    const addClickHard = () => {
      raund.value = 0;
      times.value = 0;
      asd.value = [];
      add.value = [];
      randoms(asd);
      times.value += 800;
      raund.value +=1;
      botClick(times.value);

    };
    const addClickIzi = () => {
      raund.value = 0;
      times.value = 0;
      asd.value = [];
      add.value = [];
      randoms(asd);
      times.value += 1500;
      raund.value +=1;
      botClick(times.value);

    };
    const boxClick = (el) => {
      const id = el.target.id
      add.value.push(id);
      el.target.classList.add("active");
      setTimeout(() => {
        el.target.classList.remove("active");
      }, 100);
      if (asd.value.length !== 0) {
        if (asd.value.length === add.value.length) {
          if (proverca()) {
            if ([5,10,15,20].includes(shet.value)) {
              randoms(asd);
              shet.value += 1;
              raund.value += 1;
              times.value = times.value/1.1;
              setTimeout(() => {
                botClick(times.value);
                add.value = [];
              }, 1000);
            } else {
              randoms(asd);
              shet.value += 1
              setTimeout(() => {
                botClick(1000);
                add.value = [];
              }, 1000);
              if (shet.value === 26) {
                asd.value = [];
              };
            };
          } else {
            shet.value = 0;
            fal.value = "Failed!";
          }
        };
      };
    };
    return {
      addClick,
      boxClick,
      shet,
      raund,
      addClickHard,
      addClickIzi,
      fal,
      win,
      proverca
    }
  }
}
</script>

<template>
  <div class="container">
    <div class="left">
      <div id="el0" @click="boxClick" class="box"></div>
      <div id="el1" @click="boxClick" class="box"></div>
      <div id="el2" @click="boxClick" class="box"></div>
      <div id="el3" @click="boxClick" class="box"></div>
      <h1 class="shit">Счет: {{ shet }}</h1>
      
      <h1 v-if="shet === 26" class="w"><br><br>{{ win }}</h1>
      <h1 class="f"><br><br>{{ fal }}</h1>
    </div>
    <div class="right">
      <h1 class="raynd">Раунд: {{ raund }}</h1>
      <button @click="addClickHard" class="hard">Хард</button><br>
      <button @click="addClick" class="normal">Нормал</button><br>
      <button @click="addClickIzi" class="izi">Изи</button><br>
    </div>
  </div>
</template>

<style scoped>
.f{
  color: #ff0000;
}
.w{
  color: #217411;
}
.active {
  opacity: 0.2;
}

.right {
  text-align: center;
}

button {
  margin-bottom: 20px;
  columns: #fff;
}

.container {
  display: flex;
  justify-content: center;
}

.left {
  margin-right: 100px;
  width: 200px;
  display: flex;
  flex-wrap: wrap;
}

.box {
  width: 100px;
  height: 100px;
}

#el0 {
  background: #5eff00;
}

#el1 {
  background: #1900ff;
}

#el2 {
  background: #ff00ea;
}

#el3 {
  background: #ff0000;
}
</style>