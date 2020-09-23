<div align="center">

## Perpetucal


</div>

### Description

A Javascript perpetual calendar optimized for printing. It handles holidays, birthdays, and events with timing like 'The fourth Thursday in November' (Thanksgiving) and 'The last Monday in May' (Memorial day).
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Kamilche](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/kamilche.md)
**Level**          |Beginner
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |
**Category**       |[Miscellaneous](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/miscellaneous__2-57.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/kamilche-perpetucal__2-3307/archive/master.zip)

### API Declarations

http://www.kamilche.com/html/perpetucal.html


### Source Code

```
<html>
<head>
<script language="JavaScript">
<!-- Hide
//-------------------------------------------------------------------------------------
// Global variables
//-------------------------------------------------------------------------------------
INACTIVECOLOR = "#b7b799"
TEXTCOLOR   = "#006400"
LIGHTCOLOR  = "#eaeadd"
DARKCOLOR   = "#cbcbaa"
now    = new Date();
year    = now.getYear();
month   = now.getMonth();
monthnames = new Array ("January", "February", "March", "April", "May", "June", "July",
			"August", "September", "October", "November", "December");
daynames  = new Array ("Sunday", "Monday", "Tuesday", "Wednesday",
			"Thursday", "Friday", "Saturday");
win    = null;
monthNum  = new Array (0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31);
t     = new Array (0, 3, 2, 5, 0, 3, 5, 1, 4, 6, 2, 4);
Jan = 0; Feb = 1; Mar = 2; Apr = 3; May = 4; Jun = 5;
Jul = 6; Aug = 7; Sep = 8; Oct = 9; Nov = 10; Dec = 11;
Sun = 0; Mon = 1; Tue = 2; Wed = 3; Thu = 4; Fri = 5; Sat = 6;
//-------------------------------------------------------------------------------------
// Set up birthday events, everyone will want to strip these out and make their own.
//-------------------------------------------------------------------------------------
Birthdays = new Array(12);
for (i = 0; i < 12; i++)
{
	Birthdays[i] = new Array(32);
	for (j = 0; j < 32; j++)
		Birthdays[i][j] = " ";
}
Birthdays[Jan][03] = "Someone's Birthday";
Birthdays[Jun][01] = "Someone Else's Birthday";
//-------------------------------------------------------------------------------------
// Set up 'January 1st' type events, such as New Year's Day
//-------------------------------------------------------------------------------------
Events = new Array(12);
for (i = 0; i < 12; i++)
{
	Events[i] = new Array(32);
	for (j = 0; j < 32; j++)
		Events[i][j] = " ";
}
Events[Jan][01] = "New Year's Day";
Events[Feb][02] = "Groundhog Day";
Events[Feb][14] = "Valentine's Day";
Events[Mar][17] = "St. Patrick's Day";
Events[Apr][01] = "April Fool's Day";
Events[Jul][04] = "Independence Day";
Events[Oct][31] = "Halloween";
Events[Nov][11] = "Veteran's Day";
Events[Dec][25] = "Christmas Day";
Events[Dec][31] = "New Year's Eve";
//-------------------------------------------------------------------------------------
// Set up '3rd Thursday in November' type events, such as Thanksgiving
//-------------------------------------------------------------------------------------
ThEvents = new Array(12);
for (i = 0; i < 12; i++)
{
	ThEvents[i] = new Array(7);
	for (j = 0; j < 7; j++)
	{
		ThEvents[i][j] = new Array(6);
		for (k = 0; k < 6; k++)
			ThEvents[i][j][k] = " ";
	}
}
ThEvents[Jan][Mon][3] = "Martin Luther King Day";
ThEvents[Feb][Mon][3] = "President's Day";
ThEvents[May][Sun][2] = "Mother's Day";
ThEvents[Jun][Sun][3] = "Father's Day";
ThEvents[Sep][Mon][1] = "Labor Day";
ThEvents[Oct][Mon][2] = "Columbus Day";
ThEvents[Nov][Thu][4] = "Thanksgiving Day";
//-------------------------------------------------------------------------------------
// Set up 'Last Monday in May' type events, such as Memorial Day.
//-------------------------------------------------------------------------------------
LastEvents = new Array(12);
for (i = 0; i < 12; i++)
{
	LastEvents[i] = new Array(7);
	for (j = 0; j < 7; j++)
	{
		LastEvents[i][j] = " ";
	}
}
LastEvents[May][Mon] = "Memorial Day";
//-------------------------------------------------------------------------------------
// Functions
//-------------------------------------------------------------------------------------
function IsLeapYear(year)
{
	return (year % 4 == 0 && year % 100 != 0 || year % 400 == 0);
}
function DaysInMonth(month, year)
{
	if (month == 2 && IsLeapYear(year))
		return (29);
	return (monthNum[month]);
}
function DayOfWeek(m, d, y)
{
	y -= m < 3;
	return Math.floor((y + y/4 - y/100 + y/400 + t[m-1] + d) % 7);
}
function pr(s)
{
	win.document.write(s + "\n");
}
function ClickLeft()
{
	month--;
	if (month < 0)
	{
		month = 11;
		year--;
	}
	win.close();
	MakeCalendar(year, month);
}
function ClickRight()
{
	month++;
	if (month > 11)
	{
		month = 0;
		year++;
	}
	win.close();
	MakeCalendar(year, month);
}
function MakeCalendar(year, month)
{
	win = window.open("", monthnames[month], "menubar=yes,scrollbars=yes,resizable=yes");
	win.blur();
	days   = DaysInMonth(month+1, year);
	firstday = DayOfWeek (month+1, 1, year);
	// Print the top of the page
	pr("<html>");
	pr("<title>Calendar for " + monthnames[month] + ", " + year + "</title>");
	pr("<body>");
	pr("<table border=1 cellspacing=0 bgcolor=" + LIGHTCOLOR + " width=100% height=700>");
	pr("<tr bgcolor=" + DARKCOLOR + ">");
	pr("\t<th colspan=2 align=right> <a href=\"javascript:window.opener.ClickLeft()\">&lt;&lt;</a></th>");
	pr("\t<th colspan=3 align=center><font size = \"+2\" color=" + TEXTCOLOR + "> " + monthnames[month] + " " + year + " </font></th>");
	pr("\t<th colspan=2 align=left> <a href=\"javascript:window.opener.ClickRight()\">&gt;&gt;</a></th>");
	pr("</tr>");
	pr("<tr bgcolor=" + DARKCOLOR + ">");
	for (col = 0; col < 7; col++)
		pr("\t<th width=14%><font color=" + TEXTCOLOR + ">" + daynames[col] + "</font></th>");
	pr("</tr>");
	day = 1;
	// Print the days
	day = 1;
	for (row = 1; row < 7; row++)
	{
		// Start a new row
		col = 0;
		pr("<tr height=16%>");
		// Start on the right day of the week
		if (firstday > 0 && row == 1)
		{
			pr("\t<td valign=top bgcolor=" + INACTIVECOLOR + " colspan=" + firstday + ">&nbsp;</td>");
			col += firstday;
		}
		// Print the day numbers
		for ( ; col < 7 && day <= days; col++, day++)
		{
			pr("\t<td valign=top><b>" + day + "</b><br>");
			pr("<font color=" + TEXTCOLOR + " size=\"-1\">");
			// Print holidays
			s = Events[month][day];
			if (s != " ")
				pr(s + "<br>");
			// Print '3rd tues' events
			s = ThEvents[month][col][Math.floor((day-1) / 7) + 1];
			if (s != " ")
				pr(s + "<br>");
			// Print 'last monday' events
			s = LastEvents[month][col];
			if (day > days - 7 && s != " ")
				pr(LastEvents[month][col] + "<br>");
			// Print birthdays
			s = Birthdays[month][day];
			if (s != " ")
				pr(s + "<br>");
			// Finish out the row
			pr("</font></td>");
		}
		// Fill with blank days
		if (col < 7)
			pr("\t<td valign=top bgcolor=" + INACTIVECOLOR + " colspan=" + (7 - col) + ">&nbsp;</td>");
		// Stop the row
		pr("</tr>");
	}
	// Print the bottom of the page
	pr("</table>");
	pr("</body>");
	pr("</html>");
	// Maximize the screen
	win.moveTo(0,0);
	win.resizeTo(screen.availWidth, screen.availHeight);
	win.focus();
}
function Startup()
{
	MakeCalendar(year, month);
}
function Shutdown()
{
	win.close();
}
-->
</script>
</head>
<title>Family Calendar</title></head>
<body onLoad="Startup()" onUnload="Shutdown()">
Hi! Use the &lt;&lt; and &gt;&gt; buttons to go to different months.<br>
Choose 'Print' from the 'File' menu to print the calendar for the current month.<br>
</body>
</html>
```

