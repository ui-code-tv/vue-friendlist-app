
<script>


export default {
  name: 'App',
  data () {
    return {
    list: [
      { id: 1,name:"Ashley Adams",time:"1h",text:"I am working on a very big project, too busy to talk",image:"img1.png" },
      { id: 2,name:"Ben scott",time:"2h",text:"I am working on a very big project, too busy to talk",image:"img2.png" },
      { id: 3,name:"Julie Smith",time:"4h",text:"I am working on a very big project, too busy to talk",image:"img1.png" }
    ],
    maxId: 3
    }
  },
  methods: {
    random(max) {
      return Math.floor(Math.random() * (max + 1))
    },
    add() {      
      const id = ++this.maxId;
      const name ='Angie Sims';
      const time = '1h';
      const image = "img1.png";
      const text = "Learning fullstack development, on course to become a web dev ninja"

      const index = this.random(this.list.length)
      this.list.splice(index, 0, { id,name,time,image,text })
    },
    remove() {
      const index = this.random(this.list.length - 1)
      this.list.splice(index, 1)
    },
    shuffle() {
      const shuffled = []
      while (this.list.length > 0) {
        const index = this.random(this.list.length - 1)
        shuffled.push(this.list[index])
        this.list.splice(index, 1)
      }
      this.list = shuffled
    }

  },
   mounted() {
    console.log(JSON.stringify(this.list));
  }


}
</script>

<template>
<div class="wrapper">
    <div>
      <button type="button" @click="add">Add</button>
      <button type="button" @click="remove">Remove</button>
      <button type="button" @click="shuffle">Shuffle</button>
    </div>
    <transition-group tag="ul" name="list">
      <li class='list-item' v-for="item in list" :key="item.id">
        <div class="content">
          <img v-bind:src="item.image">
          <div class="main">
            <div class="header">
              <span class="name">{{item.name}}</span>
              <span class="time">{{item.time}}</span>
            </div>
            <div class="body">
            {{item.text}}
            </div>
          </div>
        </div>
      </li>
    </transition-group>
</div>
</template>

<style> 
/* Reset */
html {
  height: 100%;
  padding: 0;
  margin: 0;
  font-family: "Open Sans", sans-serif;
  font-size: 0.8rem;
}

* {
  box-sizing: border-box;
  margin:0;
  padding:0;
}

body {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  flex-direction: column;
  padding-top:5%;
  background-color: #46a5c6
}

/* Buttons */
button {
  padding: 8px 30px;
  border-width: 0;
  background-color: transparent;
  color: #000;
  font-family: inherit;
  font-size: inherit;
  cursor: pointer;
  border: 2px solid #BBDEFB;
  border-radius: 5px;
  margin-right: 2em ;

}

button:hover {
  color: #fff;
}

button:focus {outline: none }

/* Friend list */

ul {
  position: relative;
  padding-top: 18px;
  width: 420px;
}

.list-item {
  display: block;
  margin-top: 8px;
  width: 100%;
  height: 100px;
  position: relative;
  overflow: hidden;
  border: 3px solid #BBDEFB;
  border-radius: 5px;
}

.list-item img {
  display: block;
  border-radius: 50%;
  height: 60px;
  margin: 0 10px 0 10px;
  width: 60px;
  border: 4px solid #cacfd5;
}

.list-item .content {
  align-items: center;
  background: #fff;
  display: flex;
  flex-direction: row;
  height: 100%;
  left: 0px;
  width: 100%;
  padding: 10px 0px;
  position: absolute;


}


.list-item .time {
  font-weight: bold;
  color: lightgray;
  margin-left: 1em ;

}

/* List animation */

.list-enter-active,
.list-leave-active,
.list-move {
  transition: 500ms cubic-bezier(0.64, 0.26, 0.08, 1.03);
  transition-property: opacity, transform;
}

.list-enter {
  opacity: 0;
  transform: translateY(50px) scaleY(0.5);
}

.list-enter-to {
  opacity: 1;
  transform: translateX(0) scaleY(1);
}

.list-leave-active {
  position: absolute;
  opacity: 0;
  transform: scaleY(0);
}


.list-enter-active {
  animation: bounce-in 0.5s;
}
.list-leave-active {
  animation: bounce-in 0.5s reverse;
}

@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.25);
  }
  100% {
    transform: scale(1);
  }
}

</style>
