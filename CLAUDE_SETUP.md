# Claude AI Setup Guide for Stickonomics

## What is Claude AI?

Claude is an AI assistant made by Anthropic. In Stickonomics, Claude generates sarcastic, witty verdicts about your economic situation based on your LPG predictor results.

**Example verdict from Claude:**

> "Your chances are proudly sponsored by inflation and wishful thinking. The government's blessing is reserved for those with better connections."

## Getting Started (5 Minutes)

### Step 1: Create Anthropic Account

Visit https://console.anthropic.com/ and sign up with:

- Email address
- Password
- Phone number (for verification)

It's free to sign up. You'll need to add a payment method later.

### Step 2: Verify Email & Set Up Billing

1. Check your email for verification link
2. Click the verification link
3. Log back into https://console.anthropic.com/
4. Go to **Billing & Plans** (bottom left)
5. Add a payment method (credit/debit card)
6. Set a spending limit (optional but recommended, e.g., $10/month)

### Step 3: Generate API Key

1. In Anthropic console, click your profile icon (top right)
2. Select **API Keys**
3. Click **Create Key**
4. Copy the generated key (it starts with `sk-ant-`)
5. **Do not share this key!** It's like a password

### Step 4: Add to Stickonomics

1. Go to your Stickonomics project folder
2. Open `backend/.env`
3. Find this line:
   ```env
   CLAUDE_API_KEY=sk-ant-your_actual_api_key_here
   ```
4. Replace `sk-ant-your_actual_api_key_here` with your actual key
5. Save the file

Example:

```env
CLAUDE_API_KEY=sk-ant-abcd1234xyz5678xyz9999
```

### Step 5: Test It Works

```bash
# Start the backend
cd backend
npm start

# In another terminal, test:
curl -X POST http://localhost:3001/api/test-claude
```

If you see `"status": "success"`, you're good to go! 🎉

## Pricing

Claude AI is very affordable:

- **Haiku model** (used by Stickonomics): ~$0.0008 per 1K input tokens
- **Per verdict**: ~1 cent or less
- **Monthly**: ~$0.50 for 50 predictions

You can set a spending limit in Anthropic console to avoid surprises.

## Troubleshooting

### "401 Unauthorized" Error

- ❌ Key is wrong or expired
- ✅ Regenerate key in Anthropic console
- ✅ Make sure no extra spaces in `.env`

### "Connection failed"

- ❌ API key not set in `.env`
- ✅ Check `CLAUDE_API_KEY` is present
- ✅ Verify key starts with `sk-ant-`

### "Rate limit exceeded"

- ❌ Too many requests too fast
- ✅ Wait a few seconds and try again
- ✅ This rarely happens with normal usage

### It's still using fallback responses

- Check if your key is actually in `.env` (not commented out)
- Run test endpoint: `curl http://localhost:3001/api/test-claude`
- Check terminal logs for error messages

## What Happens Without Claude?

If Claude API is not configured, Stickonomics will:

- ✅ Still work perfectly
- ✅ Show witty fallback responses instead
- ✅ All features are available

Example fallback response:

> "Better luck next life where you might be born in a fuel-rich family."

But the personalized Claude AI verdicts give a better experience! 🎭

## Security Notes

- 🔒 Never commit `.env` file to git (add to `.gitignore`)
- 🔒 Don't share your API key with anyone
- 🔒 If exposed, regenerate immediately in Anthropic console
- 🔒 The key is only used server-side (safe)

## Advanced: Using Different Claude Models

Stickonomics uses `claude-3-haiku` (fastest & cheapest). You can change it:

In `backend/index.js`, change:

```javascript
model: 'claude-3-haiku-20240307',  // Fast & cheap
// to:
model: 'claude-3-sonnet-20240229',  // Better quality, more expensive
```

Available models:

- `claude-3-haiku` - Fastest, cheapest (~$0.008/1M tokens)
- `claude-3-sonnet` - Balanced (~$0.003/1M tokens input)
- `claude-3-opus` - Best quality (~$0.015/1M tokens)

## Next Steps

1. ✅ Add API key to `.env`
2. ✅ Test with `/api/test-claude`
3. ✅ Run both servers (`npm run dev` for frontend, `npm start` for backend)
4. ✅ Try the predictor - it should show Claude verdicts now!

---

**Need help?**

- Check Anthropic docs: https://docs.anthropic.com/
- Test endpoint: `curl http://localhost:3001/api/test-claude`
- Backend logs: Watch the terminal where backend is running
