<div align="center">

## Calculate day in a week by given a date


</div>

### Description

This program can calculate the day of the week from a date key in by user.
 
### More Info
 
a date

day of week


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Stanley Wong](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/stanley-wong.md)
**Level**          |Beginner
**User Rating**    |5.0 (20 globes from 4 users)
**Compatibility**  |C, C\+\+ \(general\), Microsoft Visual C\+\+
**Category**       |[Validation/ Processing](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/validation-processing__3-16.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/stanley-wong-calculate-day-in-a-week-by-given-a-date__3-2857/archive/master.zip)

### API Declarations

```
stdio.h
string.h
```


### Source Code

```
#include <stdio.h>
#include <string.h>
/* Prototype Declaration */
int validateDate(int dd, int mm, int yyyy);
void printError();
int calcDay_Dec31(int yyyy);
int dayInYear(int dd, int mm);
void nameInStr (char daysInWord[], int days);
void main(void)
{
	int dd, mm, yyyy;
	int days;
	char daysInWord[11];
	/* Read a date and validate the date */
	do{
		printf("Enter a date(dd/mm/yyyy) :");
		scanf("%d / %d / %d", &dd, &mm ,&yyyy);
		fflush(stdin);
	}
	while(validateDate(dd, mm, yyyy));
	/* Calculate the day for Dec 31 of the previous year */
	days = calcDay_Dec31(yyyy);
	/* Calculate the day for the given date */
	days = (dayInYear(dd, mm) + days) % 7;
	/* Add one day if the year is leap year and desired date is after February */
	if ((!(yyyy % 4) && (yyyy % 100) || !(yyyy % 400)) && mm > 2)
		days++;
	nameInStr(daysInWord, days);
	/* Print the day of the desired date */
	printf("The day for date %d/%d/%d is %s\n\n", dd, mm, yyyy, daysInWord);
} /* main */
int validateDate(int dd, int mm, int yyyy)
{
	int i = 0, j = 0;
	int a[7] = {1, 3, 5, 7, 8, 10, 12};
	int b[4] = {4, 6, 9, 11};
	int error = 0;
	if (mm < 1 || mm > 12)
		error = 1;
	if (mm == 2)
	{
		if (!(yyyy % 4) && (yyyy % 100) || !(yyyy % 400))
		{
			if (dd < 1 || dd > 29)
				error = 1;
		}
		else if (dd < 1 || dd >28)
			error = 1;
	}
	for (i=0;i<6;i+=1)
	{
		if (mm == a[i])
		{
			if (dd < 1 || dd > 31)
				error = 1;
		}
	}
	for (j=0;j<4;j+=1)
	{
		if (mm == b[j])
		{
			if (dd < 1 || dd > 30)
				error = 1;
		}
	}
	if (error == 1)
		printError();
	return error;
}
void printError()
{
	printf("Invalid Input!\n\n");
}
int calcDay_Dec31(int yyyy)
{
	int dayCode = 0;
	dayCode = ((yyyy-1)*365 + (yyyy-1)/4 - (yyyy-1)/100 + (yyyy-1)/400) % 7;
	return dayCode;
} /* calcDay_Dec31 */
int dayInYear(int dd, int mm)
{
	switch(mm)
	{
	case 12:dd += 30;
	case 11:dd += 31;
	case 10:dd += 30;
	case 9:dd += 31;
	case 8:dd += 31;
	case 7:dd += 30;
	case 6:dd += 31;
	case 5:dd += 30;
	case 4:dd += 31;
	case 3:dd += 28;
	case 2:dd += 31;
	}
	return dd;
} /* dayInYear */
void nameInStr(char daysInWord[], int days)
{
	switch(days)
	{
	case 0:strcpy(daysInWord, "Sunday");break;
	case 1:strcpy(daysInWord, "Monday");break;
	case 2:strcpy(daysInWord, "Tuesday");break;
	case 3:strcpy(daysInWord, "Wednesday");break;
	case 4:strcpy(daysInWord, "Thursday");break;
	case 5:strcpy(daysInWord, "Friday");break;
	case 6:strcpy(daysInWord, "Saturday");break;
	}
} /* nameInStr */
```

