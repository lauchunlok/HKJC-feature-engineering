# HKJC-feature-engineering

### Tips for merge
#### Most of the feature engineering are performed in __form record__. Yet, there are 3 things needed to be merged from race_result and sectional time to form record
#### 1) Number of partcipating horses (for normalization)
#### 2) Prize money
#### 3) Section time

##### PS, Some races or even race day could be skipped when crawling. Not sure if because my computer do not have enough ram or whatever other reasons (e.g. the website is blocking).
##### Some steps I took might help ensure the completeness of the data.

### Analysis
#### The final goal is to make a database that contains all the apperance for houses that involved in races on 20150101 and onward
- As time-lag features is important for predicting horse performance in the future
- That means I will crawl all the historical record of houses that have appeared in the interested period (20150101 - Present)
- So form record will be larger and a race result complement will be crawled for form record normailzation

Updated 2022-04-10

Notes on Pla/Plc/finishing order:

form_record - Pla 
>- (['01', '02', '03', '04', '05', '06', '07', '08', '09', '10', '11', '12',
       '13', '14', 'WV', 'WV-A', 'WX', 'PU', 'UR', 'WX-A', 'FE', 'DNF', 'TNP',
       'DISQ', 'WXNR'])
>- No DH

race_result - Plc
>- ['1', '2', '3', '6', '4', '5', '7', '8', '9', '10', '11', '12', '13',
       '14', 'WV', 'WV A', '4 DH', 'PU', '5 DH', '3 DH', 'UR', '2 DH', 'WX',
       '1 DH', 'WX A', '7 DH', '6 DH', '8 DH', '9 DH', 'FE', 'DNF', '11 DH',
       'TNP', '10 DH', '12 DH', 'DISQ', 'WXNR']
 
>- sectional_time - finishing order also have DH

>- 1. Dropped VOID match and 2010/05/30 which aligned with form_record (which HKJC doesn't keep)
>- 2. Joint race_result
>- 3. Created prize_money table (point 2: because _key_ is used for merging instead of _date_ and _match_) after dropping VOID match and 2010/05/30 (since form_record doesn't have it neither)
>- 4. Processed DH and every invalid entry on race_result and also sectional_time (point 1: need drop any invalid horse entry) __BUT__ preserved __Plc_PM__ on race_result in case have to divide in portion (for later calculating PM_to_date in FE)

>>- __Since invalid entry is dropped here in race_result and sectional_time, prize_money is lost (since merge using key) (prize_money here is used for competitiveness proxy in FE)__
>>- And it is where the prize_money table become useful - filling up the gap for invalid entry
