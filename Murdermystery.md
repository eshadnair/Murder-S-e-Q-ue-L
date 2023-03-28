# *SQL Murder Mystery*

## Can you find out whodunnit?

**About:** This document contains SQL codes used to solve the murder
mystery puzzle published on
[[https://mystery.knightlab.com/]{.underline}](https://mystery.knightlab.com/).
The SQL Murder Mystery was created by Joon Park and Cathy He, who
designed it as a self-directed lesson to learn SQL concepts and
commands.

The assignment is done via a credited course in college under our
professor Mr. Abdul Majed Raja.

![](vertopal_91343e44f8da45bdbb0906381fd49d4e/media/image19.png){width="6.052083333333333in"
height="3.966580271216098in"}

Source: Knight lab

**By:** Esha Dinakaran Nair

eshadnair2001@gmail.com

**Information provided:** A crime has taken place, and the detective
needs your help. The detective gave you the crime scene report, but you
somehow lost it. You vaguely remember that the crime was a ​murder​ that
occurred sometime on ​Jan.15, 2018​, and that it took place in ​SQL City

**SOLUTION PROCESS**

**1)Use case -** Preliminary look at the data and understand what the
crime report mentions about the murder.

**Query -**

select \*

from crime_scene_report

where date = 20180115 AND type = \"murder\" AND city = \"SQL City\"

![](vertopal_91343e44f8da45bdbb0906381fd49d4e/media/image1.png){width="6.5in"
height="1.042195975503062in"}

**2)Use case -** To shortlist data based on the information given.

**Query -**

select \*

from person

where address_street_name = \"Northwestern Dr\" or name = \"Annabelle\"

***Result :***

![](vertopal_91343e44f8da45bdbb0906381fd49d4e/media/image7.png){width="5.510416666666667in"
height="2.9084273840769903in"}

**3)Use case -** To check all the events happening on 15th january 2018.

**Query -**

select \*

from facebook_event_checkin

where date = 20180115

***Result:***

![](vertopal_91343e44f8da45bdbb0906381fd49d4e/media/image13.png){width="5.385416666666667in"
height="2.898010717410324in"}

**4)Use case -** To understand if the murder was in the gym on the 15th
of Ja nuary 2018.

**Query -**

select \*

from get_fit_now_check_in

where check_in_date = 20180115

***Results -***

![](vertopal_91343e44f8da45bdbb0906381fd49d4e/media/image4.png){width="4.125in"
height="1.53125in"}

**5)Use case -** To join two tables via the license id to get a rough
idea of all the people and the compatibility between the tables.

**Query -**

select \*

from person P

Join drivers_license D

ON P.license_id = D.id

***Results:***

![](vertopal_91343e44f8da45bdbb0906381fd49d4e/media/image16.png){width="5.020833333333333in"
height="2.894714566929134in"}

**6)Use case -** To join two tables and get the name, address, and
license id of individuals living in suspected areas through the license
Id.

**Query -**

select name, address_street_name, license_id

from person P

Join drivers_license D

ON P.license_id = D.id

where address_street_name in(\"Northwestern Dr\", \"Franklin Ave\")

***Results:***

![](vertopal_91343e44f8da45bdbb0906381fd49d4e/media/image9.png){width="3.9895833333333335in"
height="2.9270833333333335in"}

**7)Use case -** To find the id of Annabelle Miller

**Query -**

select \*

from person

where name = \"Annabel Miller\"

***Results:***

![](vertopal_91343e44f8da45bdbb0906381fd49d4e/media/image3.png){width="6.052083333333333in"
height="0.71875in"}

**8)Use case -** Find the name of the event that Annabelle Miller went
to.

**Query-**

select \*

from facebook_event_checkin

where person_id = 16371

***Result:***

![](vertopal_91343e44f8da45bdbb0906381fd49d4e/media/image11.png){width="4.458333333333333in"
height="0.6463626421697288in"}

**9)Use case -** To find the id of the people who attended the given
event on 15th Jan 2018

**Query:**

select \*

from facebook_event_checkin

where event_id = 4719 AND date = 20180115

***Result***

![](vertopal_91343e44f8da45bdbb0906381fd49d4e/media/image8.png){width="3.8229166666666665in"
height="1.3854166666666667in"}

**10)Use case** - To find the name of the people with the following Id
who attended the event.

**Query:**

select \*

from person

Where id in(14887,16371,67318)

***Result:***

![](vertopal_91343e44f8da45bdbb0906381fd49d4e/media/image2.png){width="3.9895833333333335in"
height="1.375in"}

**11) Use case -** To find what statement did Jeremy bower give in his
interview

**Query:**

select \*

from interview

where person_id = 67318

***Result:***

![](vertopal_91343e44f8da45bdbb0906381fd49d4e/media/image12.png){width="6.34375in"
height="0.8541666666666666in"}

select \*

from facebook_event_checkin

where date LIKE \"201712%\"

**12) Use case-** To identify individuals that match the description
given by Jeremy in his statement.

**Query:**

select \*

from drivers_license

where hair_color = \"red\" AND car_make = \"Tesla\"

![](vertopal_91343e44f8da45bdbb0906381fd49d4e/media/image15.png){width="5.75in"
height="1.6354166666666667in"}

**13)** **Use case -** Joining tables to extract the details of people
with red hair and a Tesla.

**Query:**

select \*

from person P

join drivers_license D

ON P.license_id = D.id

where hair_color =\"red\" AND car_make = \"Tesla\"

![](vertopal_91343e44f8da45bdbb0906381fd49d4e/media/image18.png){width="5.333333333333333in"
height="2.0833333333333335in"}

**14) Use case** - Identify individuals who visited the SQL Symphony
concert in December 2017.

**Query:**

select \*

from facebook_event_checkin

where date LIKE \"201712%\" AND event_name = \"SQL Symphony Concert\"

![](vertopal_91343e44f8da45bdbb0906381fd49d4e/media/image6.png){width="5.3125in"
height="2.8229166666666665in"}

**15) Use case** - Joining tables and creating a new table called
"redhair_tesla" to find the name of the person who matches the
description given by Jeremy.

**Query:**

Create table redhair_tesla as

select name, address_street_name, license_id

from person P

Join drivers_license D

ON P.license_id = D.id

where hair_color = \"red\" AND car_make = \"Tesla\"

![](vertopal_91343e44f8da45bdbb0906381fd49d4e/media/image14.png){width="4.34375in"
height="1.46875in"}

**16) Use case-** Create a new table called redhair_tesla2 by merging
two more tables with more details and joining it with a new table.

**Query:**

select \*

from redhair_tesla2 R

join facebook_event_checkin F

ON R.id = F.person_id

![](vertopal_91343e44f8da45bdbb0906381fd49d4e/media/image17.png){width="5.197916666666667in"
height="2.8020833333333335in"}

**17) Use case -** To verify who attended the SQL Symphony concert
thrice.

Query:

select \*

from redhair_tesla2 R

join facebook_event_checkin F

ON R.id = F.person_id

where event_name = \"SQL Symphony Concert\"

![](vertopal_91343e44f8da45bdbb0906381fd49d4e/media/image5.png){width="4.822916666666667in"
height="2.0520833333333335in"}

***Hence, the murderer was Jeremy bowers, who was instructed to do so by
Miranda Priestly.***

![](vertopal_91343e44f8da45bdbb0906381fd49d4e/media/image10.png){width="2.494792213473316in"
height="2.494792213473316in"}

CAUGHT YOU!
