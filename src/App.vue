<template>
  <div id="app">
    <div class="conainerObtenerFraccion">
      <div>
        <button class="btnObtenerFraccion" @click="obtenerFraccion">Obtener fracción</button>
      </div>
      <div class="fraccion">
        {{this.numerador}}{{this.separador}}{{this.denominador}}
      </div>
    </div>
    <div class="containerRectangulo">
      <table class="rectangulo">
        <td   class="celda" v-for="(element, index) in numeradorRectangulo" :key="index" >
         {{element}}
        </td>
      </table>
    </div>
    <div>
      <button class="btnDenominador" @click="aumentarDenominador">+ Denominador</button>
      <button class="btnDenominador" @click="disminuirDenominador">- Denominador </button>
      <button class="btnNumerador" @click="aumentarNumerador">+ Numerador</button>
      <button class="btnNumerador" @click="disminuirNumerador">- Numerador</button>
    </div>
    <div>
      <button class="resultado" @click="obtenerResultado">Obtener Resultado </button>
      <p v-if="resultado" class="textoResultado">{{resultado}}</p>
    </div>
  </div>
</template>
<script>
export default {
  name: 'App',
  data() {
    return {
      contador:0,
      denominador:null,
      numerador: null,
      numeradorRectangulo:[ ],
      resultado:'',
      resultadoNumerador: null,
      resultadoDenominador: null,
      separador:''
    }
  },
    computed:{

},
    methods:{
    obtenerFraccion() {
      this.denominador = Math.floor(Math.random() * (11 - 2)) + 2;
      this.numerador = Math.floor(Math.random() * (this.denominador - 1)) + 1;
      this.separador='/'
      this.resultadoNumerador = null;
      this.resultadoDenominador = null;
      this.numeradorRectangulo= [];
      this.contador= 0;
      this.resultado = '';
    },
    aumentarDenominador(){
      if(this.numerador){
        this.numeradorRectangulo.push(this.active);
        this.resultadoDenominador= this.numeradorRectangulo.length
        console.log( this.resultadoDenominador)
      }
    },
    disminuirDenominador(){
      if(this.numerador){
        this.numeradorRectangulo.pop();
        this.resultadoDenominador= this.numeradorRectangulo.length
        console.log( this.resultadoDenominador)
      }
    },
    aumentarNumerador(){
      if(this.numerador){
        let celdas = document.querySelectorAll('.celda');
        if(celdas.length > this.contador){
          this.contador++
          for (let el = 0; el < celdas.length; el++) {     
            const colorear = celdas[this.contador-1]; 
            colorear.classList.add("colorear");   
          }
        }
      }
      this.resultadoNumerador= this.contador
      console.log(this.resultadoNumerador)
    },
    disminuirNumerador(){
      if(this.numerador){
        let celdas = document.querySelectorAll('.celda');
        if(this.contador > 0){
          this.contador--
          for (let el = 0; el < celdas.length; el++) {     
            const colorear = celdas[this.contador]; 
            colorear.classList.remove("colorear");   
          }
        }
      }
      this.resultadoNumerador= this.contador
      console.log('-',this.resultadoNumerador)
    },
    obtenerResultado(){
      if(this.numerador){
        if((this.numerador == this.resultadoNumerador && this.denominador == this.resultadoDenominador)||(this.numerador/this.denominador==this.resultadoNumerador/this.resultadoDenominador)){
          this.resultado='¡Resultado correcto!'
          const resultadoOk = document.querySelectorAll('.rectangulo');
          resultadoOk[0].classList.add('rectanguloOK')
          resultadoOk[0].classList.remove('rectanguloKo')
        }else{
          this.resultado='Resultado incorrecto, ¡INTENTALO DE NUEVO!'
          const resultadoKO = document.querySelectorAll('.rectangulo');
          resultadoKO[0].classList.add('rectanguloKo')
          resultadoKO[0].classList.remove('rectanguloOK')
        }
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body{
  margin: 0; 
  padding: 0;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: #182a3f;
  background-image: url("@/assets/fondo.jpg");
}
/* obtener fraccion */
.conainerObtenerFraccion{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.fraccion{
  padding: 15px 25px;
  font-size: 34px;
  font-weight: bold;
  background: rgb(135, 160, 197);
  text-align: center;
  height: 40px;
  width: 40px;
  padding: 15px 25px 15px 25px;
  margin: 30px 30px 30px 30px;
  display: flex;
  justify-content: center;
}

.btnObtenerFraccion{
  padding: 15px 25px;
  margin: 30px 30px 30px 30px;
  font-size: 24px;
  text-align: center;
  cursor: pointer;
  outline: none;
  color: #fff;
  background-color: #04AA6D;
  border: none;
  border-radius: 15px;
  box-shadow: 0 9px #999;
}
.btnObtenerFraccion:hover {background-color: #3e8e41}

.btnObtenerFraccion:active {
  background-color: #3e8e41;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
}

/* rectangulo */
.containerRectangulo{
  display: flex;
  justify-content: center;;
}
.rectangulo{
  width: 90%;
  height: 150px;
  border: 5px solid #acacdf;
  background: rgb(135, 160, 197);
}
.celda{
  background: rgb(87, 134, 204);
}

.colorear{
  background:rgb(11, 5, 63);
}
.rectanguloKo{
  animation: error 1s forwards;
}
.rectanguloOK{
  animation: correcto 1s forwards;
  border: 5px solid #04a828;
}

/* botonera numerador denominador */
.btnDenominador{
  padding: 15px 25px;
  margin: 30px 30px 30px 30px;
  font-size: 24px;
  text-align: center;
  cursor: pointer;
  outline: none;
  color: #fff;
  background-color: #ae2bc9;
  border: none;
  border-radius: 15px;
  box-shadow: 0 9px #999;
}
.btnDenominador:hover {background-color: #621172}

.btnDenominador:active {
  background-color: #621172;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
}
.btnNumerador{
  padding: 15px 25px;
  margin: 30px 30px 30px 30px;
  font-size: 24px;
  text-align: center;
  cursor: pointer;
  outline: none;
  color: #fff;
  background-color: #acc92b;
  border: none;
  border-radius: 15px;
  box-shadow: 0 9px #999;
}
.btnNumerador:hover {background-color: #687e07}

.btnNumerador:active {
  background-color: #687e07;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
}

/* boton obtener resultado */
.resultado{
  padding: 15px 25px;
  margin: 30px 30px 30px 30px;
  font-size: 24px;
  text-align: center;
  cursor: pointer;
  outline: none;
  color: #fff;
  background-color: #d61b34;
  border: none;
  border-radius: 15px;
  box-shadow: 0 9px #999;
}
.resultado:hover {background-color: #740715}

.resultado:active {
  background-color: #740715;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
}
.textoResultado{
  font-size: 34px;
  font-weight: bold;
  background: rgb(135, 160, 197);
  text-align: center;
  padding: 15px 25px;
  margin: 30px 30px 30px 30px;
}

/* animaciones */
  @keyframes error {
	0% {
    transform: translate(0, 0);
    border: 5px solid #acacdf;
	}

	10%, 30%, 50%, 70%, 90% {
    transform: translate(-20px,0);
	}

	20%, 40%, 60%, 70%, 80% {
    transform: translate(20px, 0);
		border: 10px solid red;
	}
  
	100% {
    transform: translate(0, 0);
		border: 5px solid #acacdf;
	}
}
@keyframes correcto {
	0% {
    transform: translate(0, 0);
    border: 5px solid #acacdf;
	}

	10%, 30%, 50%, 70%, 90% {
    transform: translate(-20px,0);
	}

	20%, 40%, 60%, 70%, 80% {
    transform: translate(20px, 0);
    border: 10px solid #04a828;
	}
  
	100% {
    transform: translate(0, 0);
		border: 5px solid #acacdf;
	}
}

</style>
