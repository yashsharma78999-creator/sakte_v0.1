# Fix: "TypeError: Failed to fetch" - Supabase Connection Error

## ❌ Error You're Getting
```
TypeError: Failed to fetch
    at window.fetch (eval at messageHandler...)
```

This error happens when the browser can't reach Supabase server, usually due to:
1. **Network connectivity issue** - Can't reach Supabase from builder environment
2. **Invalid/missing environment variables** - Supabase URL or key not loaded
3. **Supabase server unreachable** - Project might be inactive
4. **CORS issue** - Supabase blocking requests from your domain

---

## 🔍 Step 1: Test Supabase Connection

I've added a **diagnostic test page** that will help identify the exact problem.

### How to access it:
1. Go to: **`/test/supabase`** on your app
2. This page will run automatic tests and show:
   - ✅ Environment variables loaded
   - ✅ Supabase client initialized
   - ✅ Auth session access
   - ✅ Database connectivity

### What to look for:
**If you see red X marks**, the test will tell you exactly what's wrong.

---

## ✅ Quick Fix Checklist

### Fix #1: Verify Environment Variables

**In Builder.io:**
1. Go to Settings (top right)
2. Check Environment Variables section
3. Verify you have:
   - `VITE_SUPABASE_URL` = `https://zrqguzpaddamvbsjzyfz.supabase.co`
   - `VITE_SUPABASE_ANON_KEY` = your anon key

**The URL must:**
- Start with `https://`
- Be from Supabase (format: `https://[project-id].supabase.co`)
- Match your actual Supabase project

### Fix #2: Test Supabase Project is Active

1. Go to your Supabase Dashboard
2. Check your project is **not suspended**
3. Verify project is in **active** status
4. Check project hasn't hit rate limits

### Fix #3: Check CORS Settings (if needed)

In Supabase Dashboard → Settings → API:
- Look for "CORS" or "Allowed Origins"
- Make sure your builder domain is allowed
- If you see your domain, check it's allowed for all methods

### Fix #4: Network Connectivity

The builder environment might have restricted network access:
1. Open DevTools (F12 → Console)
2. Run this command:
```javascript
fetch('https://zrqguzpaddamvbsjzyfz.supabase.co/rest/v1/').then(r => r.json()).then(d => console.log('✓ Can reach Supabase:', d)).catch(e => console.log('✗ Cannot reach Supabase:', e))
```

**If you see error**: Network is blocked from your environment

---

## 🛠️ Advanced Debugging

### Check Browser Console (F12)

You should see these log messages:
```
[SUPABASE] Initializing client
[SUPABASE] URL: https://zrqguzpaddamvbsjzyfz.supabase.co
[SUPABASE] Key loaded: true
[SUPABASE] Client initialized successfully
```

**If you see errors instead:**

#### Error: "Missing environment variables"
**Solution:**
- Environment variables not loading
- Go to Settings → Environment Variables
- Refresh the page
- Hard refresh (Ctrl+Shift+R / Cmd+Shift+R)

#### Error: "Invalid URL format"
**Solution:**
- URL doesn't start with `https://`
- Check Settings → Environment Variables
- Ensure full URL like `https://[project].supabase.co`

#### Error: "Failed to fetch"
**Solution:**
- Network can't reach Supabase
- Try the fetch test above
- Check Supabase status page: https://status.supabase.com

---

## 📋 Complete Diagnostic Steps

### Step 1: Run Test Page
1. Go to `/test/supabase`
2. Wait for all tests to complete
3. Take a screenshot of the results
4. Note any red X marks

### Step 2: Check Console Logs
1. Open DevTools (F12)
2. Go to Console tab
3. Look for `[SUPABASE]` messages
4. Copy any error messages

### Step 3: Test Network Access
1. In Console, paste:
```javascript
fetch('https://zrqguzpaddamvbsjzyfz.supabase.co/rest/v1/')
  .then(r => console.log('✓ Status:', r.status))
  .catch(e => console.log('✗ Error:', e.message))
```
2. You should see "✓ Status: 401" or similar
3. If you see error, network is blocked

### Step 4: Verify Supabase Project
1. Log in to Supabase Dashboard
2. Click your project
3. Check status shows "Active"
4. Verify no suspension warnings
5. Check you're not over quota

### Step 5: Test with Different Browser
1. Try in a different browser (Chrome, Firefox, Safari)
2. Clear cache/cookies
3. Try incognito/private window
4. This helps identify client-side issues

---

## Common Solutions by Error Type

### Error: Environment Variables Missing
```
[SUPABASE] ERROR: Missing environment variables
[SUPABASE] VITE_SUPABASE_URL: ✗ Missing
```

**Fix:**
```bash
# In Settings → Environment Variables, add:
VITE_SUPABASE_URL=https://zrqguzpaddamvbsjzyfz.supabase.co
VITE_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

### Error: Cannot Reach Supabase
```
TypeError: Failed to fetch
    at window.fetch
```

**Fix Options:**
1. **Check network connectivity:**
   - Run fetch test above
   - Check firewall/proxy settings
   - Try from different network

2. **Check Supabase status:**
   - Visit https://status.supabase.com
   - Check for service interruptions
   - Wait for any maintenance to complete

3. **Reset Supabase client:**
   - Hard refresh page (Ctrl+Shift+R)
   - Clear browser cache
   - Try incognito window

4. **Contact Supabase Support:**
   - If status shows issues
   - Project is suspended
   - Rate limited or quota issues

### Error: Auth Session Fails
```
[SUPABASE] Connection test failed: {...}
```

**Fix:**
1. Check RLS policies exist
2. Verify anon key is correct
3. Check auth configuration in Supabase

### Error: Database Query Fails
```
[SUPABASE] Database query successful: Error
```

**Fix:**
1. Verify tables exist (user_memberships, memberships, etc.)
2. Check RLS policies allow anon reads
3. Verify database isn't corrupted

---

## 🚀 After Fixing the Error

Once `/test/supabase` shows all green checks:

1. **Test memberships:**
   - Go to Admin → Memberships
   - Should load without errors
   - Can create/edit memberships

2. **Test checkout flow:**
   - Go to Programme page
   - Add membership to cart
   - Go to Checkout
   - Complete purchase

3. **Check subscribers:**
   - Go to Admin → Subscribers
   - Should show subscriber count > 0
   - Can search and filter

4. **Verify user profile:**
   - Go to Profile
   - Should show "My Memberships"
   - Active membership visible

---

## 🆘 If Problem Persists

### Gather This Information:
1. **Screenshot of `/test/supabase` page** - shows which tests fail
2. **Console error messages** - copy full error text
3. **Supabase project ID** - from dashboard URL
4. **Environment variables being used** - (don't share secret values)
5. **Network type** - (public wifi, VPN, corporate network, etc)

### Share With Support:
- Screenshot of failing test
- Console error from F12
- Error occurs on which page
- Steps to reproduce
- Browser and OS version

---

## 📚 Reference

### Test Page URL
- Direct access: `/test/supabase`
- Full: `https://your-app-url.builderio.xyz/test/supabase`

### Environment Variables Needed
```
VITE_SUPABASE_URL=https://[project-id].supabase.co
VITE_SUPABASE_ANON_KEY=[your-anon-key]
```

### Key Files Modified
- `src/lib/supabase.ts` - Better error handling and logging
- `src/pages/SupabaseTest.tsx` - Diagnostic test page
- `src/App.tsx` - Added test route

### Console Log Prefixes to Watch For
- `[SUPABASE]` - Configuration and connection logs
- `[PAYMENT]` - Payment and membership processing logs
- `[DATABASE]` - Database operation logs

---

## ✨ Summary

1. **Go to `/test/supabase`** to identify the exact issue
2. **Check Console (F12)** for `[SUPABASE]` error messages
3. **Verify environment variables** in Settings
4. **Test network access** with fetch command
5. **Check Supabase status** and project is active
6. **Share diagnostic info** if issue persists

The diagnostic page will tell you exactly what's wrong! 🔍
