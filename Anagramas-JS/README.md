# Verificando con Anagramas

Este repositorio contiene tres métodos diferentes para verificar si dos palabras son anagramas en JavaScript.

## Método 1: Ordenando las letras

La función `areAnagrama1` toma dos palabras como entrada y verifica si son anagramas al ordenar las letras de ambas palabras y luego compararlas.

```javascript
function areAnagrama1(word1, word2) {
    // Función interna para eliminar espacios y convertir a minúsculas
    let removeSpacesAndToLower = function(str) {
        let result = '';
        for (const element of str) {
            if (element !== ('')) {
                result += element.toLowerCase();
            }
        }
        return result;
    };

    // Función interna para ordenar los caracteres de una cadena
    let sortString = function(str) {
        return removeSpacesAndToLower(str).split("").sort().join("");
    }

    // Verificar si las cadenas ordenadas son iguales (si son anagramas)
    return sortString(word1) === sortString(word2);
}

console.log(areAnagrama1('hola', 'olah')); // true
console.log(areAnagrama1('holae', 'aolDah')); // false
console.log(areAnagrama1('pato', 'aotp')); // false


Método 2: Contando la frecuencia de letras
La función areAnagrama2 cuenta la frecuencia de cada letra en ambas palabras y luego verifica si tienen
 la misma cantidad de cada letra.

function areAnagrama2(word1, word2) {
    if (word1.length !== word2.length) {
        return false;
    }

    let letterCount = {};

    for (const char of word1) {
        let lowerChar = char.toLowerCase();
        letterCount[lowerChar] = (letterCount[lowerChar] || 0) + 1;
    }

    for (const char of word2) {
        let lowerChar = char.toLowerCase();
        if (!letterCount[lowerChar]) {
            return false;
        }
        letterCount[lowerChar]--;
    }
    return true;
}

console.log(areAnagrama2('hola', 'olah')); // true
console.log(areAnagrama2('holae', 'aolDah')); // false
console.log(areAnagrama2('pato', 'aotp')); // false

Método 3: Mapa de frecuencia de letras
La función areAnagrama3 utiliza un mapa para registrar la frecuencia de cada letra en ambas palabras y luego
 verifica si los mapas son iguales.

function hasMap(string) {
    let mappedObj = {};
    for (let i of string) {
        if(mappedObj[i] === undefined) mappedObj[i] = 1;
        else mappedObj[i]++;
    }
    return mappedObj;
}

function areAnagrama3(string1, string2) {
    if (string1.length !== string2.length) return false;

    let mappedObj1 = hasMap(string1);
    let mappedObj2 = hasMap(string2);

    for (let key in mappedObj1) {
        if (mappedObj1[key] !== mappedObj2[key]) return false;
    }
    return true;
}

console.log(areAnagrama3('hola', 'olah')); // true
console.log(areAnagrama3('holae', 'aolDah')); // false
console.log(areAnagrama3('pato', 'aotp')); // false

