<template>
  <section class="list container">
    <h1>TODO List</h1>
    <form @submit.prevent='addMessage()' >
      <input class="form-control" type="hidden" format="dd/mm/yyyy" v-model="newItem.id">
      <div class="form-row">
        <div class="col-md-3 mb-3">
          <input class="form-control" type="date" format="dd/mm/yyyy" v-model="newItem.date" required>
        </div>
        <div class="col-md-7 mb-3 form-group">
          <input class="form-control" type="text" v-model="newItem.text" required>
        </div>
        <div class="col-md-2 mb-3">
          <input class="form-control btn btn-primary" type="submit" :value="buttonValue">
        </div>
      </div>
    </form>
    <hr> 
  <p v-if="errors.length" class="alert-danger">
    <b>Please correct the following error(s):</b>
    <ul>
        <li :key="errors.indexOf(error.id)" v-for="error in errors">{{ error }}</li>
    </ul>
  </p>

  <ul class="list-group">
    <transition-group  name="fade" mode="out-in">
      <li :class="{ done: item.finished }" 
          class='bg-change-trans list-group-item d-flex justify-content-between align-items-center' 
          v-for='item in todoList' 
          :key='item.id'>
        <span>{{item.date|moment}} - <strong>{{item.text}}</strong></span>
        <span>
          <input type="checkbox" v-model="item.finished" class="btn">
          <button @click="editMessage(item)" class="btn btn-warning">
            <font-awesome-icon icon="edit" />
          </button>
          <button @click="deleteMessage(item)" class="btn btn-danger">
            <font-awesome-icon icon="trash" />
          </button>
        </span>
      </li>
    </transition-group>
  </ul>
  </section>
</template>

<script>
import * as moment from "moment";
import Vue from 'vue'
import { setTimeout } from 'timers';
export default {
  name: "List",
  data: function(event) {
    return {
      buttonValue: "",
      newItem: {
      },
      test: "test",
      todoList: [
        { id: 1, text: "Start learning IT", date: "2011-06-20", finished: true },
        { id: 2, text: "Finish university", date: "2018-06-30", finished: true },
        { id: 3, text: "Join VideoSlots family", date: "2019-01-01", finished: false }
      ],
      errors: []
    };
  },
  created: function () {
    this.resetForm()
  },
  methods: {
    resetForm: function() {
      this.newItem = {
        date: moment().format("YYYY-MM-DD")
      }
      this.buttonValue="Add to list"
    },
    moment: function() {
      return moment();
    },
    addMessage: function(event) {
      if (this.newItem.date && this.newItem.text) {
        if (this.newItem.id) {
           let oldItem = this.todoList.find(item => item.id === this.newItem.id);
           oldItem.text = this.newItem.text;
           oldItem.date = this.newItem.date;
        } else {
          this.todoList.push({
            id: this.todoList.length + 1,
            text: this.newItem.text,
            date: this.newItem.date
          });
        }
      
        this.todoList.sort(function(left, right) {
          return moment.utc(left.date).diff(moment.utc(right.date));
        });

        this.resetForm()

      } else {
        this.errors = [];

        if (!this.newItem.date) {
          this.errors.push("Date required.");
        }
        if (!this.newItem.text) {
          this.errors.push("Text required.");
        }
      }
    },
    deleteMessage: function(item) {
      this.todoList.splice(this.todoList.indexOf(item), 1);
      this.resetForm()
    },
    editMessage: function(item) {
      this.newItem = {
        id: item.id,
        text: item.text,
        date: item.date
      }
      this.buttonValue = "Edit item"
    }
  },
  filters: {
    moment: function(date) {
      return moment(date, "YYYY-MM-DD").format("DD. MM. YYYY");
    }
  }
};
</script>

<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.fade-enter {
  opacity:0;
}

.fade-enter-active{
  animation: fadein 1s;
}

.fade-leave {
  opacity:1;
}

.fade-leave-active {
  animation: fadein 1s reverse;
}

.done {
  background-color: silver;
  opacity:0.7;
}


@keyframes fadein {
  from {opacity: 0;}
  to   {opacity: 1;}
}

.bg-change-trans {
  transition: .5s;
}

input[type='checkbox'] {
  height: 35px;
  width: 35px;
}
</style>
