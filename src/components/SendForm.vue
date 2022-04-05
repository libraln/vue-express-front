<template>
  <div class="container">
    <div class="row">
      <div id="app" class="col-6 mt-2">
        <form @submit.prevent="calcNum">
          <div>
            <input type="text" class="form-control" v-model="number" />
          </div>
          <p>{{ number }} * 2</p>
          <button type="submit" class="btn btn-warning">Calculate</button>
        </form>
        <div>Result: {{ newNum }}</div>
      </div>
    </div>
  </div>
</template>
<script>
/* eslint-disable */
export default {
  data() {
    return {
      number: 0,
      newNum: 0,
    };
  },
  async mounted() {
    const res = await fetch("http://localhost:3000/api/newNum");
    this.newNum = res.json();
    console.log('hello');
  },
      methods: {
        async calcNum() {
            const data = {
                number: this.number,
            }
            const res = await fetch('http://localhost:3000/api/newNum', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(data)
            })
            this.number = 0
            const newN = await res.json()
            this.newNum = newN
        }
    }
};
</script>
