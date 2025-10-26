# PayRelock Payment Gateway Module for Dhru Fusion

## 📦 Installation Instructions

### Step 1: Download the Module

**⚠️ NOTICE: Module Currently Being Encrypted**

We're upgrading the module with IonCube encryption for enhanced security.
The download will be available soon from your merchant dashboard.

When ready:
- Login to: https://store.pay.relock.net/merchant/dashboard
- Go to **Settings** → **Downloads**
- Download **Dhru Fusion PayRelock Module (Encrypted)**

### Step 2: Extract Files

Extract the downloaded `payrelock_module.zip` file. You should see:

```
payrelock_module/
├── modules/
│   └── gateways/
│       └── payrelock.php         (Gateway module)
├── payrelock.php                 (IPN callback handler)
├── confirm.php                   (Payment confirmation page)
└── INSTALLATION.md               (This file)
```

### Step 3: Upload Files to Your Dhru Fusion Installation

Upload files to your Dhru Fusion root directory:

**Via FTP/SFTP:**
```
1. Upload 'modules/gateways/payrelock.php' → /your-dhru-root/modules/gateways/
2. Upload 'payrelock.php' → /your-dhru-root/
3. Upload 'confirm.php' → /your-dhru-root/
```

**Via SSH:**
```bash
# Navigate to your Dhru Fusion root
cd /path/to/your/dhru-fusion

# Copy files
cp /path/to/extracted/modules/gateways/payrelock.php modules/gateways/
cp /path/to/extracted/payrelock.php .
cp /path/to/extracted/confirm.php .

# Set proper permissions
chmod 644 modules/gateways/payrelock.php
chmod 644 payrelock.php
chmod 644 confirm.php
```

### Step 4: Activate the Module in Dhru Fusion Admin Panel

1. Login to your Dhru Fusion Admin Panel
2. Go to **Settings** → **Payment Gateways**
3. Find **PayRelock - Crypto Payment Gateway**
4. Click **Activate**

### Step 5: Configure the Module

1. Click **Configure** on the PayRelock gateway
2. Fill in the settings:

   - **API Key**: Your PayRelock API key
     - Get it from: https://store.pay.relock.net/merchant/settings
     - Should start with `pk_test_` (test mode) or `pk_live_` (live mode)
   
   - **Payment Method**: Select your preferred method
     - `binance_usdt` - Binance USDT TRC-20 (2.5% fee)
     - `binance_pay` - Binance Pay UID (1.5% fee)
     - `bank_transfer` - Bank Transfer (0.5% fee)
   
   - **Currency**: Select your currency (USD, EUR, GBP, BDT)
   
   - **Show Fees**: Yes/No (Display gateway fees to customers)

3. Click **Save Changes**

### Step 6: Test the Integration

1. Create a test invoice in your Dhru Fusion
2. Go to the invoice payment page
3. Select **PayRelock** as payment method
4. Click "Pay Now"
5. Complete the test payment
6. Verify the payment is recorded in Dhru Fusion

## 🔧 Configuration Example

```
API Key: pk_test_a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6
Payment Method: binance_usdt
Currency: USD
Show Fees: Yes
```

## 🔐 Getting Your API Key

### For Test/Sandbox Mode:
1. Visit: https://store.pay.relock.net/merchant/register
2. Create your merchant account
3. Login to dashboard
4. Go to **Settings**
5. Copy your **API Key** (starts with `pk_test_`)

### For Live/Production Mode:
1. Login to: https://store.pay.relock.net/merchant/dashboard
2. Go to **Settings**
3. Switch environment to **Live**
4. Copy your **API Key** (starts with `pk_live_`)

## 📊 Payment Flow

```
1. Customer selects PayRelock payment method
        ↓
2. Customer clicks "Pay Now"
        ↓
3. Redirected to PayRelock checkout page
        ↓
4. Customer completes payment (Binance/Bank)
        ↓
5. PayRelock confirms payment
        ↓
6. Customer redirected back to your site
        ↓
7. IPN webhook notifies your Dhru Fusion
        ↓
8. Invoice marked as PAID in Dhru Fusion
```

## 🔔 Webhook Configuration

The module automatically configures webhooks. PayRelock will send payment notifications to:

```
https://your-dhru-site.com/payrelock.php
```

**Note**: Your server must be publicly accessible for webhooks to work!

## 💰 Payment Methods & Fees

| Method | Fee | Min | Max |
|--------|-----|-----|-----|
| Binance USDT (TRC-20) | 2.5% | $1 | $50,000 |
| Binance Pay (UID) | 1.5% | $0.50 | $10,000 |
| Bank Transfer | 0.5% | $10 | $100,000 |

**Note**: Fees are charged by PayRelock and automatically deducted from the payment amount.

## 🐛 Troubleshooting

### "API Key is missing" Error
- Make sure you configured the API key in Dhru admin panel
- Verify the key is correct (no extra spaces)
- Check the module is activated

### "Authentication Failed" Error
- Your API key is invalid
- Get a fresh key from PayRelock dashboard
- Make sure you're using the right environment (test vs live)

### Payments Not Recorded in Dhru Fusion
- Check the `payrelock.php` file is uploaded to root directory
- Verify file permissions (644)
- Check Dhru Fusion error logs
- Ensure your server is publicly accessible (not localhost)

### "Module Not Activated" Error
- Activate the module in Dhru admin panel
- Clear Dhru Fusion cache
- Check file paths are correct

## 📞 Support

### PayRelock Support
- Email: support@relock.net
- Dashboard: https://store.pay.relock.net/merchant/dashboard
- Documentation: https://store.pay.relock.net/docs/

### Dhru Fusion Support
- Contact your Dhru Fusion provider

## 🔄 Updating the Module

To update to a new version:
1. Download the latest version from PayRelock dashboard
2. Backup your current files
3. Upload the new files (overwrite old ones)
4. Clear Dhru Fusion cache
5. Test the integration

## ✅ File Checklist

After installation, verify these files exist:

```bash
# Check files
ls -la modules/gateways/payrelock.php
ls -la payrelock.php
ls -la confirm.php

# Check permissions
# All should be: -rw-r--r-- (644)
```

## 🎯 Requirements

- ✅ Dhru Fusion v6 or v7
- ✅ PHP 7.4 or higher
- ✅ cURL enabled
- ✅ JSON extension enabled
- ✅ Public server (not localhost for live mode)
- ✅ PayRelock merchant account

## 📝 Version History

- **v1.0** (2024-10-25) - Initial release
  - Binance USDT/Pay support
  - Bank transfer support
  - Multi-currency support
  - Automatic webhooks
  - Fee calculation

---

**Ready to accept crypto payments? Install now! 🚀**

Need help? Contact support@relock.net

