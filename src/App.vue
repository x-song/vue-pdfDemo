<template>
  <div id="app">
    <img src="./assets/logo.png">



   <div>
		<pdf
		
			:src="src"
			:page="num"
			style="display: inline-block; width: 50%"
		></pdf>
	</div>
<button @click="fn2">-</button>
<button @click="fn1">+</button>
  
  </div>
</template>

<script>

import pdf from 'vue-pdf'

var loadingTask = pdf.createLoadingTask('https://cdn.mozilla.net/pdfjs/tracemonkey.pdf');

export default {
 
	components: {
		pdf
	},
	data() {
		return {
      num:1,
			src: loadingTask,
			numPages: undefined,
		}
  },
  methods:{
    fn1(){
      if(this.num<= this.numPages){
        this.num ++;
      }else{
        this.num= this.numPages;
      }
    },
    fn2(){
      if(this.num<1){
        this.num = 1;
      }else{
         this.num --;
      }
    }
  },
	mounted() {

		this.src.then(pdf => {
     
      this.numPages = pdf.numPages;
       console.log(pdf.numPages);
		});
	}
}

</script>