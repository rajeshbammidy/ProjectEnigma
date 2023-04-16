
# Problem Statement

Professional home services offers multiple home services to the end users like hair cut, bathroom cleaning, kitchen cleaning, home painting,video call consultation,and many more.That being said it has so much data needs to store and process to deliver the customer request based on their needs. Every city possesses a category manager to manage the providers in that specific city-cat. So we are creating this database to simplify the things for the category managers of this huge business to track the things at any given instant.

We are storing the following information in our database:

**ProviderDetails**: Providers are the professional who delivers the service to the customers, this table contains the data like the providerId,providerName,providerPhoneNumber etc.
```
Functional Dependencies
Provider_id → provider_name
Provider_id → primary_category
Provider_id → gender
Provider_id → city
Provider_id → street_address
Provider_id → primary_hub_id
Provider_id → provider_phone_number


Provider_phone_number → provider_name
Provider_phone_number → primary_category
Provider_phone_number → gender
Provider_phone_number → city
Provider_phone_number → street_address
Provider_phone_number → primary_hub_id
Primary keys
provider_details_pkey(Provider_id)
Foreign keys


Unique Keys
provider_details_provider_phone_number_key(Provider_phone_number)
Indexes


Normalization Form
BCNF
```


**CustomerDetails**: Since this business is customer centric, we will save all the customer related information like customerName,customerAddress,hubId,phoneNumber etc..

```
Functional Dependencies
Customer_id → name
Customer_id → hub_id
Customer_id → gender
Customer_id → city
Customer_id → street_address
Customer_id → state
Customer_id → is_prime
Customer_id → phone_number

Phone_number → name
Phone_number → hub_id
Phone_number → gender
Phone_number → city
Phone_number → state
Phone_number → is_prime
Phone_number → street_address
Primary keys
customer_details_pkey(customer_id)
Foreign keys
customer_details_hub_id_fkey(hub_id)
Unique Keys


Indexes


Normalization Form
BCNF
```


**Hubs**: We divide a city into multiple small hubs to better make use of the service providers in the given region, this table holds the information about the city and its hubs.
```
Functional Dependencies
Hub_id → Demographic_id
Primary keys
hubs_pkey(hub_id)
Foreign keys
hubs_demographic_id_fkey(demographic_id)
Unique Keys


Indexes


Normalization Form
BCNF
```


**PastLeads**: This table contains all the past leads that a provider has delivered, it contains the information like the requestId,customerId,providerId(the provider who delivered the request)

```
Functional Dependencies
Request_id → Provider_id
Request_id → Customer_id
Request_id → Rating_id
Request_id → Status_id
Primary keys
past_leads_pkey(request_id)
Foreign keys
Past_leads_customer_id_fkey(customer_id)
Past_leads_provider_id_fkey(provider_id)
Past_leads_request_id_fkey(request_id)
Unique Keys


Indexes


Normalization Form
BCNF

```

**CityLevelFilters**: Every city has some set of filters to run for a given customer request, we can make use of these filters to process the requests in a given city, it has the information like the cityName and its filters.
```
Functional Dependencies
Filter_name,demographic_id → Filter_name
Filter_name,demographic_id → Demographic_id
Primary keys
city_level_filter_pkey(filter_name, demographic_id)
Foreign keys
city_level_filter_demographic_id_fkey(demographic_id)
Unique Keys


Indexes


Normalization Form
BCNF
```


**Packages**: This table holds all the information about the types of services (packages) that we offer and its respective prices.
```
Functional Dependencies
Package_id → Package_name
Package_id → Price
Primary keys
packages_pkey(package_id)
Foreign keys


Unique Keys
packages_package_name_key(package_name)
Indexes


Normalization Form
BCNF
```


**ProviderAttributes**: Every Provider has some attributes like how many jobs he can deliver during weekdays and during weekends etc.
```
Functional Dependencies
Provider_id → Max_jobs_weeks_days
Provider_id → Max_jobs_weeks_end
Primary keys
provider_attributes_pkey(provider_id)
Foreign keys
provider_attributes_provider_id_fkey(provider_id)
Unique Keys


Indexes


Normalization Form
BCNF

```

**ProviderEarnings**: It contains month wise earnings of the provider like, providerId,month,year,earnings.
```
Functional Dependencies
Provider_id, year, month → earnings
Primary keys
provider_earnings_pkey(provider_id, year, month)
Foreign keys
provider_earnings_provider_id_fkey(provider_id)
Unique Keys


Indexes


Normalization Form
BCNF
```

**Customer Request Details**:It contains all the upcoming and the past requests from the customers and their status (delivered/failed)
```
Functional Dependencies
Request_id → provider_id,customer_id,device,customer_address,city



Primary keys
customer_request_details_pkey(request_id)
Foreign keys
customer_request_details_customer_id_fkey(customer_id)
customer_request_details_provider_id_fkey(provider_id)
Unique Keys


Indexes


Normalization Form
BCNF
```


**Demographic Location**: It holds all the location related information, like city, state and its zip code extension and time zone.
```
Functional Dependencies
Demographic_id → city
Demographic_id → country
Demographic_id → state
Demographic_id → time zone
Primary keys
demographic_locations_pkey(demographic_id)
Foreign keys


Unique Keys


Indexes


Normalization Form
BCNF

```

**ProviderCalendar**: It holds the provider availability information for a given date.
```
Functional Dependencies
Provider_id, date → is_available
Primary keys
provider_calendar_pkey(provider_id, date)
Foreign keys
provider_calendar_provider_id_fkey(provider_id)
Unique Keys


Indexes


Normalization Form
BCNF
```

**PackagesDescription**: It holds more details  about the packages being offered.
```
Functional Dependencies
package_name → description
Primary keys
packages_description_pkey(package_name)
Foreign keys
packages_description_package_name_fkey(package_name)
Unique Keys


Indexes


Normalization Form
BCNF

```


### This database can help the category manager to answer the following questions:

1. How many providers are working in a given city cat
2. How many pending requests do they have in a given city-cat
3. The amount of revenue they are generating in a given city cat.
4. It will help them to manage the filters at city level, to decide if between aggressive filtering and filter relaxing
5. It will also help the Category Manager to play with the package prices.
6. Providers who earn more than average salary in that particular hub.
7. Customers who order serevices more frequently.
8. Skillsets of the providers
9. It can help to recruit the providers as needed in all the  fields which most of the customers are intrested.
10. It also helps to improve the services in those areas where there are lot of orders.

#### Get all the providerId's who belongs to the primary hub 7ece38010a7e156f2d0f0419ad7e685e
```
SELECT PROVIDER_ID FROM PROVIDER_DETAILS WHERE PRIMARY_HUB_ID='7ece38010a7e156f2d0f0419ad7e685e'
```

#### Get the count of the providers who are having "Mens_Grooming" as Primary category
```
SELECT COUNT(PROVIDER_ID) FROM PROVIDER_DETAILS WHERE PRIMARY_CATEGORY='Mens_Grooming';
```

#### Get all the customerId's who took service more than once in our platform
```
SELECT CUSTOMER_ID,COUNT(*) AS OrderFrequency FROM CUSTOMER_REQUEST_DETAILS GROUP BY CUSTOMER_ID HAVING COUNT(*)>1;
```

#### Get the city name and the prime customers count for all the cities having count greater than 1
```
SELECT COUNT(*),CITY FROM CUSTOMER_DETAILS  WHERE IS_PRIME='true' GROUP BY CITY HAVING COUNT(*)>1; 
```

#### Get all the providerIds who are are willing to do more than a dozen jobs per week
```
SELECT PROVIDER_ID,(max_jobs_week_days+max_jobs_week_ends) AS "Job Count" FROM PROVIDER_ATTRIBUTES  WHERE (max_jobs_week_days+max_jobs_week_ends)>12

```


#### Given the city of the customer and filters applied on the city, apply the filters only if the number of tagged providers in that city is less than 10.Discard all the providers if all filters given by the DBA imposed on the city.Eg: City:Denton filterAppliedOnCity ="AllSkillMatch", "PastPerfomacePercentage", "IsReebookingCustomer", "CustomerRatings"
```
create or replace function isRequestServiceble(cityName varchar(50),filterNames text[])
returns boolean
language plpgsql
as
$$
declare
   providersCount integer;
   elegibleDemographicIds integer;
begin
   SELECT COUNT(PH.provider_id) INTO providersCount  FROM provider_hubs PH INNER JOIN HUBS HBS ON PH.hub_id=HBS.hub_id INNER JOIN demographic_locations DL ON HBS.demographic_id=DL.demographic_id WHERE CITY=cityName;
    SELECT count(A.demographic_id) into elegibleDemographicIds FROM (SELECT DISTINCT(demographic_id) FROM CITY_LEVEL_FILTER WHERE demographic_id IN (SELECT demographic_id FROM demographic_locations WHERE CITY='Denton')) A WHERE  EXISTS(
SELECT * FROM CITY_LEVEL_FILTER WHERE demographic_id= A.demographic_id AND FILTER_NAME NOT IN ('AllSkillMatch', 'PastPerfomacePercentage', 'IsReebookingCustomer', 'CustomerRatings')
);
   return providersCount<10 and elegibleDemographicIds>0 ;
end;
$$;

SELECT isRequestServiceble('Denton',ARRAY['AllSkillMatch', 'PastPerfomacePercentage', 'IsReebookingCustomer', 'CustomerRatings'])


CREATE OR REPLACE FUNCTION provider_details_insert() RETURNS trigger
   LANGUAGE plpgsql AS
   $$
   declare
   phub_id VARCHAR(50);
BEGIN 
select hub_id into phub_id from hubs where demographic_id in (select T.demographic_id from demographic_locations T  where city=NEW.city) limit 1;
   NEW.primary_hub_id := phub_id;
  RAISE NOTICE 'allotted primary hub id is %', NEW.primary_hub_id;
   RETURN NEW; 
END;
$$;

CREATE OR REPLACE TRIGGER provider_primary_hub_before_insert 
   BEFORE INSERT ON provider_details FOR EACH ROW 
   EXECUTE PROCEDURE provider_details_insert();


```

### Target Users & Real Life Scenario:
This database can be used by the authorized product managers and the category managers to identify the best performing providers in a category, and most profitable and selling categories in a city, we can also keep track of customer satisfying by querying the ratings and these results can be used to train the ML models to come up with a efficient filters to discard the bad providers from the organization.



# ER Diagrams
The following is the ERD among the various entities, we have taken into consideration:

![App Screenshot](https://github.com/rajeshbammidy/ProjectEnigma/blob/main/images/er1.png)
![App Screenshot](https://github.com/rajeshbammidy/ProjectEnigma/blob/main/images/er2.png)
