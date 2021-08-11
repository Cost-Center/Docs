# Documentation

## Our Goal

Cost Center's goal is to collect raw data from your Ad Networks, Attribution Services, Analytics Services, Monetization Services and combine them into one report. In this report, Cost Center will provide powerfull metrics that can give you valuable information for decision making, such as:
* LTV Day x: Lifetime value at a day LTV D1, LTV D3, LTV D7, LTV D14, LTV 30, LTV 60
* ROAS Day x: Return on ad spend at a day ROAS D1, ROAS D3, ROAS D7, ROAS D14, ROAS D30, ROAS D60
* RR Day x: Retention at a day RR D1, RR D3, RR D7, RR D14, RR D30, RR D60
* Duration

All the powerfull metrics above can be broken down at Country, Campaign, Ad Group, Ad, Source App level.

## Dimensions Mapping

| Dimension / Data Source | Country | Campaign | Ad Group      | Ad            | Source App Id                    | Keyword              | OS Version | Ad Type |
|-------------------------|---------|----------|---------------|---------------|----------------------------------|----------------------|------------|---------|
| Google Ads              | Country | Campaign | Ad Group      | Ad            | Group Placement                  |                      |            | Ad Type |
| Facebook Ads            | Country | Campaign | Ad Set        | Ad            |                                  |                      |            |         |
| Unity Ads               | Country | Campaign | Creative Pack | Creative Pack | Source App Id                    |                      | OS Version | Ad Type |
| Apple Search Ads        | Country | Campaign | Ad Group      | Creative Set  | Search Term + Search Term Source | Keyword + Match Type |            |         |
| Applovin                | Country | Campaign |               | Ad            | App Id External                  |                      |            | Ad Type |
| IronSource Ads          | Country | Campaign |               | Creative      | Application Id                   |                      |            | Ad Type |
| Vungle                  | Country | Campaign |               | Creative      | Site Id                          |                      |            | Ad Type |

## Metrics
### From Ad Networks
- Impressions
- Clicks
- Installs
- Cost
- IAP LTV Dx: (average) IAP revenue from a user calculated from the day they install the app (day 0) until day x.

### From Analytics Services (BigQuery for Firebase)
- Active Users: number of users that have at least one user_engagement or session_start during the selected period.
- Duration: (average) total duration of all sessions of a user during the selected period.
- Sessions: (average) number of sessions of a user during the selected period.
- RR Dx (Retention Rate at Day x): total active users at day x divide by total installs at day 0

### From Attribution Services (Appsflyer)
- Att-installs: number of installs recorded by attribution services

### From Mediation Services (IronSource Mediation)
- Ad LTV: (average) Ad revenue from a user calculated from the day they install the app (day 0) until day x.

### Derived metrics
- CTR (clickthrough rate) = clicks / impressions
- CVR (conversion rate) or CTI (click to install) = installs / clicks
- oCVR (conversion rate from impressions to installs) or IPM (Installs per mille – Install per 1000 impressions) = CTR x CVR = installs / impressions
- eCPM (effective cost per mile = effective cost per 1000 impressions) = cost / (1000 x impressions)
- eCPC (effective cost per click) = cost / clicks
- eCPI (effective cost per install) = cost / installs
- Att-eCPI (eCPI fromn attribution services)= costs / att-installs
- LTV: (average) lifetime value of a user, calculated by IAP LTV + Ad LTV (= revenue / att-installs)
- Ad ROAS: returns on ad spend excluding IAP revenue
- ROAS: returns on ad spend including IAP and Ad revenue

## Data retention
When a connector is linked to an app, its data from the last 30 days will be imported. We will send you a notification when data is imported succesfully. Report will be ready after that.

Data of a connector will be removed automatically after 6 months. Please contact us if you would like to keep it longer.

## Attribution using Analytics Service
Firebase is providing attribution service for some ad networks (such as Google Ads) at campaign level. For each user in analytics / mediation service (identified by IDFA / Advertising ID / IDFV), if we can't find this user's attribution information in Attribution Service, we will try to find it in Analytics Service. 

Users attributed using Analytics Service is reportable at campaign level.

## Report limitation
Due to to the way data is organised at some data sources, the report is having these limitations:
- For Apple Search Ads: Ad dimension can't be selected with either Source App Id / Keyword / Ad Group dimension.
- For Google Ads: 
  - Source App Id, Ad, Ad Type dimension can't be selected with Country dimension
  - Source App Id dimension can't be selected with Ad and Ad Type dimension.
- Att-cost: cost from attribution service: only available for Unity Ads and IronSource Ads

## Data import
- We use UTC timezone where possible, otherwise we use the timezone that data source provide.
- Only data from connectors / customers linked to an app is updated regularly.
- [Facebook has stopped sharing viewthrough installs since April 22, 2020](https://support.appsflyer.com/hc/en-us/articles/360007512817-Facebook-AMM-terms-from-April-22-2020). Therefore, data that Cost Center imports from Appsflyer does not have viewthrough users. From our observation usually it's less than 5% attributed users.
- Data update interval:
  - Apple Search Ads: data of the last 3 days is updated every 2 hours.
  - Google Ads: yesterday's data is updated every 2 hours, data of day -3 since today is updated once a day.
  - Facebook Ads: today's and yesterday's data is updated every 2 hours, data of day -3 since today is updated once a day.
  - Unity Ads: today's and yesterday's data is updated every 2 hours, data of day -3 since today is updated once a day.
  - BigQuery: yesterday's data is updated once a day from 6pm to 8pm (UTC) data of day -3 since today is updated once a day from 6pm to 6:30pm.
  - Appsflyer: data of the last 3 days is updated once a day at 6pm (UTC).
  - IronSource Mediation: data of yesterday and day -3 since today are updated once a day at 3pm (UTC).

## Data freshness in Apps page
- App's summarised data is updated hourly + Ad Networks data is updated every 2 hours --> Summarised data can be delayed up to 3 hours in compare with Ad Networks' dashboard.

## Best practices
- Don't change campaign's / ad group's / ad's name unless you really need to do that. Some attribution services are tracking using those name (not id). So when the name's changed, it will lose the historical tracking.
- All timezone settings in Ad Networks, Analytics Services, Attribution Services and Mediation Services should be UTC to avoid data mismatch.
