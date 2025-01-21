I had a [conversation](https://chatgpt.com/share/a79ee928-8073-4c3c-addb-771cfa4c4489) with ChatGPT about the SaaS shop data model and APIs. The result is documented here.

## Users

1. Videm (cloud → volume capacity, time limit)(SaaS)
2. Liom(cloud → monthly subscription, 2 different subscriptions)(SaaS)
3. Pixiee(SaaS)
4. Muchin(e-commerce)
5. Alireza Sakhi -kandovan co-(e-commerce)
6. Rentamoon(SaaS)
7. Paziresh 24 booking payment(e-commerce)
8. Paziresh24 medical center(SaaS/Subscription, annually)
9. CRM Paziresh24(e-commerce)
10. Divar(SaaS)
11. ISP Provider(SaaS)
12. Spotify / Filimo / Taghche (per book + infinite)

## New Idea

We have 3 different services: read in detail [here](https://www.notion.so/user-flow-a2c8de2ab1c947b28fcd7af2e0d12049?pvs=21)

- Shop
    - Products/Package
    - Invoice/purchases
        - revenue sharing
        - tax handler
- SaaS
    - Enrollment
    - Usage
- E-commerce
    - Baskets

## Main Questions in SaaS services:

1. What does the user buy?
Answer: **Invoice**
2. How much does the user spend?
Answer: **Usage**
3. How much remains to spend?
Answer: **Usage**.**Remaining**
4. What can I renew?

Open Questions:

1. How can we check if a volume package requires a subscription service to use? (ISP volume package model)

## Data Model

## 8.1 SaaS

**8.1.1 Enrollment**

```json
{
  "Enrollment": {
    "uid": "uuid", // Unique identifier for the plan
    "created_at": "datetime",
    "updated_at": "datetime",
    "metadata": null,
    "is_deleted": false,
    "business_id": "uuid",
    "user_id": "string", // ID of the user
    "invoice_id":"sting",// ID of invoice this enrollment created by that
    
    "start_at": "datetime", // in day 0 the start_at is created_at
		"expired_at": "datetime",
    "plan": "json", // all plan data at the moment of enrollment copy here
  }
}
```

**8.1.2 Usage**

```python
Get all active enrollments for user_id:
	- (bus_id, user_id, expiration > now()) 
	- on_item is None or on_item in enrollment.on_items
	- resource in enrollment.limits

sort by on item, expiration # general plan is used last

for enrollment in enrollments:
	if enrollment.last_usage.remain[filter(resource)].volume > volume and (
		enrollment.on_item is None
		or on_item in enrollment.on_items
	):
		return enrollment
raise 'failed'
```

```json
{
  "Usage": {
    "uid": "uuid", // Unique identifier for the plan
    "created_at": "datetime",
    "updated_at": "datetime",
    "metadata": null,
    "is_deleted": false,
    ***"business_id": "uuid",***
    ***"user_id": "uuid", // ID of the user***
    
    "enrollment_id": "uuid",
    ***"resource": "image",
    "volume": "2",
    "on_item": "car",***
    "remain_resource": {
	    { 
		      "resource": "image", //                           image
		      "limit": 28          //                           30
		    },
		    {
		      "resource": "render", //                          render
		      "limit": 100 // the unit is "day"                 100
		    },
		    { 
		      "resource": "char", //                            char
		      "limit": 100000 // the unit is "day"              100000
		    }
    }
  }
}
```

## 8.2 Shop

**8.2.1 Plan**

```json
{
  "Plan": {
    "uid": "uuid", // Unique identifier for the plan
    "created_at": "datetime",
    "updated_at": "datetime",
    "metadata": null,
    "is_deleted": false,
    "business_id": "uuid",
 
    "name*": "string", // Name of the plan                20G monthly
    "description": "string", // Description of the plan  ...
    "price*": "number", // Price of the plan              100
    "currency*": "string", // Currency of the price       KT
    "is_active": true, // is this plan active for enrollment or not
    "category": "",
    // "tag": "",
    
    "data": {
	    "duration*": 90, // days                              30
	    "Resources*": [
		    { 
		      "resource": "API Calls", //                      image
		      "limit": 1000            //                      30
		    },
		    {
		      "resource": "cycle_period", //                   render
		      "limit": 90 // the unit is "day"                 100
		    },
		    { 
		      "resource": "cycle_period", //                   char
		      "limit": 90 // the unit is "day"                 100000
		    }
	    ],
	    "on_items*": [] or null // "car"
	  }
  }
}
```

**8.2.2 Revenue Sharing Service**

```json
{
  "Rule": {
    "id": "uuid", // Unique identifier for the revenue sharing rule
    "created_at": "datetime",
    "metadata": null,
    "is_deleted": false,
    "business_id": "uuid",

    "name": "string",
    "description": "string",
    "is_default": false,
    "is_active": true,

    "shares" : [
	    {
		    "wallet": "wallet ()",   // pezeshk ()
		    "share": 0.6,            // 0.7
		  },
		  {
		    "wallet": "wallet",      // Paziresh
		    "share": 0.2,            // 0.24
		  },
		  {
		    "wallet": "wallet",      // UFaaS
		    "share": 0.1,            // 0.03
		  },
		  {
		    "wallet": "wallet",      // Tax
		    "share": 0.1,            // 0.03
		  }
    ]
  }
}

```

**8.2.3 Invoice and Billing**

[ثبت صورتحساب با استفاده از API_v7.1.1.pdf](https://prod-files-secure.s3.us-west-2.amazonaws.com/45938a98-8b93-4194-95b4-2c8ecea9dc6e/c6bc7855-5630-4fd8-8eb2-cd2dbd0598b6/_____API_v7.1.1.pdf)

[UnitType_P1.pdf](https://prod-files-secure.s3.us-west-2.amazonaws.com/45938a98-8b93-4194-95b4-2c8ecea9dc6e/3ee5527e-08bf-4da1-acd8-44294ccbf18b/UnitType_P1.pdf)

[MoneyType_P2.pdf](https://prod-files-secure.s3.us-west-2.amazonaws.com/45938a98-8b93-4194-95b4-2c8ecea9dc6e/af773c16-4e33-454f-a9de-c3047c70b712/MoneyType_P2.pdf)

```json
{
  "Invoice": {
    "uid": "string", // Unique identifier for the invoice
    "created_at": "datetime",
    "updated_at": "datetime",
    "metadata": null,
    "is_deleted": false,
    "business_id": "uuid",
    
    "merchant": "", // seller data in an invoice
    "customer": "", // buyer data in an invoice 
    
    "proposal_id": "", // from core
    "transaction_id": "", // from core 
    
    // "currency": "USD", redundant, we have it at the bottom after amount.
    
    "items": [ {
	    "id": "",
	    "tax_id": "",
	    "details": "rent",
	    "seller": "rentamoon",
	    "quantity": 1,
	    "unit_price": 20,
	    "discount": 1,
	    "currency": "EUR",
	    "currency_fee": "1.09",
	    
	    "data": {}, // store deliverable data here
	    "revenue_share_id": "rule_uuid",
	    "webhook_url*": "URL", // POST item / the URL that called in delivery stage 
			"product_url" : "URL", // link to product page
	    "update_url": "URL", //  GET item. / the url that called before basket finilization to ensure the item price and quantity is valid / if null, no update needed
	    "reserve_url": "url" //  POST item / the url that reserve the product for customer (flight ticket example). if null, no reservation applied before payment
	    // "reserve_result_callback": "url" // reservation canceled or purchase succeeded
    } ]
    
    "user_id": "string", // ID of the user -> redundant
    "enrollment_id": "string", // ID of the plan -> redundant
    "amount": "number", // Invoice amount
    "currency": "string", // Currency of the amount
    
    "status": "string", // Status of the invoice (e.g., paid, unpaid)
    "due_date": "datetime", // Due date for the payment
    "issued_date": "string" // Date the invoice was issued
  }
  
  
}
```

```json
{
	"item": {
		"uid": "string", // Unique identifier for the invoice
    "created_at": "datetime",
    "updated_at": "datetime",
    "metadata": null,
    "is_deleted": false,
    "business_id": "uuid",
    
    "items": [ { 
	    "id": "",
	    "": "",
	    "name": "", "description": "",
	    "unit_price": 120, "currency": "KT", "quantity": 3, 
	    "discount": 20,
    }]
	}
}
```

**8.2.4 Tax Handler (Based On regional Law and Regulation)**

```json
{
"moaddian": {
	    "invoiceNumber": "3",
      "invoiceDate": "2024-06-15 14:18:11",
      "saleType": 1, // 1 no bourse, 2 bourse kala, 3 bourse energy, 4 govahi seporde kala
      "invoiceType": 2, //
      "invoicePattern": 1, // 1 with customer, 2 without customer
      "invoiceSubject": 1, // 1 main, 2 modify, 3 cancel, 4 bargasht az foroosh
      "paymentType": 1, // 1 naghd, 2 nesye, 3 naghdi nesye
      "uniqueId": "fe14229a-6754-49b1-b637-affe320eaf72",
      "buyerType": 1, // 1 haghighi, 2 hoghooghi
      "description": "",
      "invoiceItems": [{
	      "commodityType": 1, // always 1
        "commodityCode": "2330001031092", // tax id
        "amount": 1, 
        "unitType": 1627, // 1627 for addad
        "moneyType": 364, // 364 for IRR
        "unitPrice": 1000000, 
        "discount": 90909,
        "taxPercent": 10,
        "taxPrice": 90909.1
      }],
      
      "result": {
	      "data": [{
		      "status": 3,
		      "uniqueId": "fe14229a-6754-49b1-b637-affe320eaf72",
		      "trakingId": "7f6a90c9-edca-43a3-b44b-a7a1d4dc51b7",
		      "taxSerialNumber": "A2YPGZ04DB900000000644",
		      "description": "",
		      "title": ""
		    }],
        "error": false,
        "invoiceNumber": 106,
        "invoiceDate": "2024-06-23 14:34:02",
        "saleType": 1,
        "invoiceType": 2,
        "invoicePattern": 1,
        "invoiceSubject": 1,
        "paymentType": 1,
        "uniqueId": "fe14229a-6754-49b1-b637-affe320eaf72",
        "buyerType": 1,
        "invoiceItems": [{
          "commodityType": 1,
          "commodityCode": "2330001031092",
          "amount": 1,
          "unitType": 1627,
          "moneyType": 364,
          "unitPrice": 1700000,
          "discount": 154545,
          "taxPercent": 10,
          "taxPrice": 154545.5
        }],
        "unique": 549887768
      }
    }
```

**8.2.5 Basket**

```json
{
    "uid": "uuid", // Unique identifier for the invoice
    "created_at": "datetime",
    "updated_at": "datetime",
    "metadata": null,
    "is_deleted": false,
    "business_id": "uuid",
    "user_id": "uuid",
    
    "status": "open/close/reserve/cancelled",
    "invoice_id": "invoice_id" | null,
    "currency": "USD",
    
    "items": [ {
	    "id": "",
	    "tax_id": "",
	    "details": "rent",
	    "seller": "rentamoon",
	    "quantity": 1,
	    "unit_price": 20,
	    "discount": 1,
	    "currency": "EUR",
	    "currency_fee": "1.09",
	    
	    "data": {},
	    "revenue_share_id": "rule_uuid",
	    "webhook_url*": "URL", // POST item / the URL that called in delivery stage 
			"product_url" : "URL", // link to product page
	    "update_url": "URL", //  GET item. / the url that called before basket finilization to ensure the item price and quantity is valid / if null, no update needed
	    "reserve_url": "url" //  POST item / the url that reserve the product for customer (flight ticket example). if null, no reservation applied before payment
	    // "reserve_result_callback": "url" // reservation canceled or purchase succeeded
    } ]
    
    "amount": "number", // basket amount
    "checkout_at": "datetime" | null
  }
}
```

## 9. API Documentation