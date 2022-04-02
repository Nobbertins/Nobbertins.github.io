
<html>
<head>
<title>Random Names</title>
</head>
<body>
<script>
  function shuffleArray(array) {
    for (var i = array.length - 1; i > 0; i--) {
        var j = Math.floor(Math.random() * (i + 1));
        var temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }
    return array;
}
var arr = []
while(true){
var x = prompt('name')
if(x == 'done'){
  arr = shuffleArray(arr)
  string = ''
    for(i=0;i<=arr.length-2;i++){
      string+=arr[i]+' ---> '+arr[i+1]+'<br />'
    }
    string+=arr[arr.length-1]+' ---> '+arr[0]
    document.write(string)
    break
}
arr.push(x)
}
</script>
</body>
</html>
