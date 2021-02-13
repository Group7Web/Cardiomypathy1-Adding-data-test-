<template>
  <div id="uploadForm">
    <form @submit="checkForm($event)">
      <div>
        <input
          type="text"
          v-model="uploadTitle"
          name="uploadTitle"
          id="uploadTitle"
        />
      </div>
      <div>
        <input
          type="text"
          v-model="uploadDetails"
          name="uploadDetails"
          id="uploadDetails"
        />
      </div>
      <div>
        <input type="file" accept=".csv" @change="handleFileChange($event)"/>
      </div>
      <input type="submit" />
    </form>
  </div>
</template>

<script>
import Papa from 'papaparse'
export default {  
  name: '#uploadForm',
  data() {
    return {
      config: {
          delimiter: "", // auto-detect
            newline: "", // auto-detect
            quoteChar: '"',
            escapeChar: '"',
            header: true,
            dynamicTyping: true,
            preview: 0,
            encoding: "",
            delimitersToGuess: [',', '\t', '|', ';']
      },
      uploadTitle: '',
      uploadDetails: '',
      fileData: null,
      uploadValue: 0,
      availabilty: null
    }
  },
  methods: {
    handleFileChange(evt){
      var file = evt.target.files[0]
      Papa.parse(file,{
        header: true,
        complete: function (results){
          this.availabilty=results.data;
          console.log(this.availabilty);
        }
      })
    },
    checkForm(evt) {
      evt.preventDefault();
     
      if (!this.uploadTitle || !this.uploadDetails || this.availabilty == null) {
        alert("Please fill all inputs")
      } else {
        this.onUpload()
      }
    },
    onUpload() {
      
      console.log("it works")
      }
      
   
      }

      
    }
</script>
