# Line-Notify--Google-Calendar
สร้าง Line Notify แจ้งเตือน Google Calendar

> อ้างอิงจากเว็บไซต์ https://adamblog.co/line-notify-google-calendar/

```javascript
function dailyEventMessage() {
    var googleCalendarId = "Calendar Id";

    var calendar = CalendarApp.getCalendarById(googleCalendarId);
    var today = new Date();
    // var dailyEventList = calendar.getEventsForDay(today);
    var toMorrow = new Date(today.getFullYear(), today.getMonth(), today.getDate()+1);
    var toMorrowEventList = calendar.getEventsForDay(toMorrow)

    //Logger.log(dailyEventList);

    var message = "";

    for (var i = 0; i < toMorrowEventList.length; i++) {

        var eventTitle = "Title: " + "\n" + toMorrowEventList[i].getTitle();
        var eventTime = "Start Time: " + "\n" + toMorrowEventList[i].getStartTime().toTimeString().slice(0, 8);
        var eventDescribtion = "Description: " + "\n" + toMorrowEventList[i].getDescription();

        message += "\n" + eventTitle + "\n" + eventTime + "\n" + eventDescribtion;

    }

    if (message === "") {
        return;
    }

    Logger.log(message);
    sendMessage(message);

}


function sendMessage(message) {
    var lineNotifyEndPoint = "https://notify-api.line.me/api/notify";
    var accessToken = "Your line notify access token";

    var formData = {
        "message": message
    };

    var options = {
        "headers": {
            "Authorization": "Bearer " + accessToken
        },
        "method": 'post',
        "payload": formData
    };

    try {
        var response = UrlFetchApp.fetch(lineNotifyEndPoint, options);
    } catch (error) {
        Logger.log(error.name + "：" + error.message);
        return;
    }

    if (response.getResponseCode() !== 200) {
        Logger.log("Sending message failed.");
    }
}
```

<sub><sup>Note getpocket reading: https://app.getpocket.com/read/2911616899</sub></sup>

<br>
<br>

---
<p align="center"> จัดทำโปรแกรมคอมพิวเตอร์พัฒนาระบบงานธุรกิจส่วนตัวและหน่วยงาน ใส่ใจคุณภาพ คุ้มราคา ส่งงานตรงเวลา<br>ติดต่อ 086-288-7987 (ท็อป) หรืออีเมล์    nakomah.web@gmail.com<br>ติดตามผลงานได้ที่ <a href="https://nakomah.com" target="_blank">www.nakomah.com</a></p>
