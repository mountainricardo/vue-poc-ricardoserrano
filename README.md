# savia-test-ricardoserrano

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run your unit tests
```
npm run test:unit
```

### Run your end-to-end tests
```
npm run test:e2e
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

### Ricardo Serrano Solution notes
La prueba se ha realizado con Vue.js.
Es mi primera toma de contacto con Vue.js, por eso mismo he mantenido como nombre del componente que construye la aplicación el de HelloWorld.

Para realizar la prueba he aprovechado vue/cli 4.1.1 y he creado el scaffolding para la aplicación mediante el comando "vue create hello-world" con setup manual para disponer de Typescript, Router, Vuex, CSS Pre-procesors; Linter, Unit Testing y E2E testing (Unit testing y E2E testing han quedado como los instala vue/cli, sin más desarrollo, aunque se ejecutan sin errores).

El IDE empleado ha sido Visual Studio Code.
Para resolver las restricciones CORS he modificado el archivo .vscode/launch.json con la siguiente configuración

    {
        "version": "0.2.0",
        "configurations": [
            {
                "type": "chrome",
                "request": "launch",
                "name": "Launch Chrome against localhost",
                "url": "http://localhost:8080",
                "runtimeArgs": [
                    "--disable-web-security"
                 ],
                "webRoot": "${workspaceFolder}"
            }
        ]
    }
    
y he depurado el desarrollo mediante Chrome ejecutado desde Visual Studio Code.

El componente HelloWorld que construye la prueba se ha desarrollado como single file component, lo que supone que el componente vue y sus métodos, el template para el marcado y el precompilado de los estilos se encuentran dentro del mismo archivo src/components/HelloWorld.vue.

Para ejecutar las request contra el servidor https://saviatest.azurewebsites.net/api he utilizado el cliente HTTP axios (https://github.com/axios/axios) que facilita las requests concurrentes a 
/Calls y /Merits.

Para precompilar los estilos CSS de la aplicación he empleado SASS con un patrón mobile first con dos puntos de corte: mobile (IPhone ES5 320px) y desktop (IPad Pro 1024px), testeados con el emulador de Chrome. No he utilizado ningún reset genérico y me he limitado a resetear las declaraciones necesarias a partir del scafolding creado por vue/cli. Las medidas utilizadas son aproximadas, suficiente para mostrar el comportamiento y renderizado de los elementos, así como su responsividad.

No he desarrollado tests unitarios aparte de los proporcionados por vue/cli con el scafolding. La razón es que nunca he desarrollado tests unitarios para las aplicaciones en las que he trabajado hasta hoy.

El botón "Guardar" existe sólo a efectos de completar la maquetación. No he implementado una request POST para remitir al servidor los cambios realizados en el cliente con la aplicación, aunque dichos cambios sí que modifican el modelo obtenido mediante las request GET, por no estar especificada en las instrucciones. 

El proyecto está disponible en https://github.com/mountainricardo/savia-test-ricardoserrano.git

El tiempo empleado en completar la prueba ha sido de aproximadamente 40 horas.
