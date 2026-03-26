A satirical Indian LPG cylinder predictor and stick economy simulator. Built with React + Vite on the frontend and Node.js + Express on the backend. 4. Done! No payment required ever. 5. Test: `curl http://localhost:3001/api/test-groq`

Without Groq API key, the app uses witty fallback responses!

### Backend Setup

```bash
cd backend

# Install dependencies
npm install

# Copy example env file
cp .env.example .env

# Edit .env with your Groq API key and optional Firebase config
# GROQ_API_KEY=gsk_your_key_here

# Start server
npm start

# Backend runs at http://localhost:3001
```

## 📝 How It Works

### Integration Points

1. **Verdict Generation**: Frontend calls `POST /api/verdict` after calculating probability
2. **Data Persistence**: Results automatically saved to `POST /api/save-result`
3. **Global Stats**: Frontend fetches `GET /api/stats` on load and after each result
4. **Error Handling**: Graceful fallbacks if backend is unavailable

### Frontend (React + Vite)

- Real-time balance calculations as sliders move
- Dynamic stick figure and UI colors based on mental stability
- Async verdict fetching with loading state
- Automatic stats refresh after predictions

### Backend (Node.js + Express)

- Groq API integration for sarcastic verdicts
- Firebase Firestore for optional data persistence
- CORS enabled for frontend communication
- Fallback responses when APIs are unavailable

## 🔌 API Endpoints

### POST /api/verdict

```
curl -X POST http://localhost:3001/api/verdict \
  -H "Content-Type: application/json" \
  -d '{"income":50,"usage":75,"political":"common","festival":"yes","mode":"reality","prob":42}'
```

### POST /api/save-result

```
curl -X POST http://localhost:3001/api/save-result \
  -H "Content-Type: application/json" \
  -d '{"result":{...},"userData":{...}}'
```

### GET /api/stats

```
curl http://localhost:3001/api/stats
```

## 🛠️ Tech Stack

**Frontend**: React 18 + TypeScript + Vite + Axios  
**Backend**: Express.js + Firebase Admin SDK + Axios  
**External**: Groq API (mixtral-8x7b-32768) + Firebase Firestore (optional)

The React Compiler is not enabled on this template because of its impact on dev & build performances. To add it, see [this documentation](https://react.dev/learn/react-compiler/installation).

## Expanding the ESLint configuration

If you are developing a production application, we recommend updating the configuration to enable type-aware lint rules:

```js
export default defineConfig([
  globalIgnores(["dist"]),
  {
    files: ["**/*.{ts,tsx}"],
    extends: [
      // Other configs...

      // Remove tseslint.configs.recommended and replace with this
      tseslint.configs.recommendedTypeChecked,
      // Alternatively, use this for stricter rules
      tseslint.configs.strictTypeChecked,
      // Optionally, add this for stylistic rules
      tseslint.configs.stylisticTypeChecked,

      // Other configs...
    ],
    languageOptions: {
      parserOptions: {
        project: ["./tsconfig.node.json", "./tsconfig.app.json"],
        tsconfigRootDir: import.meta.dirname,
      },
      // other options...
    },
  },
]);
```

You can also install [eslint-plugin-react-x](https://github.com/Rel1cx/eslint-react/tree/main/packages/plugins/eslint-plugin-react-x) and [eslint-plugin-react-dom](https://github.com/Rel1cx/eslint-react/tree/main/packages/plugins/eslint-plugin-react-dom) for React-specific lint rules:

```js
// eslint.config.js
import reactX from "eslint-plugin-react-x";
import reactDom from "eslint-plugin-react-dom";

export default defineConfig([
  globalIgnores(["dist"]),
  {
    files: ["**/*.{ts,tsx}"],
    extends: [
      // Other configs...
      // Enable lint rules for React
      reactX.configs["recommended-typescript"],
      // Enable lint rules for React DOM
      reactDom.configs.recommended,
    ],
    languageOptions: {
      parserOptions: {
        project: ["./tsconfig.node.json", "./tsconfig.app.json"],
        tsconfigRootDir: import.meta.dirname,
      },
      // other options...
    },
  },
]);
```
