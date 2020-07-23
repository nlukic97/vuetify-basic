<template>
  <v-container>
    <v-row>
      <v-col>
        <h1>Priloži žalbu</h1>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col cols="6" align="center">
        <v-form>

          <v-row no-gutters> <!-- !!!   1. mnogo veliki vetrikalni gutter kad se ukloni 'no-gutters' --->
            <v-col cols="12" md="6">
              <v-text-field label="Name" outlined autofocus class="mr-md-2"></v-text-field>
            </v-col>

            <v-col cols="12" md="6">
              <v-text-field label="Surname" outlined class="ml-md-2"></v-text-field>
            </v-col>
          </v-row>

          <v-row no-gutters>  <!-- !!!    1. mnogo veliki verticalni gutter kad se ukloni 'no-gutters' --->

            <v-col cols="12" md="6">
              <v-text-field label="Broj lične karte" outlined class="mr-md-2"></v-text-field>
            </v-col> 

            <!-- 2. Ovde izmedju nastaje neki razmak koji ne znam kako da uklonim. Mozda sam resio sa ovim gore: !!!      ???? -->

            <v-col cols="12" md="6"> 
              <v-text-field label="Kontakt Telefon" outlined class="ml-md-2"></v-text-field>
            </v-col>

          </v-row>
          
          <v-radio-group class="mb-5">
            <h2>Pol</h2>
            <v-radio label="muški"></v-radio>
            <v-radio label="ženski"></v-radio>
            <v-radio label="Susdržan"></v-radio>
          </v-radio-group>

          <v-select class="mb-5" :items="opstine" label="Opština" outlined>
          </v-select>
          
          <h2>Da li ste osigurani?</h2>
          <v-radio-group class="mb-5"> <!-- row -->
            <v-radio label="Da"></v-radio>
            <v-radio label="Ne"></v-radio>
          </v-radio-group>

          <h2>Radni status</h2>
          <div class="mb-5 d-flex flex-wrap justify-lg-center justify-md-flex-start justify-sm-flex-start"> <!-- 3. jel ovo ok resenje? Mozda neki media query da dodam klasu drugu neku, tj da sirina svih ovih bude 100% (na 714px) -->
              <v-checkbox label="Student" class="mr-3" v-model="radniStatus.student" @change="nezaposlenUnchecked"></v-checkbox>
              <v-checkbox label="nezaposlen" class="mr-3" v-model="radniStatus.nezaposlen" @change="nezaposlenChecked"></v-checkbox>
              <v-checkbox label="stalno zaposlen" class="mr-3" v-model="radniStatus.stalnoZaposlen" @change="nezaposlenUnchecked"></v-checkbox>
              <v-checkbox label="privremeno zaposlen" class="mr-3" v-model="radniStatus.privremenoZaposlen" @change="nezaposlenUnchecked"></v-checkbox>
          </div>

          <div>
            <p>{{radniStatus.student}}</p>
            <p>{{radniStatus.nezaposlen}}</p>
            <p>{{radniStatus.stalnoZaposlen}}</p>
            <p>{{radniStatus.privremenoZaposlen}}</p>
          </div>

          <h2>Koliko ste nezadovoljni?</h2>
          <v-row class="mb-5">
            <v-col cols="9" md="10">
              <div>
                <v-slider value="10" v-model="sliderValue"></v-slider>
              </div>
            </v-col>
            <v-col cols="3" md="2"> 
              <div>
                <h4>{{sliderValue}} %</h4>
              </div>
            </v-col>
          </v-row>

          <v-textarea outlined label="Vaša poruka"></v-textarea>
          
          <v-btn outlined color="primary">Submit</v-btn>

        </v-form>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',

    data: function(){
      return {
        opstine: [
          'Zvezdara',
          'Stari Grad',
          'Zemun',
          'Vračar'
        ],
        sliderValue: 10,
        radniStatus:{
          student: false,
          nezaposlen:false,
          stalnoZaposlen:false,
          privremenoZaposlen:false
        }
      }
    },
    methods:{
      //kad se klikne na "nezaposlen"
      nezaposlenChecked: function(){ //funkcija koja nakon validiranje potvrdi celu pricu
        if(this.radniStatus.nezaposlen == true){
          this.radniStatus.nezaposlen = true;
          this.radniStatus.student = false;
          this.radniStatus.stalnoZaposlen = false;
          this.radniStatus.privremenoZaposlen = false;
        } else {
          this.radniStatus.nezaposlen = false;
        }
      },

      //kad se klikne bilo gde a da nije "nezaposlen"
      nezaposlenUnchecked: function() {
        if(this.radniStatus.nezaposlen == true){
          this.radniStatus.nezaposlen = false;
        }
      }
    }
  }
</script>
<style>
h1 {
  text-align:center;
}

.v-slider--horizontal {
  display:none;
  /* Ovako radi bato */
      /*display:none!important;*/ 
}

/* @media screen { width: 7112px
  
} */
</style>