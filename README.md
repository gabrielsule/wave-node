Cuando subimos audio a nuestro servidor y queremos darle un L&F al mejor estilo SoundCloud pero sin utilizar un reproductor de terceros, tenemos la posibilidad de generar el nuestro con la librería wavesurfer.js

### Instalación de dependencias
```bash
npm i express

npm i pug
```

### Descarga de wavesurfer.js
[wavesurfer.min.js](https://unpkg.com/wavesurfer.js@3.1.0/dist/wavesurfer.min.js)

### Estructura
```bash
├───public/
│   ├───audio/
│   │   └───33.mp3
│   └───js/
│       └───wavesurfer.min.js
├───views/
│   └───index.pug
├───index.js
└───package.json
```

### Creación de index.js
```javascript
const express = require('express');
const app = express();

app.use(express.static('./public'));

app.set('view engine', 'pug');
app.set('views', './views');

app.get('/', (req, res) => {
    res.render('index');
});

const port = process.env.PORT || 3000;
app.listen(port, () => {
    console.log(`server en port ${port}`)
});
```

### Creación de index.pug
```javascript
doctype html
head
  meta(charset='UTF-8')
  meta(name='viewport' content='width=device-width, initial-scale=1.0')
  meta(http-equiv='X-UA-Compatible' content='ie=edge')
  title Wave33
  script(src='/js/wavesurfer.min.js')
#waveContainer
script.
  var wavesurfer = WaveSurfer.create({
  container: '#waveContainer',
  waveColor: 'red',
  progressColor: 'green'
  });
  wavesurfer.load('audio/33.mp3');
  wavesurfer.on('ready', function () {
  wavesurfer.play();
  });
```
