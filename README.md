
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

### Target Users & Real Life Scenario:
This database can be used by the authorized product managers and the category managers to identify the best performing providers in a category, and most profitable and selling categories in a city, we can also keep track of customer satisfying by querying the ratings and these results can be used to train the ML models to come up with a efficient filters to discard the bad providers from the organization.


# ER Diagrams
The following is the ERD among the various entities, we have taken into consideration:

![App Screenshot](https://github.com/rajeshbammidy/ProjectEnigma/blob/main/images/er1.png)
![App Screenshot](https://github.com/rajeshbammidy/ProjectEnigma/blob/main/images/er2.png)
