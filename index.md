
<html>
<head>
<title>Timestamp Remover</title>
</head>
<body>
<input type="file" id="inputfile" accept=".txt">
<script>
 document.getElementById('inputfile').addEventListener('change', function() {
            var fr=new FileReader();
            fr.onload=function(){
                let lines = fr.result;
            }
            fr.readAsText(this.files[0]);
  });
  document.write(lines);
</script>
</body>
</html>
