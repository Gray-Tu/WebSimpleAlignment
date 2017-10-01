# WebSimpleAlignment
Run Alignment example  

v ATGTTAT  
w ATCGTAC  

-wATCGTAC  
v00000000  
A01111111  
T01222222  
G01223333  
T01223444  
T01223444  
A01223455  
T01223455  
  
-wATCGTAC  
v........  
A.↖←←←←←←  
T.↑↖←←←←←  
G.↑↑↑↖←←←  
T.↑↑↑↑↖←←  
T.↑↑↑↑↑↑↑  
A.↑↑↑↑↑↖←  
T.↑↑↑↑↑↑↑  
  
<!DOCTYPE html>
<html>
<body>

<p>Click the button to Run Alignment in JS.</p>

<button onclick="myFunction()">Try it</button>

<p id="demo"></p>

<script>

function myFunction() {
    var v = "v"+prompt("Please Enter v sequence", "ATGTTAT").trim();
    var w = "w"+prompt("Please enter w sequence", "ATCGTAC").trim();
    if (w != null) {
        document.getElementById("demo").innerHTML =
        alignment(v,w);
    }
}

function alignment(v,w){
	//make 0 matrix
	var lenV = v.length;
	var lenW = w.length;
	var matrixA = Array(), pathA = Array()
	var	w_j, v_i;
	for (v_i = 0; v_i <lenV; v_i++){
		matrixA[v_i] = [];
		pathA[v_i] = [];
		for (w_j = 0; w_j <lenW; w_j++){
			matrixA[v_i][w_j] = 0;
			pathA[v_i][w_j] = ".";
		}
	}
	//LCS
	for (v_i = 1; v_i < lenV; v_i++){
		for (w_j = 1; w_j < lenW; w_j++){
			if (v[v_i] == w[w_j]){
			
				matrixA[v_i][w_j] = Math.max(matrixA[v_i-1][w_j],
									matrixA[v_i][w_j-1],
									matrixA[v_i-1][w_j-1]+1);
			}
			else{
				matrixA[v_i][w_j] = Math.max(matrixA[v_i-1][w_j],
									matrixA[v_i][w_j-1]);
			}
		}
	}
	//Path
	for (v_i = 1; v_i < lenV; v_i++){
		for (w_j = 1; w_j < lenW; w_j++){
			switch (matrixA[v_i][w_j]){ 
				
                case matrixA[v_i-1][w_j]:
					pathA[v_i][w_j] = "↑";
					break;
                case matrixA[v_i][w_j-1]:
					pathA[v_i][w_j] = "←";
					break;
				case matrixA[v_i-1][w_j-1]+1:
					pathA[v_i][w_j] = "↖";
                    break;
            }       
            //if (v[v_i] == w[w_j] ){
			//		pathA[v_i][w_j] = "↖";
            //}
					
				
				
				
		}
	}
	
	//
	
	var Result ='<span style="font-family:Lucida Console;font-size: 48px;">-'+ w+"<br>";
		for (v_i = 0; v_i < lenV; v_i++){
			Result+=v[v_i];
            for(w_j = 0; w_j < lenW; w_j++){
				//Result+=pathA[v_i][w_j];
                Result += matrixA[v_i][w_j];
			}
			Result+= "<br>";
		}
    Result+="<br>";
    //path
   	Result+= "-"+w+"<br>";
    	for (v_i = 0; v_i < lenV; v_i++){
			Result+=v[v_i];
            for(w_j = 0; w_j < lenW; w_j++){
				Result+=pathA[v_i][w_j];
                //Result += matrixA[v_i][w_j];
			}
			Result+= "<br>";
		}
	Result+="</span>";
			
	return Result
}



</script>

</body>
</html>
