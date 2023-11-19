
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
let fileArray = []
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
    fileArray.push(item);
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

    for (let i = 0; i < items.length; i++) {
      let item = items[i].webkitGetAsEntry();

      if (item) {
        scanFiles(item);
        console.log(fileArray[0].text());
/*
const link = document.createElement("a");

// Create a blog object with the file content which you want to add to the file
const file = new Blob([finalText], { type: 'text/plain' });

// Add file content in the object URL
link.href = URL.createObjectURL(file);

// Add file name
link.download = f+"_edited.txt";

// Add click event to <a> tag to save file.
link.click();
URL.revokeObjectURL(link.href);
*/
      }
    }
  },
  false,
);
        </script>
    </body>
</html>
