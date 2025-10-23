# dispositivosmoveis26
<img width="25" height="27" alt="ar_hand_prompt" src="https://github.com/user-attachments/assets/35dff3eb-4feb-4c1c-9097-e3f071be38e0" />
<!doctype html>
<html lang="en"><img width="72" height="72" alt="ar_icon" src="https://github.com/user-attachments/assets/8daf18fe-061c-4e5d-938c-3d45a4add4e0" />

  <head>
    <title>&lt;model-viewer&gt; template</title>
    <meta charset="utf-8">
    <meta name="description" content="&lt;model-viewer&gt; template">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link type="text/css" href="./styles.css" rel="stylesheet"/>
  </head>
  <body>
    <!-- <model-viewer> HTML element -->
    <model-viewer src="BoomBox.glb" ar ar-modes="webxr scene-viewer quick-look" camera-controls tone-mapping="neutral" poster="poster.webp" shadow-intensity="1">
      <div class="progress-bar hide" slot="progress-bar">
          <div class="update-bar"></div>
      </div>
      <button slot="ar-button" id="ar-button">
          View in your space
      </button>
      <div id="ar-prompt">
          <img src="ar_hand_prompt.png">
      </div>
    </model-viewer>  
    <script src="script.js"></script>
    <!-- Loads <model-viewer> for browsers: -->
    <script type="module" src="https://ajax.googleapis.com/ajax/libs/model-viewer/4.0.0/model-viewer.min.js"></script>
  </body>
</html>
// Handles loading the events for <model-viewer>'s slotted progress bar
const onProgress = (event) => {
  const progressBar = event.target.querySelector('.progress-bar');
  const updatingBar = event.target.querySelector('.update-bar');
  updatingBar.style.width = `${event.detail.totalProgress * 100}%`;
  if (event.detail.totalProgress === 1) {
    progressBar.classList.add('hide');
    event.target.removeEventListener('progress', onProgress);
  } else {
    progressBar.classList.remove('hide');
  }
};
document.querySelector('model-viewer').addEventListener('progress', onProgress);
<model-viewer src="BoomBox.glb" ar ar-modes="webxr scene-viewer quick-look" camera-controls tone-mapping="neutral" poster="poster.webp" shadow-intensity="1">
    <div class="progress-bar hide" slot="progress-bar">
        <div class="update-bar"></div>
    </div>
    <button slot="ar-button" id="ar-button">
        View in your space
    </button>
    <div id="ar-prompt">
        <img src="https://modelviewer.dev/shared-assets/icons/hand.png">
    </div>
</model-viewer>

:not(:defined) > * {
  display: none;
}

html {
  height: 100%;
}

body {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
}

model-viewer {
  width: 100%;
  height: 90%;
  background-color: #ffffff;
}


.progress-bar {
  display: block;
  width: 33%;
  height: 10%;
  max-height: 2%;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate3d(-50%, -50%, 0);
  border-radius: 25px;
  box-shadow: 0px 3px 10px 3px rgba(0, 0, 0, 0.5), 0px 0px 5px 1px rgba(0, 0, 0, 0.6);
  border: 1px solid rgba(255, 255, 255, 0.9);
  background-color: rgba(0, 0, 0, 0.5);
}

.progress-bar.hide {
  visibility: hidden;
  transition: visibility 0.3s;
}

.update-bar {
  background-color: rgba(255, 255, 255, 0.9);
  width: 0%;
  height: 100%;
  border-radius: 25px;
  float: left;
  transition: width 0.3s;
}

#ar-button {
  background-image: url(ar_icon.png);
  background-repeat: no-repeat;
  background-size: 20px 20px;
  background-position: 12px 50%;
  background-color: #fff;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  white-space: nowrap;
  bottom: 16px;
  padding: 0px 16px 0px 40px;
  font-family: Roboto Regular, Helvetica Neue, sans-serif;
  font-size: 14px;
  color:#4285f4;
  height: 36px;
  line-height: 36px;
  border-radius: 18px;
  border: 1px solid #DADCE0;
}

#ar-button:active {
  background-color: #E8EAED;
}

#ar-button:focus {
  outline: none;
}

#ar-button:focus-visible {
  outline: 1px solid #4285f4;
}

@keyframes circle {
  from { transform: translateX(-50%) rotate(0deg) translateX(50px) rotate(0deg); }
  to   { transform: translateX(-50%) rotate(360deg) translateX(50px) rotate(-360deg); }
}

@keyframes elongate {
  from { transform: translateX(100px); }
  to   { transform: translateX(-100px); }
}

model-viewer > #ar-prompt {
  position: absolute;
  left: 50%;
  bottom: 60px;
  animation: elongate 2s infinite ease-in-out alternate;
  display: none;
}

model-viewer[ar-status="session-started"] > #ar-prompt {
  display: block;
}

model-viewer > #ar-prompt > img {
  animation: circle 4s linear infinite;
}
