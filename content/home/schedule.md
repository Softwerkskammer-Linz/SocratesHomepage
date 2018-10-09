+++
weight = 2
title = "Schedule"
linkTitle = "Schedule"
url = "schedule"

groups = ["home"]
noreadmore = true
+++

<div id="schedule"></div>


<script>
var xmlhttp;
var htmlData = "";

xmlhttp = new XMLHttpRequest();
xmlhttp.onreadystatechange = function() {
	if (this.readyState == 4 && this.status == 200) {

		schedule = JSON.parse(this.responseText);
		for (dayIndex in schedule) {
			htmlData += '<h4>' + schedule[dayIndex].name + '</h4>';
			htmlData += '<p>' + schedule[dayIndex].time + '</p>';
			
			htmlData += '<div class="schedule">'
			
			for (dataIndex in schedule[dayIndex].data) {
				if (dataIndex != schedule[dayIndex].data.length-1) {
					htmlData += '<div class="row bl br bt">'
				} else {
					// last
					htmlData += '<div class="row bl br bt bb">'
				}
				htmlData += '<div class="one column">' + schedule[dayIndex].data[dataIndex].time + '</div>'
				
				var extraIndex = schedule[dayIndex].data[dataIndex].extra
				
				var columnClass = 'eleven'
				if (extraIndex != undefined) {
					var columnClass = 'eight'
				}
				
				htmlData += '<div class="' + columnClass + ' columns bl-not-mobile">'
				for (sessionIndex in schedule[dayIndex].data[dataIndex].sessions) {
					htmlData += '<div>'
					htmlData += schedule[dayIndex].data[dataIndex].sessions[sessionIndex].name
					htmlData += ' / <span class="room">'
					htmlData += schedule[dayIndex].data[dataIndex].sessions[sessionIndex].room
					htmlData += '</span>'
					htmlData += '</div>'
				}
				htmlData += '</div>'

				if (extraIndex != undefined) {
					htmlData += '<div class="three columns bl-not-mobile center">'
					for (extraIndex in schedule[dayIndex].data[dataIndex].extra) {
						htmlData += schedule[dayIndex].data[dataIndex].extra[extraIndex].name
						htmlData += ' / <span class="room">'
						htmlData += schedule[dayIndex].data[dataIndex].extra[extraIndex].room
						htmlData += '</span>'
					}
					htmlData += '</div>'
				}
				
				htmlData += '</div>'
			}
			htmlData += '</div><br/><br/>'
		}
		document.getElementById("schedule").innerHTML = htmlData;
	}
};
xmlhttp.open("POST", "/data/schedule.json", true);
xmlhttp.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
xmlhttp.send();

</script>

<!--more-->