# Groq AI Setup Guide for Stickonomics

## What is Groq API?

Groq provides fast, free AI inference. In Stickonomics, Groq generates sarcastic, witty verdicts about your economic situation based on your LPG predictor results.

**Example verdict from Groq:**

> "Your chances are proudly sponsored by inflation and wishful thinking. The government's blessing is reserved for those with better connections."

## Getting Started (2 Minutes) - COMPLETELY FREE! 🎉

### Step 1: Create Groq Account

Visit https://console.groq.com/ and sign up with:

- Email address
- Password
- No payment method required! It's completely free.

### Step 2: Verify Email

1. Check your email for verification link
2. Click the verification link
3. Log back into https://console.groq.com/

### Step 3: Generate API Key

1. In Groq console, go to **API Keys** (left sidebar)
2. Click **Create New API Key**
3. Copy the generated key (it starts with `gsk_`)
4. **Do not share this key!** It's like a password

### Step 4: Add to Stickonomics

1. Go to your Stickonomics project folder
2. Open `backend/.env`
3. Find this line:
   ```env
   GROQ_API_KEY=gsk_your_actual_api_key_here
   ```
4. Replace `gsk_your_actual_api_key_here` with your actual key
5. Save the file

**Example:**

```env
PORT=3001
GROQ_API_KEY=gsk_abcd1234xyz5678xyz9999
```

### Step 5: Test Setup

1. Start the backend:

   ```bash
   cd backend
   npm start
   ```

2. In another terminal, test the connection:

   ```bash
   curl -X POST http://localhost:3001/api/test-groq
   ```

3. You should see a response with a sarcastic verdict! 🎭

## Pricing - $0 COMPLETELY FREE

Groq offers:

- ✅ Free tier with generous rate limits (~30 requests/minute)
- ✅ No credit card required
- ✅ No surprise charges
- ✅ Unlimited free usage (within rate limits)
- ✅ No expiration date

Perfect for hobby projects like Stickonomics!

## Troubleshooting

### Issue: "Invalid API Key"

- ✅ Check `GROQ_API_KEY` is present in `.env`
- ✅ Make sure key starts with `gsk_`
- ✅ Try generating a new key at https://console.groq.com/

### Issue: "Rate limit exceeded"

- The free tier allows ~30 requests/minute
- Wait a minute before sending more requests
- Or upgrade to paid tier at https://console.groq.com/

### Issue: Network error

- Check internet connection
- Make sure backend is running (`npm start`)
- Run test endpoint: `curl http://localhost:3001/api/test-groq`

## What Happens Without Groq?

If Groq API is not configured, Stickonomics will:

1. Continue working perfectly
2. Use witty fallback verdicts
3. Never break or crash
4. Still show all predictor features

Example fallback verdict:

> "Better luck next life where you might be born in a fuel-rich family."

But the personalized Groq AI verdicts give a better experience! 🎭

## Advanced: Model Options

Stickonomics uses `mixtral-8x7b-32768` (fast and powerful). Visit https://console.groq.com/docs/models for other models.

To change the model:

1. Open `backend/index.js`
2. Find this line:
   ```javascript
   model: 'mixtral-8x7b-32768',  // Or use another Groq model
   ```
3. Replace with another model like `llama2-70b-4096`
4. Test with `curl -X POST http://localhost:3001/api/test-groq`

Popular Groq models:

- `mixtral-8x7b-32768` - Balanced, fast ⭐ (recommended)
- `llama2-70b-4096` - Powerful, slower
- `gemma-7b-it` - Lightweight, fastest

## Support

- Groq docs: https://console.groq.com/docs
- Issues? Check backend logs: `npm start`
- Or add `GROQ_API_KEY=fake_key` to test fallback mode

---

**That's it! You're ready to generate sarcastic AI verdicts for LPG cylinder predictions.** 🚀
