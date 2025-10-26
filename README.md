# PayRelock API Documentation

## Overview
PayRelock is a crypto payment gateway API similar to PayerOne.

## Base URL
- **Production**: `https://pay.relock.net/api/v1`
- **Sandbox**: `https://pay.relock.net/api/v1/sandbox`

## Authentication
All API requests require a Bearer token in the Authorization header:

```
Authorization: Bearer YOUR_API_KEY_HERE
```

## Endpoints

### 1. Create Order
```http
POST /api/v1/orders
```

**Request Body:**
```json
{
  "merchant_order_id": "ORD-12345",
  "amount": 100.00,
  "currency": "USD",
  "payment_method": "binance_usdt",
  "callback_url": "https://yoursite.com/webhook",
  "return_url": "https://yoursite.com/success",
  "cancel_url": "https://yoursite.com/cancel",
  "customer": {
    "email": "customer@example.com",
    "name": "John Doe"
  },
  "metadata": {
    "product_id": "123",
    "notes": "Custom data"
  }
}
```

**Response:**
```json
{
  "success": true,
  "order_id": "PR-2024-10-12345",
  "payment_url": "https://pay.relock.net/checkout/PR-2024-10-12345",
  "amount": 100.00,
  "currency": "USD",
  "expires_at": "2024-10-25T12:30:00Z",
  "status": "pending"
}
```

### 2. Get Order Details
```http
GET /api/v1/orders/{order_id}
```

**Response:**
```json
{
  "success": true,
  "order_id": "PR-2024-10-12345",
  "merchant_order_id": "ORD-12345",
  "amount": 100.00,
  "currency": "USD",
  "status": "paid",
  "payment_method": "binance_usdt",
  "transaction_id": "TXN-ABC123",
  "paid_at": "2024-10-25T12:15:30Z",
  "created_at": "2024-10-25T12:00:00Z"
}
```

### 3. IPN (Webhook) Notification
When payment is completed, we send POST request to your `callback_url`:

```json
{
  "event": "payment.success",
  "order_id": "PR-2024-10-12345",
  "merchant_order_id": "ORD-12345",
  "amount": 100.00,
  "currency": "USD",
  "payment_method": "binance_usdt",
  "transaction_id": "TXN-ABC123",
  "paid_at": "2024-10-25T12:15:30Z",
  "signature": "sha256_hmac_signature_here"
}
```

## Status Codes
- `pending`: Order created, awaiting payment
- `processing`: Payment detected, confirming
- `paid`: Payment successful
- `expired`: Payment window expired
- `cancelled`: Order cancelled
- `failed`: Payment failed

## Supported Payment Methods
- `binance_usdt`: Binance USDT TRC-20
- `binance_pay`: Binance Pay (UID)
- `bank_transfer`: Local bank transfer
- `crypto_btc`: Bitcoin
- `crypto_eth`: Ethereum

## Error Codes
- `401`: Invalid or missing API key
- `400`: Invalid request parameters
- `404`: Order not found
- `429`: Rate limit exceeded
- `500`: Server error

