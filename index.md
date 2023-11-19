
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
        <p>Drag files and/or directories to the box below!</p>

        <div id="dropzone">
          <div id="boxtitle">Drop Files Here</div>
        </div>
        
        <h2>Directory tree:</h2>
        
        <ul id="listing"></ul>
        
        <script>
          let dropzone = document.getElementById("dropzone");
let listing = document.getElementById("listing");

function scanFiles(item, container) {
  let elem = document.createElement("li");
  elem.textContent = item.name;
  container.appendChild(elem);
  if (item.isDirectory) {
    let directoryReader = item.createReader();
    let directoryContainer = document.createElement("ul");
    container.appendChild(directoryContainer);
    directoryReader.readEntries((entries) => {
    console.log(entries);
      entries.forEach((entry) => {
        scanFiles(entry, directoryContainer);
        console.log("recursed");
      });
    }, (error)=>{console.log(error);});
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
        scanFiles(item, listing);
      }
    }
  },
  false,
);

/*var docxConverter = require('docx-pdf');

docxConverter('./word_file.docx','./output.pdf',function(err,result){
  if(err){
    console.log(err);
  }
  console.log('result'+result);
});*/
        </script>
    </body>
</html>
