<template>
  <div class="hello">

    <div id="info" v-bind:class="{displayed: hideInfo}">
      <ul>
        <li>Title: {{ infobook}}</li>
        <li>Author: {{infoauthor}}</li> 
        <li>Read: {{ infoisBookRead }}</li>
        <li>Pages: {{infopages}}</li>
      </ul>

    </div>


    <div name="formdiv">
      <form @submit.prevent="addBook">
          <input type="text" placeholder="Name of your book.." v-model="book">
          <input type="text" placeholder="Author.." v-model="author">
          <input type="text" placeholder="Number of pages.." v-model="pages">
          <div id="checkdiv">
            <p>The Book is read:</p>
            <div id="checkcontainer">
              <input type="checkbox" id="checkbox" v-model="checked">
            </div>
          </div>

          <input id="submit" type="submit">
      
      </form>
    </div>

    <div class="holder">
      <ul>
        <li v-on:click="showInfo(index)" v-for="(data, index) in books" :key='index'>{{ data.book}} <i id = "remove" class="fa fa-minus-circle" v-on:click="remove(index)"></i>
        </li>
      </ul>
    </div>
    


  </div>
</template>

<script>
export default {
  name: 'Booklibrary',

  data() {
    return {
      infobook: '',
      infoauthor: '',
      infoisBookRead: '',
      infopages: '',
      hideInfo: true,
      checked: false,
      isBookRead: '',
      pages: '',
      author: '',
      book: '',
      books: [
        {
          "book": "Harry Potter",
          "author": "JK Rowling",
          "isBookRead": true,
          "pages": "349",
        },
        {
        "book": "1984",
        "author": "George Orwell",
        "isBookRead": false,
        "pages": "240",
        },
      ],
    }
  },

  methods : {
      addBook() {
        this.books.push({book: this.book, author: this.author, isBookRead: this.checked, pages: this.pages});
        this.book= '';

      },
      remove(id) {
        this.books.splice(id, 1);
      },
      showInfo(id) {
          this.hideInfo = false;

          this.infobook = this.books[id].book
          this.infoauthor = this.books[id].author
          if(this.books[id].isBookRead == true) {
            this.infoisBookRead = "Yes"
          } else {
            this.infoisBookRead = "No"
          }
          this.infopages = this.books[id].pages


      }

  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css"; 

  .holder {
    background: #fff;
  }

  ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }
  
  ul li {
    padding: 20px;
    font-size: 1.3em;
    background-color: #E0EDF4;
    border-left: 5px solid #3EB3F6;
    margin-bottom: 2px;
    color: #3E5252;
  }

  p {
    text-align:center;
    padding: 30px 0;
    color: gray;
  }

  .container {
    box-shadow: 0px 0px 40px lightgray;
  }



  input:not([type="checkbox"]), #checkdiv {
    width: calc(100% - 40px);
    border: 0;
    padding: 20px;
    font-size: 1.3em;
    background-color: #323333;
    color: #687F7F;
  }

  #checkdiv {
    display:flex;
    align-items:center;

    
  }


  #checkdiv p {
    margin: 0;
    padding: 0;
  
  }

  #checkcontainer {
    margin-left: 5%;
  }

  #submit {
    display:none;
  }



  .displayed {
    display: none;
  }

  #remove {
    float:right;
  }
</style>
