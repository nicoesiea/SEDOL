# SEDOL
Valide a SEDOL code

function checkSedol(text){
	var weight = [1, 3, 1, 7, 3, 9, 1];
	try {
		var input = text.substr(0,6);
		var check_digit = sedol_check_digit(input);
		return text == input + check_digit;
	} catch(e) {
		return false;
	}       
	return false;
    
	function sedol_check_digit(char6) {
	    if (char6.search(/^[0-9BCDFGHJKLMNPQRSTVWXYZ]{6}$/) == -1){
	        throw "Invalid SEDOL number '" + char6 + "'";
	    }
	    var sum = 0;
	    for (var i = 0; i < char6.length; i++){
	        sum += weight[i] * parseInt(char6.charAt(i), 36);
	    }
	    var check = (10 - sum%10) % 10;
	    return check.toString();
	}
}
