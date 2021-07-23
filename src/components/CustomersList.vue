<template>
  <Wrapper>
    <div class="mainContainer">
      <div v-if="customers" class="customerList">
        <div class="customerListOptions">
          <div class="textInputContainer">
            <Card>
              <input
                type="text"
                v-model="name"
                @input="filterCustomers"
                placeholder="Find customers"
              />
            </Card>
          </div>
                  
              <div class="dropdown">
                <button @click="runDropDown" class="dropbtn">Filter by Name (A-Z)</button>
                
                    <div id="myDropdown" class="dropdown-content" :class="{show: showDropDown}">
                        <button @click="sortCustomers('alphabetical')">Name (A-Z)</button>
                        <button @click="sortCustomers('reverseAlphabetical')">Name (Z-A)</button>
                    </div>
                
               
                
          </div>
        </div>
        <div v-for="customer in filteredCustomers" :key="customer.id">
          <Customer :data="customer" />
        </div>
        <div v-if="filteredCustomers.length === 0">
          <p>no customer(s) found with the search criteria.</p>
        </div>
      </div>

      <div v-else class="loadingAnimation">
        <h2>
          Loading Customers <span class="dot1">.</span
          ><span class="dot2">.</span><span class="dot3">.</span>
        </h2>
      </div>
    </div>
  </Wrapper>
</template>

<script>
import Customer from "./Customer.vue";
import Wrapper from "./ui/Wrapper.vue";
import Card from "./ui/Card.vue";
import faker from "faker";
export default {
  components: { Customer, Wrapper, Card },
  data() {
    return {
      name: "",
      customers: null,
      filteredCustomers: null,
      showDropDown: false,
      customerUrl: "https://jsonplaceholder.typicode.com/users",
    };
  },
  methods: {
    filterCustomers() {
      this.filteredCustomers = this.customers.filter((value) => {
        const customerName = value.name;
        if (this.name.trim() === "") {
          return value;
        } else if (
          customerName.toUpperCase().includes(this.name.trim().toUpperCase())
        ) {
          return value;
        }
        return null;
      });
    },
    sortCustomers(value) {
      this.filteredCustomers.sort((a, b) =>
        a.name.toLowerCase().localeCompare(b.name.toLowerCase())
      );
      if (value === "reverseAlphabetical") {
        this.filteredCustomers = this.filteredCustomers.reverse();
      }
      this.runDropDown();
    },
    getImages() {
      //used to get images from faker because the provided api has no img links
      for (let i = 0; i < this.customers.length; i++) {
        this.customers[i].imgUrl = faker.fake("{{image.avatar}}");
      }
    },
    runDropDown() {
        this.showDropDown = !this.showDropDown
    }
  },
  mounted() {
    fetch(this.customerUrl)
      .then((res) => res.json())
      .then((data) => {
        this.customers = data;
        this.filteredCustomers = data;
        this.getImages();
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style>
.mainContainer {
  width: 100%;
  min-height: calc(100vh - 60px);
}
.customerList {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

.customerListOptions {
  display: grid;
  grid-template-columns: 1.2fr 1fr 0.8fr;
  grid-template-rows: 1fr;
  gap: 0px 0px;
  grid-template-areas: "one . two";
  width: 100%;
  margin: 50px;
}

.textInputContainer {
  grid-area: one;
}


input[type="text"] {
  width: 100%;
  background: url('https://www.freeiconspng.com/uploads/magnifying-glass-icon-13.png') 12px / 12px no-repeat white;
  padding: 0px 40px;
  height: 40px;
  border: none;
}
select {
  width: 100%;

  border: none;
  padding: 0px 10px;
  height: 40px;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  background: url('../assets/dropTriangle.png') 97% / 12px no-repeat white;
}

.dot1,
.dot2,
.dot3 {
  font-size: 3.5rem;
  display: inline-block;
}

.dot1 {
  animation: jump 1.5s infinite 0.4s;
}
.dot2 {
  animation: jump 1.5s infinite 0.7s;
  position: relative;
}
.dot3 {
  animation: jump 1.5s infinite 0.9s;
}

.loadingAnimation {
  padding: 25px;
}

@keyframes jump {
  0% {
    transform: scale(1, 1) translateY(0);
  }
  10% {
    transform: scale(1.1, 0.9) translateY(0);
  }
  30% {
    transform: scale(0.9, 1.1) translateY(-15px);
  }
  50% {
    transform: scale(1, 1) translateY(0);
  }
  57% {
    transform: scale(1, 1) translateY(-3px);
  }
  64% {
    transform: scale(1, 1) translateY(0);
  }
  100% {
    transform: scale(1, 1) translateY(0);
  }
}

.dropbtn {
    background-color: white;
    position: relative;
    margin: 0px 0px 0px 30%;
    color: black;
    width: 70%;
    min-width: 200px;
    border: none;
    cursor: pointer;
    padding: 12px;
    font-size: 16px;
    text-align: left;
    background: url('../assets/dropTriangle.png') 95% / 12px no-repeat white;
    border-radius: 12px;
    box-shadow: 0 1px 8px rgba(0, 0, 0, 0.25);
}
.dropdown-content {
  display: none;
  position: absolute;
  padding: 5px;
  margin-top: 5px;
  min-width: 200px;
  background-color: white;
  margin: 6px 0px 0px 30%;
  width: 70%;
  overflow: auto;
  z-index: 100;
  border-radius: 12px;
  box-shadow: 0 1px 8px rgba(0, 0, 0, 0.25);
}

.dropdown {
  grid-area: two;
  position: relative;
  display: inline-block;
}


.dropdown-content button {
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
  width: 100%;
  background: white;
  border-radius: 5px;
  border: none;
  
}

.dropdown button:hover {background: #F6F6F7;}

.show {display: block;}

@media only screen and (max-width: 900px) {
    .customerListOptions {
        display: grid;
        grid-template-columns: 1.2fr 0.5fr 1fr;
        grid-template-rows: 1fr;
        gap: 0px 0px;
        grid-template-areas: "one . two";
        width: 100%;
        margin: 50px 10px;
    }
    .dropbtn { 
        margin: 0px 0px 0px 0px;
        width: 100%;
        min-width: auto;
    }
    .dropdown-content { 
        margin: 5px 0px 0px 0px;
        width: 100%;
        min-width: auto;
    }
    
}

@media only screen and (max-width: 600px) {
  .customerListOptions {
    display: grid;
    grid-template-columns: 1.2fr;
    grid-template-rows: 1fr 1fr;
    gap: 25px 0px;
    grid-template-areas:
      "one"
      "two";
    margin: 50px 10px;
  }
  .dropbtn { 
        margin: 0px 0px 0px 30%;
        width: 70%;
  }
  .dropdown-content { 
        margin: 5px 0px 0px 30%;
        width: 70%;
  }


}
</style>