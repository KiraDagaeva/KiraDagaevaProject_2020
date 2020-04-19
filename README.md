<html>
<head>
<meta charset="utf-8">
<link type="text/css" rel="stylesheet" href="stylesheet.css"/>
		<title>Convert GeoJSON</title>
		<script src="http://d3js.org/d3.v3.min.js"></script>
  		<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js"></script>

  		<script src="http://github.com/KiraDagaevaProject_2020/route.js"></script>
</head>
<body>
<left><h1>Транссибирская магистраль </h1></left>

Это железная дорога. Она проходит через всю Россию от Москвы до Владивостока. Протяжённость дороги: 9288 км. Весь путь занимает шесть дней и 10 минут. Эта дорога проходит через 19 разных регионов. Сегодня мы узнаем о ней подробнее.
<left><img alt="Это поезд на Транссибе" width="100%" src=https://capost.media/upload/iblock/b4c/b4cfc54f9a29aada1d36b11612ec2e30.jpg></left>

<h1>Convert <a href="http://geojson.org/geojson-spec.html#appendix-a-geometry-examples">GeoJSON-LineString</a> to <a href="http://en.wikipedia.org/wiki/Well-known_text">WKT-LINESTRING</a></h1>
	    		
		<div class='block'>
			<div>
				<h1>Input: GeoJSON</h1>
	    		<textarea id="geojson-input" placeholder="Paste GeoJSON here"></textarea>
	    		<p class = 'convert' id='convert'>Convert</p>	
			</div>
		</div>
		<div class='block'>
			<div>
				<h1>Output: GeoJSON</h1>
	    		<textarea id="geojson-output" placeholder="Resulting WKT will be displayed here"></textarea>
	    		<p class = 'convert' id='revert'>Convert</p>	
			</div>
	    </div>
	    
		
	</body>
<script>
	d3.select('#convert').on('mouseup',function(){convert();})
	d3.select('#revert').on('mouseup',function(){revert();})

  	//initialise input of textarea
  	d3.select('#geojson-input').text(JSON.stringify(LineString, null, 4));

  	
  	function convert(){
  		console.log('hey')
	  	//initialize json-textarea-input
	  	var input = $('#geojson-input').val();
	  	//get the input as json-object
	  	var input_json = JSON.parse(input);
		//console.log(input_json)

		//convert the json-input to WKT
  		var wkt_str = 'LINESTRING(';
  		input_json.coordinates.forEach(function(p,i){
  		//	console.log(p)
  			if(i<input_json.coordinates.length-1)wkt_str =  wkt_str + p[0] + ' ' + p[1] + ', ';
  			else wkt_str =  wkt_str + p[0] + ' ' + p[1] + ')';
  		})
  		//console.log(wkt_str)

  		//fill the resulting WKT-Linestring to output textarea
  		d3.select('#geojson-output').text(wkt_str);
  	}
  	function revert(){
  		console.log('hu')
  		//initialize wkt-textarea-input
	  	var input2 = $('#geojson-output').val();
	  	var input_cache = input2.replace('LINESTRING(','');
	  	input_cache = input_cache.replace(')','');
	  	var input_array = input_cache.split(',')

	  	var output_json = {"type":"LineString", "coordinates":[]}
	  	input_array.forEach(function (p,i){
	  		if(i==0)  var p_cache = p;
	  		else var p_cache = p.slice(1,p.length);
	  		var p_array = p_cache.split(' ');
	  		output_json.coordinates.push([Number(p_array[0]), Number(p_array[1])])
	  		
	  	})
	  	var json_str = JSON.stringify(output_json, null, 4) 
	  	d3.select('#geojson-input').text(json_str);
  	}

</script>

<h2>Контакты:</h2>
Страничка <a href=https://vk.com/green_leo/>vkontakte</a>
<br/>

Телефон: <b>+79685357749</b>
<br/>
E-mail: <i>kiradagaeva@yandex.ru</i>
</body>
</html>
