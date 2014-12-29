googlecalendar_v3_chrome_extenstion
===================================

Incomplete Google Calendar v3 API for Chrome extensions.

I wasn't able to get Google's Javascript api's to work with Chrome extensions. So I pulled together some code to authenticate to Google and reimplemented the parts of the Calendar v3 API that I needed. 

It authenticates for the person (current user) who is logged into the browser.

Examples
=========
    var calendarlist = new gcal.CalendarList(),
        calendar     = new gcal.Calendars(),
        events       = new gcal.Events();
    
    //Calendar and CalendarList
    function testCalendar(){
        calendarlist.list().then(function(aCalendarListEntry){
            console.log(aCalendarListEntry);
        }).done();

        calendarlist.execute();
        calendar.get('18s4kn3fhvriai8jujb1ss2m7k@group.calendar.google.com').then(function(c){
            console.log(c);
        }).done();

        calendar.insert( new gcal.Calendar({ summary:'Test 6', description:'Does it work?' }) ).then(function(cal){
            console.log(cal);
        }).done();

        calendar.delete('ipn1dro22mgg7ojjfm1g9uirb4@group.calendar.google.com').then(function(cal){
            console.log(cal);
        }).done();

        calendar.execute();

        calendarlist.list().then(function(aCalendarListEntry){
            console.log(aCalendarListEntry);
        }).done();

        calendarlist.get('18s4kn3fhvriai8jujb1ss2m7k@group.calendar.google.com').then(function(oCalenderListEntry){
            console.log(oCalenderListEntry);
        }).done();

        calendarlist.insert({
            id:'18s4kn3fhvriai8jujb1ss2m7k@group.calendar.google.com',
            defaultReminders:[
                {
                    method:'email',
                    minutes:10
                }
            ],
            notificationSettings:{
                notifications:[
                    {
                        method:'email',
                        type:'eventCreation'
                    }
                ]
            }
        }).then(
            function( obj ){
            },
            function( error ){
                debugger;
                console.error(error);
            }
        ).done();

        calendarlist.delete('0vf8d7bhs203c0rk92as26v2qk@group.calendar.google.com').then(
            function(oCalenderListEntry){
                console.log('Delete: ');
                debugger;
            },
            function(obj){
                debugger;
            }
        ).done();

        calendarlist.insert({
            id:'bgi5k124bf64bohkavm62qmu8o@group.calendar.google.com',
            defaultReminders:[
                {
                    method:'email',
                    minutes:10
                }
            ],
            notificationSettings:{
                notifications:[
                    {
                        method:'email',
                        type:'eventCreation'
                    }
                ]
            }
        }).then(
            function( obj ){
            },
            function( error ){
                debugger;
                console.error(error);
            }
        ).done();

        calendarlist.get('bgi5k124bf64bohkavm62qmu8o@group.calendar.google.com').then(function(oCalenderListEntry){
            console.log(oCalenderListEntry);
        }).done();
    };

    //Events
    function testEvents(){
        //listid: 18s4kn3fhvriai8jujb1ss2m7k@group.calendar.google.com
        //eventid:5466160332369527 
        events.list('18s4kn3fhvriai8jujb1ss2m7k@group.calendar.google.com').then(
            function(evnts){
                console.log(evnts);
            },
            function( reason ){
                console.log(reason);
            }
        ).done();
        events.get('18s4kn3fhvriai8jujb1ss2m7k@group.calendar.google.com', 'ljjnf3faadocv1idboue0mii00').then(
            function(evnts){
                console.log(evnts);
            },
            function( reason ){
                console.log(reason);
            }
        ).done();

        events.insert( '18s4kn3fhvriai8jujb1ss2m7k@group.calendar.google.com', {
            description:"test " + Math.random(),
            summary:"test summary " + Math.random(),
            start: new gcal.Event.Date({
                dateTime: Date.today().setTimeToNow().set({hour:7,minute:10}).toISOString()
            }),
            end: new gcal.Event.Date({
                dateTime: Date.today().setTimeToNow().addHours(1).toISOString()
            })
        }).then(
            function(evnts){
                console.log(evnts);
            },
            function( reason ){
                console.log(reason);
            }
        ).done();

        events.execute();
    };
    testEvents();
