<script>
	export let selectedGender = null;
	export let selectedActivityLevel = null;
	export let height = 0;
	export let weight = 0;
	export let age = 0;
	export let result = 0;
  
	function getActivityMultiplier(level) {
        switch (level) {
            case 'Sedentario (0 a 2 hrs por semana)':
                return 1.2;
            case 'Actividad Leve (3 a 5 hrs por semana)':
                return 1.55;
            case 'Actividad Moderada (6 hrs por semana)':
                return 1.78;
            case 'Actividad Intensa (4 - 5 hrs diarias)':
                return 2.1;
            default:
                return 1.0;
        }
    }

    // Aquí indicas que cuando cualquiera de estas variables cambie, se debe volver a calcular
    $: if (selectedGender && selectedActivityLevel && height && weight && age) {
        calculateCalories();
    }

    function calculateCalories() {
        if (selectedGender === 'Hombre') {
            result = (66.473 + (13.7516 * weight) + (5.0033 * height) - (6.755 * age)) * getActivityMultiplier(selectedActivityLevel);
        } else if (selectedGender === 'Mujer') {
            result = (655.0955 + (9.5634 * weight) + (1.8449 * height) - (4.6756 * age)) * getActivityMultiplier(selectedActivityLevel);
        }
        result += result * 0.10; // Agregar el 10% al resultado
    }
  </script>
  
  <main>
	<h1>Calculadora de kcals</h1>
  
	<h2 style="color: black;">¿Eres hombre o mujer?</h2>
	<button 
    	class="rounded-button {selectedGender === 'Hombre' ? 'selected' : ''}" 
    	on:click={() => selectedGender = 'Hombre'}>
    	Hombre
	</button>
	<button 
    	class="rounded-button {selectedGender === 'Mujer' ? 'selected' : ''}" 
    	on:click={() => selectedGender = 'Mujer'}>
    	Mujer
	</button>

  
	<h2 style="color: black;">Nivel de actividad física que realizas</h2>
	<button 
    	class="rounded-button {selectedActivityLevel === 'Sedentario (0 a 2 hrs por semana)' ? 'selected' : ''}" 
    	on:click={() => selectedActivityLevel = 'Sedentario (0 a 2 hrs por semana)'}>
    	Sedentario (0 a 2 hrs por semana)
	</button>
	<button 
		class="rounded-button {selectedActivityLevel === 'Actividad Leve (3 a 5 hrs por semana)' ? 'selected' : ''}" 
		on:click={() => selectedActivityLevel = 'Actividad Leve (3 a 5 hrs por semana)'}>
		Actividad Leve (3 a 5 hrs por semana)
	</button>
	<button 
		class="rounded-button {selectedActivityLevel === 'Actividad Moderada (6 hrs por semana)' ? 'selected' : ''}" 
	 	on:click={() => selectedActivityLevel = 'Actividad Moderada (6 hrs por semana)'}>
		Actividad Moderada (6 hrs por semana)
	</button>
	<button 
		class="rounded-button {selectedActivityLevel === 'Actividad Intensa (4 - 5 hrs diarias)' ? 'selected' : ''}"
		on:click={() => selectedActivityLevel = 'Actividad Intensa (4 - 5 hrs diarias)'}>
		Actividad Intensa (4 - 5 hrs diarias)
	</button>
  
	<h2 style="color: black;">Ingresa tus datos</h2>

	<div class="input-group">
    	<label for="height">Estatura en cm: </label>
    	<input id="height" type="number" placeholder="Estatura en cm" bind:value={height}>
	</div>

	<div class="input-group">
    	<label for="weight">Peso en kg: </label>
    	<input id="weight" type="number" placeholder="Peso en kg" bind:value={weight}>
	</div>

	<div class="input-group">
    	<label for="age">Edad en años: </label>
    	<input id="age" type="number" placeholder="Edad en años" bind:value={age}>
	</div>

  
	<div class="result" style="color: pink;">
	  <p>Las kcals que necesitas para mantener tu peso son: {result.toFixed(2)}</p>
	</div>
  </main>
  
  <style>
	main {
	  text-align: center;
	  font-family: Arial, sans-serif;
	  background: linear-gradient(to bottom, #FF66CC, #6600FF);
	  color: white;
	  padding: 20px;
	}
  
	.rounded-button {
	  background-color: purple;
	  color: white;
	  border: none;
	  padding: 10px 20px;
	  margin: 5px;
	  border-radius: 20px;
	  cursor: pointer;
	}
	
  
	input {
	  padding: 10px;
	  margin: 5px;
	}
	.input-group {
        display: flex;
        justify-content: center;
        align-items: center;
        margin-bottom: 10px;
    }

    .input-group label {
        margin-right: 10px;
    }
	
	.result {
	  font-size: 24px;
	}

	.selected {
    background-color: #81eaf0; /* Color de fondo turquesa */
    color: black; /* Color de texto negro */
	}

  </style>
  
   

  