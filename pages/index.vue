<template>
  <div class="ind-container">
    <div id="header-panel" class="panel panel-dark-blue panel-no-border trailer-half">
      <div class="font-size-2">Connection Speed Test</div>
    </div>

    <div id="connection-test-panel" class="panel panel-white panel-no-border">
      <div class="trailer-half">
        <mark class="label label-grey font-size-3">1</mark>
        <div class="inline-block padding-left-half">Test Current Internet Speed</div>
      </div>
      <div class="panel panel-dark-grey panel-no-border"></div>
      <div id="speed-test-panel" class="panel panel-light-blue panel-no-border">
        <div class="text-center">
          <button
            id="speed-test-btn"
            class="btn btn-large btn-teal font-size-1 icon-ui-dashboard leader-quarter trailer-half"
          >click here to test download speed</button>
          <div class="form-container">
            <div id="sc-container">
              <div id="sc-branding" class="sc-bb">
                <a target="_blank" href="https://www.speedcheck.org/">
                  <img
                    src="https://cdn.speedcheck.org/branding/speedcheck-logo-18.png"
                    alt="Speedcheck"
                  />
                </a>
              </div>
            </div>
          </div>
          <script src="https://cdn.speedcheck.org/basic/scbjs.min.js" async></script>
          <div id="speed-test-label" class="font-size-0 avenir-bold-italic text-black">...</div>
        </div>
      </div>
    </div>

    <div id="survey-panel" class="panel panel-white panel-no-border hide">
      <div class="trailer-half">
        <mark class="label label-grey font-size-3">2</mark>
        <div class="inline-block padding-left-half">Submit Internet Speed Survey</div>
      </div>
      <div id="survey123-webform" class="panel panel-no-padding panel-no-border"></div>
    </div>
  </div>
</template>

<script>
  var open = window.XMLHttpRequest.prototype.open,
        send = window.XMLHttpRequest.prototype.send;
      function openReplacement(method, url, async, user, password) {
        this._url = url;
        return open.apply(this, arguments);
      }
      function sendReplacement(data) {
        if (this._url == "https://api.speedspot.org/basic" && arguments[0]) {
          console.log(arguments[0]);
          vm.results = JSON.parse(arguments[0]);
        }
        return send.apply(this, arguments);
      }
      window.XMLHttpRequest.prototype.open = openReplacement;
      window.XMLHttpRequest.prototype.send = sendReplacement;

    define([
      "calcite",
      "dojo/_base/declare",
      "esri/identity/IdentityManager",
      "esri/core/promiseUtils"
    ], function(calcite, declare, IdentityManager, promiseUtils, initializeSurvey){
      return declare([], {

        /**
        *
        */
        constructor: function(){

          // INITIALIZE CALCITE WEB //
          calcite.init();

          // INITIALISE SURVEY //
          this.initializeSurvey();

        },

      /**
      *  INITIALIZE SURVEY123 FORM AFTER CONNECTION SPEED TEST //
      */

            //
            // SURVEY123 WEB FORM //
            //

            let webform = new Survey123WebForm({
              container: "survey123-webform",
              clientId: "Jy4JtM71ralXVggd",
              portalUrl: "https://www.arcgis.com",
              itemId: "f7d1b61670ec49788a8a9f246f5b2e9b",
              onFormLoaded: (data) => {

                //
                // ANSWER INTERNET SPEED QUESTION WITH CONNECTION SPEED INFO //
                //
                Survey123WebForm.setQuestionValue({ "internet_speed": speedMbps });
              }
            });

            // SHOW SURVEY123 FORM //
            surveyPanel = document.getElementById('survey-panel');
            surveyPanel.classList.remove('hide');

          });
        });

      },

</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
  width: 100%;
  height: auto;
  font-size: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-text-size-adjust: 100%;
  -ms-text-size-adjust: 100%;
}

body {
  background-color: #fff;
  display: flex;
  flex-direction: column;
}

#speed-test-panel {
  flex-shrink: 0;
  flex-grow: 0;
  min-width: 0;
  min-height: 0;
  display: flex;
  flex-direction: column;
}

.panel-dark-blue {
  background-color: #626060;
}

.panel-light-blue {
  background-color: #f4f1f1;
}

.panel-dark-grey {
  background-color: #626060;
}

.label-grey {
  background-color: #626060;
  color: #fff;
}

.btn-teal {
  background: #1dddd9;
  color: #fff;
  border: 1px solid #1dddd9;
}

#survey123-webform {
  height: auto;
  flex-shrink: 1;
  flex-grow: 1;
  min-width: 0;
  min-height: 0;
}
</style>
