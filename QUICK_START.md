# Quick Start Guide

## 🎉 Your E-Commerce Platform is Ready!

Your complete e-commerce solution with Supabase backend, PayU integration, and admin dashboard has been set up. Follow these steps to get it running.

---

## ⚡ Quick Setup (5 Minutes)

### Step 1: Run the Database Migration

1. Open your Supabase project: https://app.supabase.com
2. Go to **SQL Editor** → **New Query**
3. Copy all content from `supabase/migrations/001_init_schema.sql`
4. Paste and run the query
5. Wait for completion ✓

### Step 2: Create Admin Account

Run this SQL in Supabase SQL Editor:

```sql
-- Create admin user profile
INSERT INTO public.profiles (id, email, full_name, role)
VALUES (
  '00000000-0000-0000-0000-000000000000',
  'admin@example.com',
  'Admin User',
  'admin'
) ON CONFLICT (email) DO UPDATE SET role = 'admin';
```

**Note:** Replace the UUID with the actual user ID from Supabase Auth

### Step 3: Start the App

```bash
npm run dev
```

The app will start on `http://localhost:5173`

---

## 🔐 Admin Login

- **URL**: `http://localhost:5173/admin/login`
- **Email**: `admin@example.com`
- **Password**: Your Supabase password

---

## 📍 Quick Links

### Customer Areas
- **Home**: `/`
- **Shop**: `/store`
- **Cart**: Floating button (bottom right)
- **Checkout**: `/checkout`
- **Orders**: `/orders`

### Admin Areas
- **Admin Login**: `/admin/login`
- **Dashboard**: `/admin/dashboard`
- **Manage Orders**: `/admin/orders`
- **Manage Inventory**: `/admin/inventory`
- **Manage Memberships**: `/admin/memberships`

---

## 📋 What's Included

### ✅ Database (Supabase)
- Users & Profiles with roles (admin/customer)
- Products with inventory tracking
- Orders with detailed tracking
- Memberships & Subscriptions
- Payment transactions
- All with Row-Level Security (RLS)

### ✅ Authentication
- Supabase Auth integration
- JWT token-based sessions
- Admin & Customer role management
- Protected routes and pages

### ✅ Admin Dashboard
- **Dashboard**: Stats, charts, recent orders
- **Orders**: View, filter, update status, export CSV
- **Inventory**: Add/edit/delete products, stock alerts
- **Memberships**: Create and manage plans
- **Navigation**: Sidebar with quick access

### ✅ Customer Features
- **Shopping**: Browse products by category
- **Cart**: Add/remove items, manage quantities
- **Checkout**: Shipping address, order review
- **Payments**: PayU integration (demo mode enabled)
- **Orders**: Track order status with visual progress

### ✅ PayU Integration
- Payment initiation and verification
- Demo mode for testing (no real payments needed)
- Transaction logging
- Order status updates on payment

---

## 🛠️ Admin Dashboard Features

### Dashboard Tab
- Total orders count
- Total revenue
- Product count
- Memberships count
- Order trends (7-day graph)
- Revenue trends (7-day graph)
- Recent orders list

### Orders Tab
- Filter by order status
- Filter by payment status
- Sort and search
- Update order status in real-time
- Export to CSV
- View detailed order information

### Inventory Tab
- Add new products
- Edit existing products
- Delete products
- Stock level alerts (low & out of stock)
- SKU management
- Price and discount tracking

### Memberships Tab
- Create membership plans
- Set price and duration
- Add custom benefits
- Edit and delete plans
- Activate/deactivate plans

---

## 🧪 Test the Platform

### Create Sample Products

1. Go to `/admin/login`
2. Sign in with admin credentials
3. Click **Inventory** → **Add Product**
4. Fill in details:
   - Name: "Premium Ice Skates"
   - Price: 2999
   - Category: "Ice Skates"
   - Stock: 50
5. Click **Create Product**
6. Repeat for more products

### Test Customer Flow

1. Sign in as customer at `/auth`
2. Go to `/store` and add products to cart
3. Click cart button (bottom right)
4. Click **Checkout**
5. Fill shipping details
6. Click **Continue to Payment**
7. Payment is automatically processed (demo mode)
8. View order at `/orders`

---

## 🔧 Configuration

### Environment Variables

Your Supabase credentials are already configured:
- `VITE_SUPABASE_URL`: Your Supabase URL
- `VITE_SUPABASE_ANON_KEY`: Your anonymous key

### PayU Setup (Optional)

For live PayU payments, add:
```
VITE_PAYU_KEY=your_key_here
VITE_PAYU_SALT=your_salt_here
VITE_PAYU_BASE_URL=https://secure.payu.in
```

Currently running in **demo mode** (simulated payments).

---

## 📱 Features in Detail

### Authentication
- ✓ Sign up for customers
- ✓ Sign in with email/password
- ✓ Admin role verification
- ✓ Protected routes
- ✓ Session management

### Shopping Cart
- ✓ Add/remove items
- ✓ Update quantities
- ✓ Clear cart
- ✓ Persistent storage (localStorage)

### Checkout & Payments
- ✓ Shipping address form
- ✓ Order summary
- ✓ PayU integration
- ✓ Demo payment simulation
- ✓ Order confirmation

### Order Tracking
- ✓ Order history
- ✓ Status tracking (Pending → Confirmed → Processing → Shipped → Delivered)
- ✓ Order details view
- ✓ Item-by-item breakdown

### Admin Controls
- ✓ Real-time order updates
- ✓ Inventory management
- ✓ Stock alerts
- ✓ Membership creation
- ✓ Analytics dashboard

---

## 🚀 Deployment

### Deploy to Production

1. **Vercel/Netlify**:
   ```bash
   npm run build
   # Upload the 'dist' folder
   ```

2. **Docker**:
   ```bash
   docker build -t ecommerce .
   docker run -p 3000:5173 ecommerce
   ```

3. **Traditional Server**:
   ```bash
   npm run build
   # Upload 'dist' folder to web server
   ```

### Environment Variables for Production
- Set `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY`
- Add real PayU credentials
- Update any hardcoded URLs

---

## 🐛 Troubleshooting

### Admin Login Fails
- ✓ Verify profile exists in Supabase with role='admin'
- ✓ Check email matches exactly
- ✓ Clear browser cache and cookies

### Products Not Showing
- ✓ Ensure products have `is_active = true`
- ✓ Check product category matches
- ✓ Verify images are accessible (use full URLs)

### Cart Not Working
- ✓ Check browser console for errors
- ✓ Verify CartContext is wrapping the app
- ✓ Clear localStorage: `localStorage.clear()`

### Payment Issues
- ✓ Currently in demo mode (all payments succeed)
- ✓ For real PayU, update `src/services/payment.ts`
- ✓ Check PayU credentials in environment

---

## 📚 Full Documentation

For detailed information, see:
- **IMPLEMENTATION_GUIDE.md** - Complete setup & features
- **Database Schema** - See `supabase/migrations/001_init_schema.sql`
- **API Documentation** - See `src/services/database.ts`

---

## 🎯 Next Steps

1. ✅ Run database migration
2. ✅ Create admin account
3. ✅ Add sample products
4. ✅ Test admin dashboard
5. ✅ Test customer checkout
6. ✅ Configure PayU for production
7. ✅ Deploy to production

---

## 💡 Tips

- Use the **Dashboard** to monitor business metrics
- Export orders from **Orders** page for accounting
- Keep inventory updated in **Inventory** page
- Test payment flow before going live
- Monitor order status and update customers

---

## 🆘 Need Help?

Check the detailed guides in:
1. `IMPLEMENTATION_GUIDE.md` - Comprehensive setup
2. Browser console - Look for error messages
3. Supabase dashboard - Check data in tables
4. Network tab - Inspect API calls

---

## 🎊 You're All Set!

Your e-commerce platform is ready. Start with:

```bash
npm run dev
```

Then visit: `http://localhost:5173`

Happy selling! 🚀
