
<html>
    <head>
        <title>Word to Pdf</title>
        <style>
#dropzone {
  text-align: center;
  width: 300px;
  height: 100px;
  margin: 10px;
  padding: 10px;
  border: 4px dashed red;
  border-radius: 10px;
}

#boxtitle {
  display: table-cell;
  vertical-align: middle;
  text-align: center;
  color: black;
  font:
    bold 2em "Arial",
    sans-serif;
  width: 300px;
  height: 100px;
}

body {
  font:
    14px "Arial",
    sans-serif;
}
        </style>
    </head>
    <body>
        <p>Drag folder to the box below!</p>

        <div id="dropzone">
          <div id="boxtitle">Drop Files Here</div>
        </div>    
        <script>
          let dropzone = document.getElementById("dropzone");
let listing = document.getElementById("listing");
let fileNames = []
function scanFiles(item) {
  if (item.isDirectory) {
    let directoryReader = item.createReader();
    directoryReader.readEntries((entries) => {
      entries.forEach((entry) => {
        scanFiles(entry);
      });
    }, (error)=>{console.log(error);});
  }
  else{
    fileNames.append(item.name);
  }
}
dropzone.addEventListener(
  "dragover",
  (event) => {
    event.preventDefault();
  },
  false,
);
dropzone.addEventListener(
  "drop",
  (event) => {
    let items = event.dataTransfer.items;

    event.preventDefault();
    listing.textContent = "";

    for (let i = 0; i < items.length; i++) {
      let item = items[i].webkitGetAsEntry();

      if (item) {
        scanFiles(item);
      }
    }
  },
  false,
);
var docxConverter = require('docx-pdf');
/*docxConverter('./word_file.docx','./output.pdf',function(err,result){
  if(err){
    console.log(err);
  }
  console.log('result'+result);
});*/
        </script>
    </body>
</html>
