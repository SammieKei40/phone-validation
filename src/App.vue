<template>
  <div>
    <main>
      <div class="search-box">
        <input type="text" class="search-bar" placeholder="Type in the format +234808XXXXX" 
        v-model="query" 
        @keypress="fetchPhone">
      </div>
  
       <div class="phone-wrap">
        <div class="phone-box">
          <div class="country">{{phone.location}}</div>
          <div class="type">{{phone.type}}</div>
          <div class="carrier">{{phone.carrier}}</div>
        </div>
      </div>
    </main>
  </div>  
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
    api_key: "47bd0f6e7bcd4e9ba6dc26a87ee64913",
    base_url: "https://phonevalidation.abstractapi.com/v1/",
    query: '',
    phone: {}
    }
  },
  methods: {
    fetchPhone(e){
      if(e.key == "Enter"){
        fetch(`${this.base_url}?api_key=${this.api_key}&phone=${this.query}`)
        .then(res => {
          return res.json();
        }).then(this.setResults);
    
      }
    },
    setResults(results){
      this.phone = results;
      console.log(this.phone)
    }
  }
}
</script>

<style>
*{
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}

body{
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}

#app{
  background-image: url(./assets/phone.jpeg);
  background-position: bottom;
  background-size: cover;
  transition: 0.4s;
}

main{
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75))
}

.search-box{
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar{
  display: block;
  width: 100%;
  padding: 15px;
  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255,255, 225, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}

.search-box .search-bar:focus{
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255,255, 225, 0.75);
  border-radius: 16px 0px 16px 0px;
}

.phone-box .country{
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.phone-box .location{
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.phone-box{
  text-align: center;
}

.phone-box .carrier{
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 80px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255,255, 225, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.phone-box .type{
  color: #fff;
  font-size: 40px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
