
# Mi Tigo B2C

**Journey**

Subscription - Mobile + Home

**Description**

blab llbalb abala 

**Goals and KPIs**
- active users
- invoices: pay
- invoices: electronic invoices activated
- nps

## Features
- Login with email: mobile+fixed accounts
- Login with HE. limited view + switch to email
- Discovery
    - Banner
    - Push notifications
- Use & Self-service
    - See Balances
    - See Quota
    - Call History
    - Sms History
    - Internet details 
    - Buy Add-Ons
        - core balance
        - mfs
    - Loans
    - Invoices
    - Pay invoice
        - CC/DC
        - tokenization
        - Recurrent payment
        - With TM
    - Invoice History
    - Download last invoice
    - Loans
        - current debt & credit limit
        - loan balance
        - loan packs
    - Home self-service
        - change wifi password
        - change wifi name
        - reset modem
- Care & Recommendation
    - NPS
    - Help
        - chat
        - faq

## Basic architecture

```mermaid
graph TD

subgraph Channel Juvo
    android[Android]
    ios[ios]
    appbackend[App Backend]
    fapi[API Proxy]
    android---appbackend
    ios---appbackend
    appbackend---fapi
end

subgraph Channel Bits
    web[web - Angular]
    drupal[drupal]
    web-->drupal
end

subgraph Digital Backend
    backend[Apigee]
    fapi-->backend
    drupal-->backend

    segment
    newrelic
    payment_gateway
    tigoid
end

subgraph Country
    bss[Core BSS - OSB]
    mobile[Mobile]
    fixed[Fixed]
    backend-->bss
    bss-->fixed
    bss-->mobile
end
subgraph Mobile Domain
    customer[customer]
    products[product catalog]
    lend[lending]
    fulfillment[fulfillment]
    mfs[mfs]
    dpi[dpi]
    mobile-->customer
end

subgraph fixed Domain
    customerfixed[customer fixed]
    productsfixed[product catalog]
    fulfillmentfixed[order management]
    fixed-->customerfixed

end

```



## Implementation Details

### Authentication
- tigo id
    - TigoID Public

### Exposure layer
- apigee
    - Tigo Mobile Upselling Info
    - Tigo Lend APIs
    - Tigo Mobile Product Fulfillment
    - TigoMoney Payment
    - TigoMoney AccountStatusService
    - Selfcare Api V2
    - BSS Product
- kinesis

### Engines / Enablers
- payment gateway
- evam
    - lifecycle campaigns
    - broadcast
    - upselling (exacaster)
- zendesk

### Marketing tools
- digital turbine
- push notifications
    - pushwoosh
- kannel
- yourls
- attribution tools
    - tune
    - appflyer

### Repositories
- redshift
- BaaS
- Convergent DB
- S3

### Other tools
- segment
- new relic
- tableau
    - dashboard tigo shop
    - active users
- analytics
    - mixpanel
    - google analytics
    - facebook analytics

## SOUTH ARCHITECTURE (COUNTRY)

### Data services
- exacaster
    - nbo prepaid
    - nbo pospaid

