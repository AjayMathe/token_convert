# token_convert

<!DOCTYPE html>
<html>
<head>
<!-- Developed by Ajay Mathe.-->
<!-- What this tool does ?
This tool converts Database names in soft tokens to hard tokens
example $nlstemp --- NLS_TEMP_TABLES
How to use ?
Paste the SQL in 1st text area, Click convert. and then click Copy. As simple as that!
-->
<title>DB Token Convert</title>
<link rel="icon" type="image/x-icon" href="favicon.ico">
<script>
function ClearFields() {
     document.getElementById("source").value = "";
     document.getElementById("target").value = "";
}

function copySelectionText(){
	var copysuccess // var to check whether execCommand successfully executed
	try{
		copysuccess = document.execCommand("copy") // run command to copy selected text to clipboard
	} catch(e){
		copysuccess = false
	}
	return copysuccess
}

function copyfieldvalue(e, id){
	var field = document.getElementById(id)
	field.focus()
	field.setSelectionRange(0, field.value.length)
	var copysuccess = copySelectionText()
	if (copysuccess){
		alert("copied!")
	}
}

function ConvertSoftToken() {
var str = document.getElementById("source").value;
var tar = document.getElementById("target");
//str = str.replace(/\$/g, '&');

// Add the New database name in case if it doesnt exist here.
var mapObj = {
'&sample':"sampledb",
'&hello':"sampledb",
};
var re = new RegExp(Object.keys(mapObj).join("|"),"gi");
str = str.replace(new RegExp(re,"g"), function(matched){
  return mapObj[matched];
});
tar.value = str;

}

</script>
<style> 
body
{
margin:0px;
padding:0px;
width:100%;
}
header, footer {
    padding: 5px;
    background-color: #154251;
    clear: left;
	color: white;
    text-align: center;
}
h1{
font-family: Garamond;
}
textarea {
    width: 100%;
    height: 230px;
    padding: 12px 20px;
    box-sizing: border-box;
    border: 2px solid #ccc;
    border-radius: 4px;
    background-color: #e6e6e6;
    font-size: 16px;
    resize: none;
}
textarea:hover {
    background-color: #f8f8f8;
}
input[type=button], input[type=submit], input[type=reset] {
    background-color: #4CAF50;
    border: none;
    color: white;
	border-radius: 12px;
    padding: 16px 32px;
    text-decoration: none;
    margin: 4px 2px;
    cursor: pointer;
}
.button {
  border-radius: 4px;
  background-color: #4CAF50;
  border: none;
  color: #FFFFFF;
  text-align: center;
  font-size: 20px;
  padding: 15px;
  width: 200px;
  transition: all 0.5s;
  cursor: pointer;
  margin: 5px;
}

.button span {
  cursor: pointer;
  display: inline-block;
  position: relative;
  transition: 0.5s;
}

.button span:after {
  content: '\00bb';
  position: absolute;
  opacity: 0;
  top: 0;
  right: -20px;
  transition: 0.5s;
}

.button:hover span {
  padding-right: 25px;
}

.button:hover span:after {
  opacity: 1;
  right: 0;
}

.button:active{
background-color : green;
}

</style>
</head>
<body>

<header>
   <h1>DB Names Token Convert</h1>
</header>
<button class="button" style="background-color: #47476b; float: right; padding : 10px" onclick="ClearFields();"><span>Clear</span></button>
<form>
  <textarea id="source"></textarea>
</form>

<button class="button" style="background-color: #e65c00;" onClick="ConvertSoftToken();return false"><span>Convert </span></button>
<button class="button" onClick="copyfieldvalue(event, 'target');return false" id="cpy"><span>Copy </span></button>

<form>
  <textarea id="target"></textarea>
</form>
<footer>Copyright &copy; Aj</footer>
<!-- Developed by Ajay Mathe. -->
</body>
</html>
