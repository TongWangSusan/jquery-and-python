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
    //in python the json-like array and 
    types_details = [
    {
        'name': '普招',
        'sub': [
            {'name': '普通招募', 'id': 6},
            {'name': '时段招募', 'id': 8},
            {'name': '快速普通招募', 'id': 41},
        ]
    },
    {
        'name': '高招',
        'sub': [
            {'name': '高级招募', 'id': 7},
            {'name': '快速高级招募', 'id': 42},
            {'name': 'vip-免费招募', 'id': 255},
            {'name': 'vip-半价招募', 'id': 256},
        ]
    },
    {
        'name': '超票',
        'sub': [
            {'name': '球票招募', 'id': 3401},
        ]
    },
    {
        'name': '金票',
        'sub': [
            {'name': '球票招募', 'id': 3402},
        ]
    }
]
//convert it to json data
import web
import json


def to_json(obj):
    if not web.cookies().get('user'):
        return json.dumps({'status': False, 'message': 'you should login...'})
    try:
        return "%s(%s)" % (web.input().jsoncallback, json.dumps(obj, sort_keys=True))
    except AttributeError:
        return json.dumps(obj)

class TypesDetails(object):
    def GET(self):
        return app.to_json(types_details)
//jquery - display option drop-down menu with its detail drop-down menu
var er = function(er1, er2, link, func) {

	var erji1 = $(er1);
	erji1.append('<option value="fuck">请选择</option>');
	var erji2 = $(er2);
	erji2.hide();
	var json_data;
	var recruitment_types_details = $.getJSON(link);
	recruitment_types_details.done(function(data) {
		json_data = data;
		$.each(data, function(index, item) {
			erji1.append('<option value ="' + index + '">' + item.name + '</option>');
		});
	});

	erji1.on('change', function() {
		erji2.html('<option value="fuck">请选择</option>');

		if (erji1.val() != 'fuck') {
			//var all= '<option value="all">全部</option>';
			var all_id = [];

			$.each(json_data[erji1.val()].sub, function(index, item) {
				erji2.append('<option value="' + item.id + '">' + item.name + '</option>');
				all_id.push(item.id);
			});
			erji2.append('<option value="' + all_id + '">全部</option>');
			erji2.fadeIn(300);
		} else {
			erji2.fadeOut(300);
		}
	});

	erji2.on('change', function() {
		func(erji2.val());
	});
};
//call the function
er('#erji1', '#erji2', apihost_1 + '/recruitment/types/details.json?jsoncallback=?', function(id) {
		recruitment_type_id = id;
	});
