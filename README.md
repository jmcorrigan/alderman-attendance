# alderman-attendance
The data work for the South Side Weekly's alderman attendance story



Documentation
1. Run committee_filter.py

2. In committee_participation.csv:
	- remove vacancies
	- remove office of mayor/city clerk
	- remove council office of financial oversight
	- remove Thomas Allen, Toni Preckwinckle, Ed Smith (their terms ending before data collection began)
	- correct "Col/xf3n, Rey" to "Colon, Rey"
	- save as committee_terms_clean.csv

3. Run attendance_filter.py

4. In who_there.csv:
	- sort by committee, then date
	- remove dates before 1/27/2011, after 1/25/2017
	- correct "Col/xf3n, Rey" to "Colon, Rey"
	- sort meetings w/ attendance and meetings w/o attendance 
		=IF(C1="",IF(B1<>B2,0,IF(A1<>A2,0,1)),"")
		[1 if no attendance record, 0 if attendance record]
	- strip time value from column b { =left(B1, 10) }, replace ' - ' with ' / '
	- remove meeting placemarker entries (no alderman or status fields)
	- Cut placemarker entries, paste in separate file (all_meetings.csv)

5. Run check_attendance.py

6. In attendance.csv:
	- sort by column d, then b
	- remove Joint Committee/Committee on Energy, Environmental Protection and Public Utilities entries
	- add period column 
	(1 = Jan. 2011 - June 2011; 2 = July 2011 - Dec. 2011; 3 = Jan. 2012 - June 2012... 12 = July 2016 - Jan. 2017)
	- Remove entries for non-member committee entries and pre/post-term meeting entries
		listed in (removed_entries.csv)
	- Add missing entries 
		listed in (added_entries.csv)
	- Name columns {committee, date, alderman, status, period}
	- count total absences for each meeting
		{ =IF(AND(D2=0,D1=0),G1+1,IF(AND(D2=0,D1=1),1,IF(AND(D2=1,B2<>B1),0,""))) }
		{ =IF(AND(G2<>"",G3=""),G2,"") }
	- Copy absences with total figures to separate file { absences_by_meeting.csv }
	- Save attendance.csv as attendance-final.csv

7. Open all_meetings.csv
	- In column C, replace ‘1’ with ’not recorded’ and ‘0’ with ‘recorded’
	- Remove dupes




