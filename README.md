# Paylii payment Gateway

## Payment Initiation API Documentation
  

## Endpoint

```

POST https://paylii.com/api/transactions/initiate_payment/

```
  

## Description

This endpoint initiates a new payment transaction and returns a redirect URL to the payment gateway. The API requires authentication via an API key in the request headers.
 

## Authentication

- Required: API Key
- Header: `X-API-Key`

## Request Body

```
{
    "amount": "decimal",
    "currency": "string",
    "redirect_url": "string (optional)",
    "error_url": "string (optional)",
    "callback_url": "string (optional)",
    "metadata": {
        "language": "string (optional, default: 'en')",
        "customer_info": {
            "first_name": "string (required)",
            "last_name": "string (required)",
            "email": "string (required)",
            "phone": "string (required)",
            "countryCode": "string (optional)",
            "country": "string (optional)",
            "address": "string (optional)",
        },
        "product_info":
        [
            {
                "ItemName": "string (optional)",
                "Quantity": "integer (optional)",
                "UnitPrice": "decimal (optional)",
                "Weight": "decimal (optional)",
                "Width": "decimal (optional)",
                "Height": "decimal (optional)",
                "Depth": "decimal (optional)"
            }
        ],
        "custom_data": "any (optional)"
    }
}
```

  
### Parameters

| Parameter    | Type    | Required | Description                               |     |
| ------------ | ------- | -------- | ----------------------------------------- | --- |
| amount       | decimal | Yes      | Payment amount                            |     |
| currency     | string  | Yes      | Currency code (e.g., "USD", "EUR")        |     |
| redirect_url | string  | No       | URL to redirect after payment completion  |     |
| error_url    | string  | No       | URL to redirect after payment error     |     |
| callback_url | string  | No       | URL for payment gateway to send callback  |     |
| metadata     | object  | No       | Additional data to store with transaction |     |

### Metadata Fields

| Field | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| language | string | No | 'en' | Language code in ISO 639-1 format |
| customer_info | object | No | - | Customer information |
| product_info | array | No | - | Product information |
| custom_data | any | No | - | Any additional custom data you want to store |  

### Customer Info Fields

| Field | Type | Required | Default | Description |
| ------- | ------|----------|---------| ------------- |
| first_name | string | No | - | Customer's first name |
| last_name | string | No | - | Customer's last name |
| email | string | No | - | Customer's email address |
| phone | string | No | - | Customer's phone number |
| countryCode | string | No | 'KWT' | ISO 3166-1 alpha-3 country code |
| country | string | No | - | Customer's country |
| address | string | No | - | Customer's address |  

### Product Info Fields

| Field | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| ItemName | string | No | - | Product name |
| Quantity | integer | No | 1 | Product quantity |
| UnitPrice | decimal | No | - | Price per unit |
| Weight | decimal | No | 0 | Product weight |
| Width | decimal | No | 0 | Product width |
| Height | decimal | No | 0 | Product height |
| Depth | decimal | No | 0 | Product depth |  

## Response

### Success Response (200 OK)

```
{
    "redirect_url": "string"
}
```
  

### Error Responses  

#### 400 Bad Request

```
{
    "error": "Payment gateway not found or inactive"
}
```

or

```
{
    "field_name": ["error message"]
}
```
  

#### 401 Unauthorized

```
{
    "error": "Invalid API key"
}
```

  

#### 500 Internal Server Error

```
{
    "error": "Error message"
}
```

  

## Example Usage
  

### cURL

```bash
curl -X POST \
  'https://paylii.com/api/transactions/initiate_payment/' \
  -H 'X-API-Key: your-api-key' \
  -H 'Content-Type: application/json' \
  -d '{
    "amount": "100.00",
    "currency": "USD",
    "redirect_url": "https://your-domain.com/success",
    "error_url": "https://your-domain.com/error",
    "callback_url": "https://your-domain.com/webhook",
    "metadata": {
        "language": "en",
        "customer_info": {
            "first_name": "John",
            "last_name": "Doe",
            "email": "john@example.com",
            "phone": "34567890",
            "countryCode": "KWT",
            "country": "Kuwait",
            "address": "123 Main St"
        },
        "product_info": [
            {          
                "ItemName": "Premium Subscription",
                "Quantity": 1,
                "UnitPrice": "100.00",
                "Weight": 0,
                "Width": 0,
                "Height": 0,
                "Depth": 0
            }
        ]
    }
}'

```
  

### Python (requests)

```python
import requests
  
url = 'https://paylii.com/api/transactions/initiate_payment/'
headers = {
    'X-API-Key': 'your-api-key',
    'Content-Type': 'application/json'
}
data = {
    'amount': '100.00',
    'currency': 'USD',
    'redirect_url': 'https://your-domain.com/success',
    'error_url': 'https://your-domain.com/error',
    'callback_url': 'https://your-domain.com/webhook',
    'metadata': {
        'language': 'en',
        'customer_info': {
            'first_name': 'John',
            'last_name': 'Doe',
            'email': 'john@example.com',
            'phone': '34567890',
            'countryCode': 'KWT',
            'country': 'Kuwait',
            'address': '123 Main St'
        },
        'product_info': [
            {
                'ItemName': 'Premium Subscription',
                'Quantity': 1,
                'UnitPrice': '100.00',
                'Weight': 0,
                'Width': 0,
                'Height': 0,
                'Depth': 0
            }
        ]
    }
}  

response = requests.post(url, headers=headers, json=data)
print(response.json())
```

  
### JavaScript (fetch)

```javascript
const url = 'https://paylii.com/api/transactions/initiate_payment/';
const data = {
    amount: '100.00',
    currency: 'USD',
    redirect_url: 'https://your-domain.com/success',
    error_url: 'https://your-domain.com/error',
    callback_url: 'https://your-domain.com/webhook',
    metadata: {
        language: 'en',
        customer_info: {
            first_name: 'John',
            last_name: 'Doe',
            email: 'john@example.com',
            phone: '34567890',
            countryCode: 'KWT',
            country: 'Kuwait',
            address: '123 Main St',
        },
        product_info: [
            {
                ItemName: "string",
                Quantity: 0,
                UnitPrice: 0,
                Weight: 0,
                Width: 0,
                Height: 0,
                Depth: 0
            }
        ]
    }
};  

fetch(url, {
    method: 'POST',
    headers: {
        'X-API-Key': 'your-api-key',
        'Content-Type': 'application/json'
    },
    body: JSON.stringify(data)
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

## Notes

1. The API requires a valid API key in the request headers
2. The payment gateway must be active and exist in the system
3. The application associated with the API key must be active
4. The response will include a transaction ID and a redirect URL to the payment gateway
5. If the payment gateway processing fails, the transaction will be marked as 'failed'
6. The callback_url will be used by the payment gateway to notify about the payment status
7. The redirect_url will be used to redirect the user after payment completion
8. If not provided, metadata fields will use their default values (countryCode: 'KWT', language: 'en')
9. Customer info fields (name, email, phone) are required when customer_info is provided


## Webhook Notifications

The payment gateway will send webhook notifications to your callback URL to inform you about payment status changes. These notifications are sent via HTTP POST requests.

### Webhook Endpoint

```
POST https://your-domain.com/webhook
```

### Webhook Payload

```json
{
    "transaction_id": "string",
    "status": "string",
    "amount": "string",
    "currency": "string",
    "invoice_id": "string",
    "timestamp": "string",
    "metadata": {
        "myfatoorah_data": {
            "invoice_id": "string",
            "payment_id": "string",
            "customer_reference": "string",
            "transaction_status": "string",
            "payment_method": "string",
            "base_currency": "string",
            "display_currency": "string",
            "pay_currency": "string",
            "invoice_value_base": "string",
            "invoice_value_display": "string",
            "invoice_value_pay": "string"
        }
    }
}
```

### Status Values

| Status | Description |
|--------|-------------|
| completed | Payment was successfully completed |
| failed | Payment failed or was declined |
| cancelled | Payment was cancelled by the user |
| authorized | Payment is authorized but not yet captured |
| processing | Payment is being processed |

### Security

- Webhook requests are signed using HMAC SHA-256
- The signature is sent in the `MyFatoorah-Signature` header
- Validate the signature using your webhook secret key

### Example Webhook Handler

```python
import hmac
import hashlib
import base64

def verify_webhook_signature(payload, signature, secret):
    # Sort payload keys alphabetically
    ordered_parts = []
    for key in sorted(payload.keys(), key=str.lower):
        value = "" if payload[key] is None else payload[key]
        ordered_parts.append(f"{key}={value}")
    
    ordered_string = ",".join(ordered_parts)
    
    # Generate signature
    message_encoded = ordered_string.encode('utf8')
    secret_encoded = secret.encode('utf8')
    hmac_obj = hmac.new(secret_encoded, message_encoded, digestmod=hashlib.sha256)
    calculated_signature = base64.b64encode(hmac_obj.digest()).decode('utf8')
    
    return calculated_signature == signature

@app.route('/webhook', methods=['POST'])
def webhook_handler():
    signature = request.headers.get('MyFatoorah-Signature')
    payload = request.get_json()
    
    # Verify signature
    if not verify_webhook_signature(payload, signature, WEBHOOK_SECRET):
        return jsonify({"error": "Invalid signature"}), 400
    
    # Process the webhook
    transaction_id = payload['transaction_id']
    status = payload['status']
    
    # Update your system based on the payment status
    # ...
    
    return jsonify({"status": "success"})
```

### Best Practices

1. Always verify the webhook signature
2. Implement idempotency to handle duplicate webhooks
3. Respond quickly to webhooks (within 5 seconds)
4. Log all webhook events for debugging
5. Handle all possible status values
6. Keep your webhook secret secure
7. Use HTTPS for your webhook endpoint
8. Implement retry logic for failed webhook deliveries
