# Cost Center Documentation

## What's Our Goal?

Cost Center's goal is collecting all raw data from your Ad Networks, Attribution Service, Analytics Service, Monetization Service and combine it into one report. When combine the data, Cost Center generate most powerfull metrics that can give you enough information for making decistion like:
* LTV Day x: Life time value at a day LTV D1, LTV D3, LTV D7, LTV D14, LTV 30, LTV 60
* ROAS Day x: Return on ad spend at a day ROAS D1, ROAS D3, ROAS D7, ROAS D14, ROAS D30, ROAS D60
* RR Day x: Retention at a day RR D1, RR D3, RR D7, RR D14, RR D30, RR D60
* Duration

All the powerfull metrics above can breakdown at Country, Campaign, Ad Group, Ad, Source App level.

## Dimensions Mapping

| Data Source / Dimension | OS Version | Country | Campaign | Ad Group      | Ad Type | Ad            | Source App Id                    | Keyword              |
|-------------------------|------------|---------|----------|---------------|---------|---------------|----------------------------------|----------------------|
| Google Ads              |            | Country | Campaign | Ad Group      |         | Ad            | Group Placement                  |                      |
| Facebook Ads            |            | Country | Campaign | Ad Set        |         | Ad            |                                  |                      |
| Unity Ads               | OS Version | Country | Campaign | Creative Pack | Ad Type | Creative Pack | Source App Id                    |                      |
| Apple Search Ads        |            | Country | Campaign | Ad Group      |         | Creative Set  | Search Term + Search Term Source | Keyword + Match Type |

## Metrics
### From Ad Networks:
- Impressions
- Clicks
- Installs
- Cost
- IAP LTV Dx: (average) IAP revenue from a user calculated from the day they install the app (day 0) until day x.

### From Analytics Services (BigQuery for Firebase):
- Active Users: number of users that have at least one user_engagement or session_start during the selected period.
- Duration: (average) total duration of all sessions of a user during the selected period.
- Sessions: (average) number of sessions of a user during the selected period.
- RR Dx (Retention Rate at Day x): total active users at day x divide by total installs at day 0

### From Attribution Services (Appsflyer):
- Att-installs: number of installs recorded by attribution services

### From Mediation Services (IronSource Mediation):
- Ad LTV: (average) Ad revenue from a user calculated from the day they install the app (day 0) until day x.

### Derived metrics:
- CTR (clickthrough rate) = clicks / impressions
- CVR (conversion rate) or CTI (click to install) = installs / clicks
- oCVR (conversion rate from impressions to installs) or IPM (Installs per mille – Install per 1000 impressions) = CTR x CVR = installs / impressions
- eCPM (effective cost per mile = effective cost per 1000 impressions) = cost / (1000 x impressions)
- eCPC (effective cost per click) = cost / clicks
- eCPI (effective cost per install) = cost / installs
- Att-eCPI (eCPI fromn attribution services)= costs / att-installs
- LTV: (average) lifetime value of a user, calculated by IAP LTV + Ad LTV
- Ad ROAS: returns on ad spend excluding IAP revenue
- ROAS: returns on ad spend including IAP and Ad revenue
