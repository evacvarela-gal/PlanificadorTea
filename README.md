# Planificador Visual TEA

[![Licenza: CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](https://creativecommons.org/licenses/by/4.0/deed.gl)

Aplicación web de planificación visual con pictogramas ARASAAC para alumnado con Trastorno do Espectro Autista (TEA): tiras de anticipación, editor de frases con lematización, axenda visual e biblioteca de pictogramas personalizável.

Desenvolvida orixinalmente para o **CEIP Plurilingüe Santo Estevo de Parga** (Galicia), para uso en Educación Infantil e Primaria.

---

## Que fai

- **Tira visual (Primeiro/Despois)**: crea tiras de tarefa e recompensa con pictogramas para estruturar a sesión. Inclúe espazo de "Rematado" e previsualización imprimible.
- **Editor de frases**: converte calquera frase en galego ou castelán en pictogramas ARASAAC, eliminando automaticamente os conectores gramaticais (artigos, preposicións) para seguir o principio de linguaxe telegráfica.
- **Anticipación paso a paso**: planifica saídas, eventos ou rutinas en secuencias de ata 4 pasos, con pictogramas e texto de apoio.
- **Biblioteca de pictogramas**: xestiona os pictogramas cargados, organizados por categorías personalizables. Permite engadir novos pictogramas desde a API de ARASAAC ou subir imaxes propias (base64, sen custos de almacenamento externo).
- **Perfís de alumnado**: xestiona varios perfís con datos de nivel comunicativo, comprensión e expresión. As frases gardadas son individuais por alumno/a; a biblioteca de pictogramas é compartida.
- **Configuración**: exportación e importación de datos en JSON para copia de seguridade.

---

## Pautas pedagóxicas incorporadas

A aplicación está deseñada segundo os principios de uso de axudas visuais para alumnado con TEA:

- **Linguaxe telegráfica**: só substantivos e verbos clave; sen conectores que engadan "ruído" visual.
- **Secuenciación esquerda-dereita**: os pictogramas organízanse linealmente seguindo a dirección natural de lectura.
- **Sistema "Rematado"**: espazo específico para que o alumnado retire o pictograma ao completar cada paso.
- **Máximo de 4 pasos**: límite na tira de anticipación para evitar sobrecarga.
- **Coherencia de códigos**: os mesmos pictogramas úsanse na aula e na casa para facilitar a xeneralización.

---

## Como está construída

- **Un único ficheiro HTML** (`index.html`) con toda a estrutura, estilos e lóxica. Non require compilación nin instalación de dependencias.
- **Firebase Realtime Database** (SDK modular v12) para gardar e sincronizar datos entre dispositivos.
- **API pública de ARASAAC** para buscar e engadir pictogramas en liña.
- **GitHub Pages** para a publicación.

---

## Instalación nun centro novo

Calquera centro pode implementar a súa propia copia. Necesítanse unha conta de GitHub e unha conta de Google (para Firebase), ambas gratuítas.

### 1. Copiar o proxecto

1. Crea un repositorio novo na túa conta de GitHub.
2. Sube o ficheiro `index.html` e o ficheiro `LICENSE`.

### 2. Crear a base de datos en Firebase

1. Entra en [https://console.firebase.google.com](https://console.firebase.google.com) e crea un proxecto novo.
2. No menú **Compilación → Realtime Database**, crea unha base de datos (rexión recomendada: `europe-west1`).
3. En **Configuración do proxecto → As túas aplicacións**, rexistra unha aplicación web e copia o obxecto `firebaseConfig`.
4. No ficheiro `index.html`, localiza o bloque `firebaseConfig` e substitúe os valores polos do teu proxecto:

```js
const firebaseConfig = {
  apiKey: "A_TÚA_CLAVE",
  authDomain: "o-teu-proxecto.firebaseapp.com",
  databaseURL: "https://o-teu-proxecto-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "o-teu-proxecto",
  storageBucket: "o-teu-proxecto.firebasestorage.app",
  messagingSenderId: "...",
  appId: "..."
};
```

### 3. Regras da base de datos

En **Realtime Database → Regras**, configura acceso público (a aplicación non usa autenticación de Firebase):

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

> Isto implica que a base de datos é pública. Non gardes nela información persoal identificable do alumnado; usa sempre iniciais.

### 4. Publicar con GitHub Pages

1. No repositorio, vai a **Settings → Pages**.
2. En **Source**, escolle a rama (`main`) e a carpeta raíz (`/root`).
3. Garda. En poucos minutos a aplicación estará dispoñible no enderezo que indica GitHub.

### 5. Adaptar ao teu centro

Abre a aplicación, crea os perfís de alumnado desde a pestana **Alumnado** e comeza a engadir pictogramas á biblioteca desde **Biblioteca de pictogramas → Buscar en ARASAAC**.

---

## Desenvolvemento local

Para probar cambios antes de publicar, abre o `index.html` directamente no navegador. Firebase non funciona co protocolo `file://`; a sincronización en tempo real funciona unha vez publicada en GitHub Pages (`https://`).

---

## Implementación noutro centro

Os centros interesados en implementar este planificador poden solicitalo como **actividade de formación do PFPP** (Plan de Formación Permanente do Profesorado).

Contacto: **evamariacorredoira@edu.xunta.gal**

---

## Nota sobre os pictogramas ARASAAC

Os pictogramas utilizados pertencen ao sistema [ARASAAC](https://arasaac.org) (Portal Aragonés de Comunicación Aumentativa y Alternativa). O Goberno de Aragón é titular dos dereitos e distribúeos baixo licenza **CC BY-NC-SA 4.0**. Esta aplicación accede a eles en liña a través das URL públicas de ARASAAC e non os redistribúe nin almacena de forma permanente no código.

---

## Autoría e licenzas

- **Idea, deseño pedagóxico e planificación**: Eva C. Varela [![ORCID](https://img.shields.io/badge/ORCID-0009--0008--4320--4886-green)](https://orcid.org/0009-0008-4320-4886)
- **Programación**: Claude (Anthropic)

© 2026 Eva C. Varela

Este proxecto distribúese baixo **dúas licenzas**:

- O **concepto, o deseño pedagóxico e a planificación** están baixo licenza **Creative Commons Recoñecemento 4.0 Internacional (CC BY 4.0)**: pódense copiar, adaptar e implementar noutros centros sempre que se manteña o recoñecemento da autoría de Eva C. Varela.
- O **código fonte** está baixo licenza **MIT**.

Consulta o ficheiro [`LICENSE`](LICENSE) para os textos completos.
