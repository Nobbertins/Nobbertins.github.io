
<html>
<head>
<title>Timestamp Remover</title>
</head>
<body>
<input type="file" id="inputfile" accept=".txt">
<script>
 function is_number(char) {
    return !isNaN(parseInt(char));
}
document.getElementById('inputfile')
            .addEventListener('change', function() {
            let f = this.value
            f = f.replace(/.*[\/\\]/, '').replace('.txt','');
            var fr=new FileReader();
            fr.onload=function(){
                let content = fr.result;
                let lines = content.split("\n");
                let finalText = ""
 for(let i = 0; i < lines.length; i++){
    if(lines[i].trim().length == 0){
        continue;
     }
    if(is_number(lines[i][0])){
        continue;
     }
    finalText += lines[i].trim();
    finalText += '\n';
  }
// Create element with <a> tag
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
            }
              
   fr.readAsText(this.files[0]);
        })
</script>
</body>
</html>
