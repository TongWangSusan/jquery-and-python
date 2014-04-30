jquery-and-python
=================
//array in jquery push()
$(document).ready(function(){
      var total_putong = [];
			var total_youxiu = [];
			var total_jingying = [];
			var total_jiechu=[];
			var total_mingxing = [];
			var total_juxing= [];
			var total_chuanqi = [];
//put every data in the total lists
			async.eachSeries(loglist, function(item, cb) {
				$.getJSON(apihost_1 + '/recruitment/day/' + item + '/type/' + recruitment_type_id + '.json?jsoncallback=?', function(data) {
					temp++;
					putong = parseInt(data[0]);
					youxiu = parseInt(data[1]);
					jingying = parseInt(data[2]);
					jiechu = parseInt(data[3]);
					mingxing = parseInt(data[4]);
					juxing = parseInt(data[5]);
					chuanqi = parseInt(data[6]);
					total_putong.push(putong);
					total_youxiu.push(youxiu);
					total_jingying.push(jingying);
					total_jiechu.push(jiechu);
					total_mingxing.push(mingxing);
					total_juxing.push(juxing);
					total_chuanqi.push(chuanqi);
					cb();
    });
    //eval() function
				biao.append("<li class='biao_bottom'><ul><li>" + "求和" + "</li><li>" + eval(total_putong.join("+")) + "</li><li>" + eval(total_youxiu.join("+")) + "</li><li>" + eval(total_jingying.join("+")) + "</li><li>" + eval(total_jiechu.join("+")) + "</li><li>" + eval(total_mingxing.join("+")) + "</li><li>" + eval(total_juxing.join("+")) + "</li><li>" + eval(eval(total_chuanqi.join("+"))) + "</li></ul></li>");
    });
    //in python and jquery - display option drop-down menu with its detail drop-down menu
    
    
