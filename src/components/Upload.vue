<template>
  <div class="file-upload">
    <div class="file-select">
      <div class="file-select-button" id="fileName">Choose</div>
      <div class="file-select-name noFile">No file chosen...</div>
      <input
        type="file"
        name="chooseFile"
        class="chosenFile"
        @change="loadTextFromFile"
      />
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    loadTextFromFile(ev) {
      const file = ev.target.files[0]
      const reader = new FileReader()

      // // Upload data from JSON and save to store.state.data
      reader.onload = e => this.$store.dispatch('uploadData', e.target.result)
      reader.readAsText(file)

      // Add visual change to input
      const chosenFiles = document.getElementsByClassName('chosenFile')
      let filenames = []

      for (let i = 0; i < chosenFiles.length; i++) {
        filenames[i] = chosenFiles[i].value

        if (/^\s*$/.test(filenames[i])) {
          document
            .getElementsByClassName('file-upload')
            [i].classList.remove('active')
          document.getElementsByClassName('noFile')[i].innerHTML =
            'No file chosen...'
        } else {
          document
            .getElementsByClassName('file-upload')
            [i].classList.add('active')
          document.getElementsByClassName('noFile')[i].innerHTML = filenames[
            i
          ].replace('C:\\fakepath\\', '')
        }
      }
    }
  }
}
</script>

<style style="scss" scoped>
.file-upload {
  display: block;
  text-align: center;
  font-weight: bold;
}
.file-upload .file-select {
  display: block;
  border: 1px solid #ddd;
  color: #34495e;
  cursor: pointer;
  height: 40px;
  line-height: 40px;
  text-align: left;
  background: #ffffff;
  overflow: hidden;
  position: relative;
}
.file-upload .file-select .file-select-button {
  background: #ddd;
  padding: 0 10px;
  display: inline-block;
  height: 40px;
  line-height: 40px;
}
.file-upload .file-select .file-select-name {
  font-weight: normal;
  line-height: 40px;
  display: inline-block;
  padding: 0 8px;
}
.file-upload .file-select:hover {
  border-color: #34495e;
  transition: all 0.2s ease-in-out;
  -moz-transition: all 0.2s ease-in-out;
  -webkit-transition: all 0.2s ease-in-out;
  -o-transition: all 0.2s ease-in-out;
}
.file-upload .file-select:hover .file-select-button {
  background: #34495e;
  color: #ffffff;
  transition: all 0.2s ease-in-out;
  -moz-transition: all 0.2s ease-in-out;
  -webkit-transition: all 0.2s ease-in-out;
  -o-transition: all 0.2s ease-in-out;
}
.file-upload.active .file-select {
  border-color: #337ab7;
  transition: all 0.2s ease-in-out;
  -moz-transition: all 0.2s ease-in-out;
  -webkit-transition: all 0.2s ease-in-out;
  -o-transition: all 0.2s ease-in-out;
}
.file-upload.active .file-select .file-select-button {
  background: #337ab7;
  color: #ffffff;
  transition: all 0.2s ease-in-out;
  -moz-transition: all 0.2s ease-in-out;
  -webkit-transition: all 0.2s ease-in-out;
  -o-transition: all 0.2s ease-in-out;
}
.file-upload .file-select input[type='file'] {
  z-index: 100;
  cursor: pointer;
  position: absolute;
  height: 100%;
  width: 100%;
  top: 0;
  left: 0;
  opacity: 0;
  filter: alpha(opacity=0);
}
.file-upload .file-select.file-select-disabled {
  opacity: 0.65;
}
.file-upload .file-select.file-select-disabled:hover {
  cursor: default;
  display: block;
  border: 1px solid #ddd;
  color: #337ab7;
  cursor: pointer;
  height: 40px;
  line-height: 40px;
  margin-top: 5px;
  text-align: left;
  background: #ffffff;
  overflow: hidden;
  position: relative;
}
.file-upload .file-select.file-select-disabled:hover .file-select-button {
  background: #ddd;
  color: #666666;
  padding: 0 8px;
  display: inline-block;
  height: 40px;
  line-height: 40px;
}
.file-upload .file-select.file-select-disabled:hover .file-select-name {
  line-height: 40px;
  display: inline-block;
  padding: 0 8px;
}
</style>
