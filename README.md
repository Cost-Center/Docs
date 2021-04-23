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

### From Analytics Services (BigQuery for Firebase):
- Active Users
- Duration
- Sessions
- Retention Rate (RR)

### From Attribution Services (Appsflyer):
- Att-installs: number of installs recorded by attribution services
