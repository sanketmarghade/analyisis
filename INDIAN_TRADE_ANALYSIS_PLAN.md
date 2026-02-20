# INDIAN TRADE ANALYSIS - PROJECT PLAN
## TypeScript-Based Technical Analysis Platform for NSE

---

## 1. PROJECT OVERVIEW

**Project Name:** Indian Trade Analysis  
**Type:** Web Application (React + TypeScript)  
**Target:** NSE (National Stock Exchange of India)  
**Features:** Real-time Technical Analysis, AI/ML Predictions, Interactive Charts

---

## 2. TECH STACK

### Frontend
- **Framework:** React 18+ with TypeScript
- **State Management:** Redux Toolkit / Zustand
- **UI Library:** Material-UI (MUI) or Tailwind CSS
- **Charts:** Lightweight Charts (TradingView) or Recharts
- **Routing:** React Router v6

### Backend (Optional/Integration)
- **API:** Node.js + Express + TypeScript
- **Data Sources:** 
  - NSE Official API (nseindia.com)
  - Yahoo Finance API
  - Alpha Vantage
  - Websocket for real-time data

### AI/ML Components
- **TensorFlow.js** (browser-based predictions)
- **Python Integration** (optional for heavy ML)
- **Indicators Library:** Tulip Indicators or TA-Lib wrappers

### Database (Optional)
- PostgreSQL / MongoDB for historical data caching
- Redis for real-time data

---

## 3. PROJECT STRUCTURE

```
indian-trade-analysis/
├── public/
│   ├── index.html
│   └── assets/
│       └── logo.png
├── src/
│   ├── components/
│   │   ├── common/
│   │   │   ├── Button.tsx
│   │   │   ├── Input.tsx
│   │   │   ├── Dropdown.tsx
│   │   │   ├── Card.tsx
│   │   │   └── LoadingSpinner.tsx
│   │   ├── charts/
│   │   │   ├── CandlestickChart.tsx
│   │   │   ├── IndicatorOverlay.tsx
│   │   │   ├── VolumeChart.tsx
│   │   │   └── ChartControls.tsx
│   │   └── indicators/
│   │       ├── RSIDisplay.tsx
│   │       ├── MACDDisplay.tsx
│   │       ├── MovingAverages.tsx
│   │       └── BollingerBands.tsx
│   ├── screens/
│   │   ├── SplashScreen.tsx
│   │   ├── HomeScreen.tsx
│   │   ├── LoadingScreen.tsx
│   │   ├── ResultScreen.tsx
│   │   └── ChartScreen.tsx
│   ├── hooks/
│   │   ├── useStockData.ts
│   │   ├── useTechnicalIndicators.ts
│   │   ├── useAIPredictions.ts
│   │   └── useChartData.ts
│   ├── services/
│   │   ├── api/
│   │   │   ├── nseApi.ts
│   │   │   └── yahooFinance.ts
│   │   ├── indicators/
│   │   │   ├── calculateRSI.ts
│   │   │   ├── calculateMACD.ts
│   │   │   ├── calculateSMA.ts
│   │   │   ├── calculateEMA.ts
│   │   │   └── calculateBollingerBands.ts
│   │   └── ai/
│   │       ├── predictionModel.ts
│   │       ├── patternRecognition.ts
│   │       └── sentimentAnalysis.ts
│   ├── store/
│   │   ├── index.ts
│   │   ├── slices/
│   │   │   ├── stockSlice.ts
│   │   │   ├── chartSlice.ts
│   │   │   └── analysisSlice.ts
│   │   └── thunks/
│   │       └── fetchStockData.ts
│   ├── types/
│   │   ├── stock.ts
│   │   ├── indicators.ts
│   │   ├── chart.ts
│   │   └── api.ts
│   ├── utils/
│   │   ├── formatters.ts
│   │   ├── validators.ts
│   │   ├── constants.ts
│   │   └── helpers.ts
│   ├── styles/
│   │   ├── theme.ts
│   │   ├── global.css
│   │   └── components/
│   ├── App.tsx
│   ├── index.tsx
│   └── routes.tsx
├── ml-models/
│   ├── models/
│   │   ├── lstm-model.json
│   │   └── pattern-model.json
│   ├── training/
│   │   └── train-model.py
│   └── predictions/
│       └── predict.ts
├── package.json
├── tsconfig.json
├── tailwind.config.js
└── README.md
```

---

## 4. SCREEN DESIGNS

### 4.1 SPLASH SCREEN
**Purpose:** Initial loading and brand introduction
**Duration:** 2-3 seconds
**Elements:**
- Animated logo
- App name with tagline
- Loading progress bar
- Background: Gradient (Blue/Orange - Indian theme)

```typescript
interface SplashScreenProps {
  onComplete: () => void;
}
```

### 4.2 HOME SCREEN
**Purpose:** Main entry point for stock symbol input
**Layout:**
```
┌─────────────────────────────────────┐
│  HEADER: Logo + Navigation          │
├─────────────────────────────────────┤
│                                     │
│     [SEARCH SYMBOL INPUT BOX]       │
│     (Auto-complete with NSE list)   │
│                                     │
│     [INTERVAL DROPDOWN]             │
│     - 1 Minute                      │
│     - 5 Minutes                     │
│     - 15 Minutes                    │
│     - 30 Minutes                    │
│     - 1 Hour                        │
│     - 1 Day                         │
│     - 1 Week                        │
│     - 1 Month                       │
│                                     │
│     [ANALYZE BUTTON]                │
│                                     │
├─────────────────────────────────────┤
│  POPULAR SYMBOLS (Quick Select)     │
│  [RELIANCE] [TCS] [INFY] [HDFC]     │
└─────────────────────────────────────┘
```

**Components:**
- SymbolInput: Search with autocomplete
- IntervalSelector: Dropdown
- PopularSymbols: Quick access grid
- RecentSearches: History display

### 4.3 LOADING SCREEN
**Purpose:** Show analysis progress
**Elements:**
- Animated loading indicator
- Progress steps:
  1. Fetching market data...
  2. Calculating technical indicators...
  3. Running AI analysis...
  4. Generating insights...
- Estimated time remaining
- Cancel button

### 4.4 RESULT SCREEN
**Purpose:** Display analysis summary and indicators
**Layout:**
```
┌─────────────────────────────────────┐
│  SYMBOL: RELIANCE | Interval: 1D    │
├─────────────────────────────────────┤
│  ┌─────────────┐  ┌───────────────┐ │
│  │   SUMMARY   │  │ PRICE METRICS │ │
│  │             │  │               │ │
│  │ Signal: BUY │  │ Current: 2450 │ │
│  │ Confidence  │  │ Change: +2.5% │ │
│  │    85%      │  │ Volume: 5.2M  │ │
│  └─────────────┘  └───────────────┘ │
├─────────────────────────────────────┤
│  TECHNICAL INDICATORS GRID          │
│  ┌─────────┬─────────┬─────────┐   │
│  │  RSI    │  MACD   │  SMA    │   │
│  │  65.4   │ Bullish │  2420   │   │
│  │ Neutral │ Signal  │ Support │   │
│  ├─────────┼─────────┼─────────┤   │
│  │  EMA    │Bollinger│ Volume  │   │
│  │  2440   │  Bands  │  High   │   │
│  │  Trend  │ Squeeze │  Above  │   │
│  └─────────┴─────────┴─────────┘   │
├─────────────────────────────────────┤
│  AI INSIGHTS                        │
│  • Pattern detected: Cup & Handle   │
│  • Sentiment: Positive              │
│  • Prediction: Upward momentum      │
├─────────────────────────────────────┤
│  [VIEW CHART] [EXPORT] [SHARE]      │
└─────────────────────────────────────┘
```

**Components:**
- SummaryCard: Buy/Sell/Hold signal with confidence
- IndicatorCard: Individual indicator display
- AIInsightsPanel: ML-generated insights
- PriceMetrics: Current price, change, volume

### 4.5 CHART SCREEN
**Purpose:** Interactive technical chart with indicators
**Layout:**
```
┌─────────────────────────────────────┐
│  TOOLBAR: [Indicators] [Timeframe]  │
├─────────────────────────────────────┤
│                                     │
│         CANDLESTICK CHART           │
│    ┌─────────────────────────┐      │
│    │                         │      │
│    │   ═══════════════════   │      │
│    │      ┌───┐  ┌───┐       │      │
│    │      │   │  │   │       │      │
│    │      └───┘  └───┘       │      │
│    │   ═══════════════════   │      │
│    │         \/              │      │
│    │                         │      │
│    └─────────────────────────┘      │
│                                     │
│  OVERLAYS:                          │
│  ☑ SMA (20,50)  ☑ EMA (12,26)      │
│  ☑ Bollinger Bands  ☑ VWAP         │
│                                     │
├─────────────────────────────────────┤
│  INDICATOR PANELS (Bottom)          │
│  ┌─────────────────────────────┐    │
│  │ RSI (0-100)     [====65===] │    │
│  │ Overbought:70  Oversold:30  │    │
│  ├─────────────────────────────┤    │
│  │ MACD                        │    │
│  │ Histogram | Signal | Line   │    │
│  ├─────────────────────────────┤    │
│  │ VOLUME     ████████░░░░░░   │    │
│  └─────────────────────────────┘    │
├─────────────────────────────────────┤
│  [ZOOM] [PAN] [RESET] [FULLSCREEN]  │
└─────────────────────────────────────┘
```

**Chart Features:**
- Candlestick/OHLC display
- Multiple timeframe support
- Drawing tools (trendlines, Fibonacci)
- Crosshair with price/volume info
- Zoom and pan functionality
- Screenshot/Export

---

## 5. TECHNICAL INDICATORS

### 5.1 Trend Indicators
- **SMA (Simple Moving Average):** 20, 50, 100, 200 periods
- **EMA (Exponential Moving Average):** 12, 26 periods
- **VWAP (Volume Weighted Average Price)**
- **Ichimoku Cloud**

### 5.2 Momentum Indicators
- **RSI (Relative Strength Index):** 14-period
- **MACD (Moving Average Convergence Divergence)**
- **Stochastic Oscillator**
- **CCI (Commodity Channel Index)**

### 5.3 Volatility Indicators
- **Bollinger Bands:** 20-period, 2 std dev
- **ATR (Average True Range)**
- **Keltner Channels**
- **Donchian Channels**
- **Standard Deviation**

### 5.4 Volume Indicators
- **Volume Profile**
- **OBV (On Balance Volume)**
- **Volume Rate of Change**
- **Accumulation/Distribution Line (A/D)**
- **Chaikin Money Flow (CMF)**
- **VWAP (Volume Weighted Average Price)** - Anchored & Rolling

### 5.5 Momentum Indicators (Extended)
- **Stochastic RSI**
- **Williams %R**
- **Ultimate Oscillator**
- **MFI (Money Flow Index)**
- **PPO (Percentage Price Oscillator)**

### 5.6 Trend Indicators (Extended)
- **ADX (Average Directional Index)**
- **Parabolic SAR**
- **Supertrend**
- **Aroon Indicator**

### 5.7 Market Breadth (Index Analysis)
- **Advance/Decline Line**
- **TRIN (Arms Index)**
- **McClellan Oscillator**

---

## 5A. ADVANCED TECHNICAL CONCEPTS

### 5A.1 Price Action
- **Supply & Demand Zones:** Automated detection of unmitigated zones
- **Pivot Points:** Standard, Fibonacci, Camarilla, Woodie
- **Gap Analysis:** Identification of Common, Breakaway, Runaway, and Exhaustion gaps
- **Market Structure:** HH/HL (Higher Highs/Lows) and LH/LL detection

### 5A.2 Fibonacci Analysis
- **Retracements:** Auto-levels (0.236, 0.382, 0.5, 0.618, 0.786)
- **Extensions:** price targets (1.272, 1.618, 2.618)
- **Fans & Arcs:** Trend following tools
- **Time Zones:** Time-based reversal prediction

### 5A.3 Harmonic Patterns (Auto-Detection)
- **Gartley Pattern**
- **Bat Pattern**
- **Butterfly Pattern**
- **Crab Pattern**
- **Cypher Pattern**
- **Shark Pattern**

### 5A.4 Derivative & Market Data Analysis
- **Option Chain Analytics:**
  - PCR (Put-Call Ratio) Tracking
  - Max Pain Calculation
  - Open Interest (OI) Buildup/Unwinding interpretation
- **FII/DII Activity:** Net flow analysis & correlation with NIFTY
- **Delivery Percentage:** High delivery volume breakouts

### 5A.5 Divergence Analysis
- **Regular Divergence:** Trend reversal signal (Price vs RSI/MACD)
- **Hidden Divergence:** Trend continuation signal

### 5A.6 Multi-Timeframe Analysis
- **Trend Alignment:** Checking trend across 3 timeframes (e.g., Daily, 1H, 15m)
- **Signal Confirmation:** Entry on lower timeframe aligned with higher timeframe trend

---

## 6. AI/ML COMPONENTS

### 6.1 Pattern Recognition
- **Candlestick Patterns:** Doji, Hammer, Engulfing, Morning Star, etc.
- **Chart Patterns:** Head & Shoulders, Triangles, Flags, Cup & Handle
- **Neural Network:** CNN for pattern detection

### 6.2 Price Prediction
- **LSTM Model:** Time-series forecasting
- **Features:** OHLCV + Technical Indicators
- **Prediction Horizon:** Next 5, 10, 20 candles

### 6.3 Sentiment Analysis
- **News Integration:** Parse financial news
- **Social Media:** Twitter/Reddit sentiment
- **NLP Model:** BERT-based classifier

### 6.4 Signal Generation
- **Ensemble Model:** Combine multiple indicators
- **Risk Score:** Volatility and trend strength
- **Recommendation Engine:** Buy/Sell/Hold with confidence

---

## 7. DATA FLOW

```
┌──────────────┐
│  User Input  │
│ Symbol + TF  │
└──────┬───────┘
       │
       ▼
┌──────────────┐     ┌──────────────┐
│   API Call   │────▶│  NSE/Yahoo   │
│  Fetch Data  │     │    API       │
└──────┬───────┘     └──────────────┘
       │
       ▼
┌──────────────┐
│  Raw Data    │
│  OHLCV       │
└──────┬───────┘
       │
       ▼
┌──────────────┐     ┌──────────────┐
│ Calculate    │────▶│  Technical   │
│ Indicators   │     │  Indicators  │
└──────┬───────┘     └──────────────┘
       │
       ▼
┌──────────────┐     ┌──────────────┐
│  AI/ML       │────▶│  Prediction  │
│  Analysis    │     │  Model       │
└──────┬───────┘     └──────────────┘
       │
       ▼
┌──────────────┐
│  Generate    │
│  Results     │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│   Display    │
│  Screens     │
└──────────────┘
```

---

## 8. KEY FEATURES

### 8.1 Real-Time Data
- WebSocket connection for live prices
- Auto-refresh intervals
- Price alerts and notifications

### 8.2 Historical Analysis
- Backtesting capabilities
- Historical pattern search
- Performance metrics

### 8.3 Watchlist & Portfolio
- Custom watchlists
- Portfolio tracking
- P&L calculations

### 8.4 Export & Sharing
- PDF report generation
- Chart image export
- Social media sharing

---

## 9. IMPLEMENTATION PHASES

### Phase 1: Core Foundation (Week 1-2)
- [ ] Project setup with TypeScript + React
- [ ] Basic routing and navigation
- [ ] Splash screen implementation
- [ ] Home screen with input components
- [ ] API integration for NSE data

### Phase 2: Data & Charts (Week 3-4)
- [ ] Loading screen with progress
- [ ] Chart library integration
- [ ] Candlestick chart display
- [ ] Timeframe switching
- [ ] Basic zoom and pan

### Phase 3: Indicators (Week 5-6)
- [ ] Calculate SMA, EMA
- [ ] RSI implementation
- [ ] MACD calculation
- [ ] Bollinger Bands
- [ ] Volume indicators
- [ ] Chart overlay system

### Phase 4: AI/ML Integration (Week 7-8)
- [ ] TensorFlow.js setup
- [ ] Pattern recognition model
- [ ] Price prediction LSTM
- [ ] Sentiment analysis
- [ ] Signal generation engine

### Phase 5: Result Screen (Week 9)
- [ ] Summary cards
- [ ] Indicator grid layout
- [ ] AI insights panel
- [ ] Export functionality

### Phase 6: Polish & Optimization (Week 10)
- [ ] Responsive design
- [ ] Performance optimization
- [ ] Error handling
- [ ] Testing and debugging
- [ ] Documentation

---

## 10. TECHNICAL REQUIREMENTS

### 10.1 NPM Packages
```json
{
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-router-dom": "^6.8.0",
    "typescript": "^5.0.0",
    "lightweight-charts": "^4.0.0",
    "@reduxjs/toolkit": "^1.9.0",
    "react-redux": "^8.0.0",
    "axios": "^1.3.0",
    "@tensorflow/tfjs": "^4.0.0",
    "technicalindicators": "^3.1.0",
    "date-fns": "^2.29.0",
    "@mui/material": "^5.11.0",
    "recharts": "^2.5.0",
    "framer-motion": "^10.0.0",
    "react-query": "^3.39.0"
  }
}
```

### 10.2 API Endpoints (Sample)
```typescript
// NSE API
GET /api/equity-stockIndices?index=NIFTY%2050
GET /api/historical/cm/equity?symbol=RELIANCE&series=EQ
GET /api/quote-equity?symbol=RELIANCE

// Custom Backend
GET /api/analysis/:symbol/:interval
POST /api/predict
GET /api/indicators/:symbol
```

---

## 11. TYPE DEFINITIONS

```typescript
// types/stock.ts
export interface StockData {
  symbol: string;
  open: number;
  high: number;
  low: number;
  close: number;
  volume: number;
  timestamp: Date;
}

export interface TechnicalIndicators {
  sma20: number[];
  sma50: number[];
  ema12: number[];
  ema26: number[];
  rsi: number[];
  macd: MACDResult;
  bollingerBands: BollingerResult;
  atr: number[];
}

export interface AnalysisResult {
  symbol: string;
  interval: string;
  signal: 'BUY' | 'SELL' | 'HOLD' | 'NEUTRAL';
  confidence: number;
  indicators: TechnicalIndicators;
  aiInsights: AIInsight[];
  priceMetrics: PriceMetrics;
}

export interface AIInsight {
  type: 'pattern' | 'prediction' | 'sentiment';
  title: string;
  description: string;
  confidence: number;
}
```

---

## 12. SECURITY & PERFORMANCE

### Security
- API key management
- Rate limiting
- Input validation
- HTTPS enforcement

### Performance
- Data caching (React Query)
- Lazy loading for charts
- Virtualization for large datasets
- Web Workers for ML computations
- Image optimization

---

## 13. FUTURE ENHANCEMENTS

- [ ] Multi-language support (Hindi, English)
- [ ] Mobile app (React Native)
- [ ] Real-time notifications
- [ ] Paper trading integration
- [ ] Options analysis
- [ ] Mutual fund analysis
- [ ] IPO tracking
- [ ] Economic calendar
- [ ] Broker integration

---

## 14. RESOURCES

### Data Sources
- NSE India: https://www.nseindia.com
- Yahoo Finance API
- Alpha Vantage: https://www.alphavantage.co

### Libraries
- Lightweight Charts: https://tradingview.github.io/lightweight-charts/
- TensorFlow.js: https://www.tensorflow.org/js
- Technical Indicators: https://github.com/anandanand84/technicalindicators

### Learning Resources
- Technical Analysis: Investopedia
- ML for Trading: QuantStart
- NSE API Docs

---

## 15. ADDITIONAL SCREENS & FEATURES

### 15.1 SCANNER SCREEN
**Purpose:** Find stocks matching technical criteria
**Layout:**
```
┌─────────────────────────────────────┐
│  STOCK SCANNER                      │
├─────────────────────────────────────┤
│  FILTERS:                           │
│  [Price Range] [Volume >] [RSI 0-100]│
│                                     │
│  PATTERN FILTERS:                   │
│  ☑ Breakout    ☑ Support Touch     │
│  ☑ Volume Spike ☑ Golden Cross     │
│                                     │
│  [RUN SCAN]                         │
├─────────────────────────────────────┤
│  RESULTS (50 stocks found)          │
│  ┌─────────┬───────┬────────┬─────┐ │
│  │ Symbol  │ Price │ Change │ RSI │ │
│  ├─────────┼───────┼────────┼─────┤ │
│  │ RELIANCE│ 2450  │ +2.5%  │ 65  │ │
│  │ TCS     │ 3450  │ +1.2%  │ 58  │ │
│  │ INFY    │ 1420  │ -0.8%  │ 42  │ │
│  └─────────┴───────┴────────┴─────┘ │
└─────────────────────────────────────┘
```

### 15.2 PORTFOLIO SCREEN
**Purpose:** Track user's stock holdings
**Features:**
- Add/edit/delete holdings
- Real-time P&L calculation
- Portfolio allocation pie chart
- Sector-wise distribution
- Performance vs NIFTY benchmark

### 15.3 ALERTS SCREEN
**Purpose:** Set price and indicator alerts
**Alert Types:**
- Price crosses above/below
- RSI overbought/oversold
- Volume spike
- Pattern detection
- MACD crossover

### 15.4 MARKET OVERVIEW SCREEN
**Purpose:** Overall market sentiment
**Widgets:**
- NIFTY 50 & SENSEX live tickers
- Sectoral indices heatmap
- Top gainers/losers
- Market breadth (advance/decline)
- FII/DII activity

### 15.5 BACKTESTING SCREEN
**Purpose:** Test trading strategies
**Features:**
- Strategy builder (visual)
- Historical data range selection
- Performance metrics:
  - Win rate
  - Profit factor
  - Max drawdown
  - Sharpe ratio
  - Total returns
- Equity curve chart
- Trade log table

### 15.6 PAPER TRADING SCREEN
**Purpose:** Practice trading without real money
**Features:**
- Virtual wallet (₹10,00,000)
- Buy/sell orders
- Order history
- Position tracking
- Real-time P&L
- Leaderboard (optional)

### 15.7 SETTINGS SCREEN
**Purpose:** User preferences
**Options:**
- Theme (Light/Dark/Auto)
- Default chart interval
- Notification preferences
- API key management
- Data export
- Language selection
- Account management

---

## 16. EXPANDED PROJECT STRUCTURE

```
indian-trade-analysis/
├── public/
│   ├── index.html
│   ├── manifest.json
│   ├── robots.txt
│   └── assets/
│       ├── logo.png
│       ├── logo-dark.png
│       ├── favicon.ico
│       └── icons/
│           ├── icon-72x72.png
│           ├── icon-96x96.png
│           ├── icon-128x128.png
│           ├── icon-144x144.png
│           ├── icon-152x152.png
│           ├── icon-192x192.png
│           ├── icon-384x384.png
│           └── icon-512x512.png
├── src/
│   ├── components/
│   │   ├── common/
│   │   │   ├── Button/
│   │   │   │   ├── Button.tsx
│   │   │   │   ├── Button.test.tsx
│   │   │   │   └── Button.styles.ts
│   │   │   ├── Input/
│   │   │   │   ├── SymbolInput.tsx
│   │   │   │   ├── NumberInput.tsx
│   │   │   │   └── SearchInput.tsx
│   │   │   ├── Dropdown/
│   │   │   │   ├── IntervalDropdown.tsx
│   │   │   │   └── MultiSelect.tsx
│   │   │   ├── Card/
│   │   │   │   ├── MetricCard.tsx
│   │   │   │   └── IndicatorCard.tsx
│   │   │   ├── Table/
│   │   │   │   ├── DataTable.tsx
│   │   │   │   └── SortableTable.tsx
│   │   │   ├── Modal/
│   │   │   │   ├── AlertModal.tsx
│   │   │   │   └── ConfirmModal.tsx
│   │   │   ├── Loading/
│   │   │   │   ├── Spinner.tsx
│   │   │   │   ├── Skeleton.tsx
│   │   │   │   └── ProgressBar.tsx
│   │   │   ├── Toast/
│   │   │   │   └── ToastNotification.tsx
│   │   │   └── Error/
│   │   │       ├── ErrorBoundary.tsx
│   │   │       └── ErrorMessage.tsx
│   │   ├── layout/
│   │   │   ├── Header.tsx
│   │   │   ├── Sidebar.tsx
│   │   │   ├── Footer.tsx
│   │   │   ├── Navigation.tsx
│   │   │   └── Layout.tsx
│   │   ├── charts/
│   │   │   ├── CandlestickChart/
│   │   │   │   ├── CandlestickChart.tsx
│   │   │   │   ├── ChartTooltip.tsx
│   │   │   │   └── ChartLegend.tsx
│   │   │   ├── overlays/
│   │   │   │   ├── SMAOverlay.tsx
│   │   │   │   ├── EMAOverlay.tsx
│   │   │   │   ├── BollingerOverlay.tsx
│   │   │   │   ├── VWAPOverlay.tsx
│   │   │   │   └── PivotPointsOverlay.tsx
│   │   │   ├── panels/
│   │   │   │   ├── RSIPanel.tsx
│   │   │   │   ├── MACDPanel.tsx
│   │   │   │   ├── VolumePanel.tsx
│   │   │   │   ├── StochasticPanel.tsx
│   │   │   │   └── ATRPanel.tsx
│   │   │   ├── drawing/
│   │   │   │   ├── TrendLineTool.tsx
│   │   │   │   ├── FibonacciTool.tsx
│   │   │   │   ├── RectangleTool.tsx
│   │   │   │   └── TextTool.tsx
│   │   │   └── controls/
│   │   │       ├── TimeframeSelector.tsx
│   │   │       ├── ChartTypeSelector.tsx
│   │   │       ├── IndicatorToggle.tsx
│   │   │       └── ZoomControls.tsx
│   │   ├── indicators/
│   │   │   ├── TrendIndicators/
│   │   │   │   ├── SMA.tsx
│   │   │   │   ├── EMA.tsx
│   │   │   │   ├── VWAP.tsx
│   │   │   │   └── Ichimoku.tsx
│   │   │   ├── MomentumIndicators/
│   │   │   │   ├── RSI.tsx
│   │   │   │   ├── MACD.tsx
│   │   │   │   ├── Stochastic.tsx
│   │   │   │   ├── CCI.tsx
│   │   │   │   └── WilliamsR.tsx
│   │   │   ├── VolatilityIndicators/
│   │   │   │   ├── BollingerBands.tsx
│   │   │   │   ├── ATR.tsx
│   │   │   │   └── KeltnerChannels.tsx
│   │   │   ├── VolumeIndicators/
│   │   │   │   ├── VolumeProfile.tsx
│   │   │   │   ├── OBV.tsx
│   │   │   │   ├── MFI.tsx
│   │   │   │   └── VolumeROC.tsx
│   │   │   └── Display/
│   │   │       ├── IndicatorCard.tsx
│   │   │       ├── IndicatorGrid.tsx
│   │   │       └── IndicatorDetail.tsx
│   │   ├── scanner/
│   │   │   ├── FilterPanel.tsx
│   │   │   ├── ScanResults.tsx
│   │   │   ├── ScanBuilder.tsx
│   │   │   └── SavedScans.tsx
│   │   ├── portfolio/
│   │   │   ├── HoldingsList.tsx
│   │   │   ├── PortfolioSummary.tsx
│   │   │   ├── AllocationChart.tsx
│   │   │   ├── AddPositionModal.tsx
│   │   │   └── PerformanceChart.tsx
│   │   ├── alerts/
│   │   │   ├── AlertList.tsx
│   │   │   ├── CreateAlert.tsx
│   │   │   ├── AlertHistory.tsx
│   │   │   └── NotificationSettings.tsx
│   │   └── ai/
│   │       ├── PredictionCard.tsx
│   │       ├── PatternMatch.tsx
│   │       ├── SentimentGauge.tsx
│   │       ├── ConfidenceMeter.tsx
│   │       └── ModelExplanation.tsx
│   ├── screens/
│   │   ├── Splash/
│   │   │   ├── SplashScreen.tsx
│   │   │   └── SplashScreen.test.tsx
│   │   ├── Home/
│   │   │   ├── HomeScreen.tsx
│   │   │   ├── HeroSection.tsx
│   │   │   ├── QuickSearch.tsx
│   │   │   ├── MarketTicker.tsx
│   │   │   └── RecentAnalysis.tsx
│   │   ├── Loading/
│   │   │   ├── LoadingScreen.tsx
│   │   │   ├── ProgressSteps.tsx
│   │   │   └── AnalysisStage.tsx
│   │   ├── Result/
│   │   │   ├── ResultScreen.tsx
│   │   │   ├── SummarySection.tsx
│   │   │   ├── IndicatorsSection.tsx
│   │   │   ├── AIInsightsSection.tsx
│   │   │   ├── PriceActionSection.tsx
│   │   │   └── ExportOptions.tsx
│   │   ├── Chart/
│   │   │   ├── ChartScreen.tsx
│   │   │   ├── ChartContainer.tsx
│   │   │   ├── IndicatorSidebar.tsx
│   │   │   ├── DrawingToolbar.tsx
│   │   │   └── ChartSettings.tsx
│   │   ├── Scanner/
│   │   │   ├── ScannerScreen.tsx
│   │   │   ├── FilterBuilder.tsx
│   │   │   └── ScanResults.tsx
│   │   ├── Portfolio/
│   │   │   ├── PortfolioScreen.tsx
│   │   │   ├── HoldingsTab.tsx
│   │   │   ├── PerformanceTab.tsx
│   │   │   └── TransactionsTab.tsx
│   │   ├── Alerts/
│   │   │   ├── AlertsScreen.tsx
│   │   │   ├── ActiveAlerts.tsx
│   │   │   └── CreateAlertWizard.tsx
│   │   ├── Market/
│   │   │   ├── MarketOverviewScreen.tsx
│   │   │   ├── IndicesWidget.tsx
│   │   │   ├── Heatmap.tsx
│   │   │   ├── GainersLosers.tsx
│   │   │   └── MarketBreadth.tsx
│   │   ├── Backtest/
│   │   │   ├── BacktestScreen.tsx
│   │   │   ├── StrategyBuilder.tsx
│   │   │   ├── ResultsView.tsx
│   │   │   └── TradeLog.tsx
│   │   ├── PaperTrading/
│   │   │   ├── PaperTradingScreen.tsx
│   │   │   ├── VirtualPortfolio.tsx
│   │   │   ├── OrderPanel.tsx
│   │   │   └── OrderHistory.tsx
│   │   └── Settings/
│   │       ├── SettingsScreen.tsx
│   │       ├── AppearanceSettings.tsx
│   │       ├── NotificationSettings.tsx
│   │       ├── APISettings.tsx
│   │       └── AccountSettings.tsx
│   ├── hooks/
│   │   ├── useStockData.ts
│   │   ├── useTechnicalIndicators.ts
│   │   ├── useAIPredictions.ts
│   │   ├── useChartData.ts
│   │   ├── useWebSocket.ts
│   │   ├── useLocalStorage.ts
│   │   ├── useDebounce.ts
│   │   ├── usePagination.ts
│   │   ├── useScanner.ts
│   │   ├── usePortfolio.ts
│   │   ├── useAlerts.ts
│   │   ├── useTheme.ts
│   │   └── useMediaQuery.ts
│   ├── services/
│   │   ├── api/
│   │   │   ├── nseApi.ts
│   │   │   ├── yahooFinance.ts
│   │   │   ├── alphaVantage.ts
│   │   │   └── websocketService.ts
│   │   ├── indicators/
│   │   │   ├── trend/
│   │   │   │   ├── sma.ts
│   │   │   │   ├── ema.ts
│   │   │   │   ├── vwap.ts
│   │   │   │   ├── wma.ts
│   │   │   │   └── ichimoku.ts
│   │   │   ├── momentum/
│   │   │   │   ├── rsi.ts
│   │   │   │   ├── macd.ts
│   │   │   │   ├── stochastic.ts
│   │   │   │   ├── cci.ts
│   │   │   │   ├── williamsR.ts
│   │   │   │   └── momentum.ts
│   │   │   ├── volatility/
│   │   │   │   ├── bollingerBands.ts
│   │   │   │   ├── atr.ts
│   │   │   │   ├── keltnerChannels.ts
│   │   │   │   ├── standardDeviation.ts
│   │   │   │   └── donchianChannels.ts
│   │   │   ├── volume/
│   │   │   │   ├── obv.ts
│   │   │   │   ├── volumeProfile.ts
│   │   │   │   ├── mfi.ts
│   │   │   │   ├── volumeROC.ts
│   │   │   │   └── chaikinMoneyFlow.ts
│   │   │   └── index.ts
│   │   ├── ai/
│   │   │   ├── models/
│   │   │   │   ├── lstmModel.ts
│   │   │   │   ├── cnnPatternModel.ts
│   │   │   │   └── sentimentModel.ts
│   │   │   ├── training/
│   │   │   │   ├── dataPreparation.ts
│   │   │   │   ├── modelTraining.ts
│   │   │   │   └── modelEvaluation.ts
│   │   │   ├── predictions/
│   │   │   │   ├── pricePrediction.ts
│   │   │   │   ├── patternDetection.ts
│   │   │   │   └── trendForecasting.ts
│   │   │   ├── patterns/
│   │   │   │   ├── candlestickPatterns.ts
│   │   │   │   ├── chartPatterns.ts
│   │   │   │   └── harmonicPatterns.ts
│   │   │   └── sentiment/
│   │   │       ├── newsAnalysis.ts
│   │   │       ├── socialMediaAnalysis.ts
│   │   │       └── marketSentiment.ts
│   │   ├── scanner/
│   │   │   ├── filterEngine.ts
│   │   │   ├── scanExecutor.ts
│   │   │   └── resultsProcessor.ts
│   │   ├── portfolio/
│   │   │   ├── portfolioCalculator.ts
│   │   │   ├── performanceTracker.ts
│   │   │   └── dataSync.ts
│   │   └── export/
│   │       ├── pdfExport.ts
│   │       ├── csvExport.ts
│   │       ├── imageExport.ts
│   │       └── reportGenerator.ts
│   ├── store/
│   │   ├── index.ts
│   │   ├── slices/
│   │   │   ├── authSlice.ts
│   │   │   ├── stockSlice.ts
│   │   │   ├── chartSlice.ts
│   │   │   ├── analysisSlice.ts
│   │   │   ├── scannerSlice.ts
│   │   │   ├── portfolioSlice.ts
│   │   │   ├── alertsSlice.ts
│   │   │   ├── settingsSlice.ts
│   │   │   └── uiSlice.ts
│   │   ├── thunks/
│   │   │   ├── fetchStockData.ts
│   │   │   ├── runAnalysis.ts
│   │   │   ├── executeScan.ts
│   │   │   └── savePortfolio.ts
│   │   └── selectors/
│   │       ├── stockSelectors.ts
│   │       ├── chartSelectors.ts
│   │       └── analysisSelectors.ts
│   ├── types/
│   │   ├── stock.ts
│   │   ├── indicators.ts
│   │   ├── chart.ts
│   │   ├── api.ts
│   │   ├── ai.ts
│   │   ├── scanner.ts
│   │   ├── portfolio.ts
│   │   ├── alerts.ts
│   │   ├── user.ts
│   │   └── common.ts
│   ├── utils/
│   │   ├── formatters/
│   │   │   ├── priceFormatter.ts
│   │   │   ├── dateFormatter.ts
│   │   │   └── numberFormatter.ts
│   │   ├── validators/
│   │   │   ├── symbolValidator.ts
│   │   │   ├── inputValidator.ts
│   │   │   └── dataValidator.ts
│   │   ├── constants/
│   │   │   ├── intervals.ts
│   │   │   ├── indicators.ts
│   │   │   ├── nseSymbols.ts
│   │   │   ├── chartColors.ts
│   │   │   └── thresholds.ts
│   │   ├── helpers/
│   │   │   ├── calculations.ts
│   │   │   ├── dataTransformers.ts
│   │   │   ├── chartHelpers.ts
│   │   │   └── analysisHelpers.ts
│   │   └── errorHandlers/
│   │       ├── apiErrorHandler.ts
│   │       ├── chartErrorHandler.ts
│   │       └── generalErrorHandler.ts
│   ├── styles/
│   │   ├── theme.ts
│   │   ├── global.css
│   │   ├── variables.css
│   │   ├── animations.css
│   │   ├── responsive.css
│   │   └── components/
│   │       ├── button.styles.ts
│   │       ├── card.styles.ts
│   │       ├── chart.styles.ts
│   │       └── layout.styles.ts
│   ├── config/
│   │   ├── api.config.ts
│   │   ├── chart.config.ts
│   │   ├── ai.config.ts
│   │   ├── theme.config.ts
│   │   └── app.config.ts
│   ├── constants/
│   │   ├── routes.ts
│   │   ├── apiEndpoints.ts
│   │   ├── indicators.ts
│   │   ├── intervals.ts
│   │   └── messages.ts
│   ├── context/
│   │   ├── AuthContext.tsx
│   │   ├── ThemeContext.tsx
│   │   ├── WebSocketContext.tsx
│   │   └── ChartContext.tsx
│   ├── guards/
│   │   ├── AuthGuard.tsx
│   │   └── RoleGuard.tsx
│   ├── middleware/
│   │   ├── errorMiddleware.ts
│   │   ├── loggingMiddleware.ts
│   │   └── cacheMiddleware.ts
│   ├── tests/
│   │   ├── unit/
│   │   ├── integration/
│   │   ├── e2e/
│   │   └── mocks/
│   ├── App.tsx
│   ├── index.tsx
│   ├── routes.tsx
│   └── serviceWorker.ts
├── ml-models/
│   ├── models/
│   │   ├── lstm-price-prediction/
│   │   │   ├── model.json
│   │   │   ├── weights.bin
│   │   │   └── metadata.json
│   │   ├── cnn-pattern-recognition/
│   │   │   ├── model.json
│   │   │   ├── weights.bin
│   │   │   └── metadata.json
│   │   └── sentiment-analysis/
│   │       ├── model.json
│   │       ├── vocab.json
│   │       └── config.json
│   ├── training/
│   │   ├── data/
│   │   │   ├── raw/
│   │   │   ├── processed/
│   │   │   └── features/
│   │   ├── notebooks/
│   │   │   ├── lstm_training.ipynb
│   │   │   ├── cnn_training.ipynb
│   │   │   └── sentiment_training.ipynb
│   │   ├── scripts/
│   │   │   ├── prepare_data.py
│   │   │   ├── train_lstm.py
│   │   │   ├── train_cnn.py
│   │   │   ├── evaluate_models.py
│   │   │   └── convert_to_tfjs.py
│   │   └── config/
│   │       ├── model_config.yaml
│   │       └── training_config.yaml
│   └── predictions/
│       ├── pricePrediction.ts
│       ├── patternRecognition.ts
│       └── sentimentAnalysis.ts
├── database/
│   ├── migrations/
│   ├── seeds/
│   ├── schema.sql
│   └── models/
├── docs/
│   ├── api/
│   ├── architecture/
│   ├── deployment/
│   └── user-guide/
├── scripts/
│   ├── setup.sh
│   ├── build.sh
│   ├── test.sh
│   └── deploy.sh
├── .env.example
├── .env.development
├── .env.production
├── .eslintrc.json
├── .prettierrc
├── .gitignore
├── tsconfig.json
├── vite.config.ts
├── tailwind.config.js
├── postcss.config.js
├── jest.config.js
├── cypress.config.ts
├── package.json
└── README.md
```

---

## 17. COMPLETE TYPE DEFINITIONS

```typescript
// types/stock.ts
export interface OHLCV {
  timestamp: number;
  open: number;
  high: number;
  low: number;
  close: number;
  volume: number;
}

export interface StockQuote {
  symbol: string;
  name: string;
  exchange: string;
  sector: string;
  currentPrice: number;
  change: number;
  changePercent: number;
  open: number;
  high: number;
  low: number;
  close: number;
  volume: number;
  avgVolume: number;
  marketCap: number;
  peRatio: number;
  fiftyTwoWeekHigh: number;
  fiftyTwoWeekLow: number;
  lastUpdated: Date;
}

export interface HistoricalData {
  symbol: string;
  interval: string;
  data: OHLCV[];
  from: Date;
  to: Date;
}

export interface IntradayData extends OHLCV {
  symbol: string;
}

export interface MarketDepth {
  symbol: string;
  bids: Level2Data[];
  asks: Level2Data[];
}

export interface Level2Data {
  price: number;
  quantity: number;
  orders: number;
}

// types/indicators.ts
export interface IndicatorConfig {
  name: string;
  period: number;
  parameters: Record<string, number>;
  visible: boolean;
  color: string;
}

export interface IndicatorResult {
  name: string;
  values: number[];
  timestamps: number[];
  signals?: IndicatorSignal[];
}

export interface IndicatorSignal {
  timestamp: number;
  type: 'BUY' | 'SELL' | 'NEUTRAL';
  strength: number;
  message: string;
}

export interface RSIResult extends IndicatorResult {
  overbought: number;
  oversold: number;
  currentValue: number;
}

export interface MACDResult {
  macdLine: number[];
  signalLine: number[];
  histogram: number[];
  timestamps: number[];
  currentMACD: number;
  currentSignal: number;
  currentHistogram: number;
}

export interface BollingerResult {
  upper: number[];
  middle: number[];
  lower: number[];
  timestamps: number[];
  currentUpper: number;
  currentMiddle: number;
  currentLower: number;
  bandwidth: number;
  percentB: number;
}

export interface MovingAverageResult extends IndicatorResult {
  type: 'SMA' | 'EMA' | 'WMA';
  period: number;
}

export interface VolumeProfileResult {
  priceLevels: number[];
  volumes: number[];
  poc: number; // Point of Control
  valueAreaHigh: number;
  valueAreaLow: number;
}

export interface TechnicalIndicatorsSet {
  trend: {
    sma20: MovingAverageResult;
    sma50: MovingAverageResult;
    sma200: MovingAverageResult;
    ema12: MovingAverageResult;
    ema26: MovingAverageResult;
    vwap: IndicatorResult;
    adx: IndicatorResult;
    supertrend: IndicatorResult;
    parabolicSAR: IndicatorResult;
  };
  momentum: {
    rsi14: RSIResult;
    macd: MACDResult;
    stochastic: IndicatorResult;
    stochRSI: IndicatorResult;
    williamsR: IndicatorResult;
    cci: IndicatorResult;
    ultimate: IndicatorResult;
  };
  volatility: {
    bollinger: BollingerResult;
    atr14: IndicatorResult;
    keltner: IndicatorResult;
    donchian: IndicatorResult;
  };
  volume: {
    obv: IndicatorResult;
    mfi: IndicatorResult;
    volumeProfile: VolumeProfileResult;
    adLine: IndicatorResult;
    cmf: IndicatorResult;
  };
  breadth?: {
    advanceDecline: number;
    trin: number;
  };
}

export interface PivotPoints {
  classic: { r1: number; r2: number; r3: number; p: number; s1: number; s2: number; s3: number };
  fibonacci: { r1: number; r2: number; r3: number; p: number; s1: number; s2: number; s3: number };
  camarilla: { r3: number; r4: number; s3: number; s4: number };
}

export interface FibonacciLevels {
  retracements: Record<string, number>;
  extensions: Record<string, number>;
}

export interface OptionChainAnalysis {
  pcr: number;
  maxPain: number;
  totalCE_OI: number;
  totalPE_OI: number;
  pcrVolume: number;
  atmIV: number;
  expiry: Date;
}

// types/chart.ts
export type ChartType = 'candlestick' | 'line' | 'bar' | 'area' | 'heikinashi';

export type Timeframe = '1m' | '5m' | '15m' | '30m' | '1h' | '4h' | '1d' | '1w' | '1M';

export interface ChartSettings {
  type: ChartType;
  timeframe: Timeframe;
  indicators: IndicatorConfig[];
  overlays: string[];
  theme: 'light' | 'dark';
  showVolume: boolean;
  showGrid: boolean;
  autoScale: boolean;
}

export interface ChartAnnotation {
  id: string;
  type: 'line' | 'fibonacci' | 'rectangle' | 'text';
  points: { x: number; y: number }[];
  color: string;
  text?: string;
}

export interface ChartData {
  ohlcv: OHLCV[];
  indicators: Map<string, IndicatorResult>;
  annotations: ChartAnnotation[];
  volume: OHLCV[];
}

// types/ai.ts
export interface AIPrediction {
  symbol: string;
  timeframe: Timeframe;
  prediction: 'UP' | 'DOWN' | 'SIDEWAYS';
  confidence: number;
  targetPrice: number;
  stopLoss: number;
  timeHorizon: string;
  generatedAt: Date;
  modelVersion: string;
}

export interface PatternMatch {
  pattern: string;
  type: 'candlestick' | 'chart' | 'harmonic';
  confidence: number;
  startIndex: number;
  endIndex: number;
  targetPrice?: number;
  description: string;
}

export interface SentimentResult {
  overall: 'positive' | 'negative' | 'neutral';
  score: number;
  sources: {
    news: number;
    social: number;
    market: number;
  };
  keywords: string[];
  analyzedAt: Date;
}

export interface ModelPerformance {
  modelName: string;
  accuracy: number;
  precision: number;
  recall: number;
  f1Score: number;
  lastTrained: Date;
  totalPredictions: number;
}

// types/scanner.ts
export interface ScanFilter {
  id: string;
  field: string;
  operator: '>' | '<' | '=' | '>=' | '<=' | 'between' | 'in';
  value: number | number[] | string[];
}

export interface ScanCriteria {
  name: string;
  filters: ScanFilter[];
  patternFilters: string[];
  timeframe: Timeframe;
  exchanges: string[];
}

export interface ScanResult {
  symbol: string;
  name: string;
  price: number;
  change: number;
  volume: number;
  matchedCriteria: string[];
  technicalScore: number;
}

export interface SavedScan {
  id: string;
  name: string;
  criteria: ScanCriteria;
  createdAt: Date;
  lastRun: Date;
  resultCount: number;
}

// types/portfolio.ts
export interface Position {
  id: string;
  symbol: string;
  name: string;
  quantity: number;
  avgPrice: number;
  currentPrice: number;
  invested: number;
  currentValue: number;
  pnl: number;
  pnlPercent: number;
  sector: string;
  addedAt: Date;
}

export interface Portfolio {
  id: string;
  name: string;
  positions: Position[];
  totalInvested: number;
  currentValue: number;
  totalPnL: number;
  totalPnLPercent: number;
  dayPnL: number;
  dayPnLPercent: number;
  createdAt: Date;
}

export interface Transaction {
  id: string;
  symbol: string;
  type: 'BUY' | 'SELL';
  quantity: number;
  price: number;
  total: number;
  timestamp: Date;
  brokerage: number;
  taxes: number;
}

// types/alerts.ts
export type AlertType = 'price' | 'indicator' | 'volume' | 'pattern' | 'news';

export type AlertCondition = 'above' | 'below' | 'crosses_above' | 'crosses_below' | 'equals';

export interface Alert {
  id: string;
  symbol: string;
  type: AlertType;
  condition: AlertCondition;
  value: number;
  message: string;
  isActive: boolean;
  createdAt: Date;
  triggeredAt?: Date;
  notificationMethods: ('push' | 'email' | 'sms')[];
}

export interface AlertHistory {
  alertId: string;
  symbol: string;
  triggeredAt: Date;
  triggeredValue: number;
  message: string;
}

// types/user.ts
export interface User {
  id: string;
  email: string;
  name: string;
  avatar?: string;
  preferences: UserPreferences;
  subscription: SubscriptionTier;
  createdAt: Date;
  lastLogin: Date;
}

export interface UserPreferences {
  theme: 'light' | 'dark' | 'system';
  defaultChartInterval: Timeframe;
  defaultIndicators: string[];
  notifications: NotificationPreferences;
  language: string;
  timezone: string;
}

export interface NotificationPreferences {
  priceAlerts: boolean;
  newsAlerts: boolean;
  portfolioUpdates: boolean;
  marketOpenClose: boolean;
  emailDigest: 'daily' | 'weekly' | 'never';
}

export type SubscriptionTier = 'free' | 'basic' | 'pro' | 'enterprise';

export interface Subscription {
  tier: SubscriptionTier;
  validUntil: Date;
  features: string[];
  maxAlerts: number;
  maxScans: number;
  apiRateLimit: number;
}

// types/analysis.ts
export interface AnalysisResult {
  symbol: string;
  interval: Timeframe;
  timestamp: Date;
  signal: 'STRONG_BUY' | 'BUY' | 'NEUTRAL' | 'SELL' | 'STRONG_SELL';
  confidence: number;
  priceMetrics: {
    current: number;
    open: number;
    high: number;
    low: number;
    close: number;
    change: number;
    changePercent: number;
    volume: number;
    avgVolume: number;
  };
  indicators: TechnicalIndicatorsSet;
  aiInsights: AIInsight[];
  patterns: PatternMatch[];
  priceAction: {
    pivots: PivotPoints;
    fibonacci: FibonacciLevels;
    supportResistance: { support: number[]; resistance: number[] };
    supplyDemandZones: { type: 'SUPPLY' | 'DEMAND'; range: [number, number]; strength: number }[];
    gaps: { type: string; range: [number, number] }[];
  };
  derivatives?: OptionChainAnalysis;
  riskMetrics: {
    volatility: number;
    beta: number;
    sharpeRatio: number;
    maxDrawdown: number;
  };
}

export interface AIInsight {
  type: 'pattern' | 'prediction' | 'sentiment' | 'correlation';
  title: string;
  description: string;
  confidence: number;
  data?: Record<string, any>;
}

// types/api.ts
export interface APIResponse<T> {
  success: boolean;
  data?: T;
  error?: APIError;
  meta?: {
    page?: number;
    limit?: number;
    total?: number;
    timestamp: string;
  };
}

export interface APIError {
  code: string;
  message: string;
  details?: Record<string, any>;
}

export interface PaginationParams {
  page: number;
  limit: number;
  sortBy?: string;
  sortOrder?: 'asc' | 'desc';
}

// types/common.ts
export interface SelectOption {
  value: string;
  label: string;
  disabled?: boolean;
}

export interface TableColumn<T> {
  key: string;
  title: string;
  dataIndex?: keyof T;
  render?: (value: any, record: T) => React.ReactNode;
  sorter?: (a: T, b: T) => number;
  width?: number;
}

export interface ChartPoint {
  x: number;
  y: number;
}

export interface Range {
  min: number;
  max: number;
}
```

---

## 18. DATABASE SCHEMA (PostgreSQL)

```sql
-- Users table
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    name VARCHAR(255) NOT NULL,
    avatar_url TEXT,
    subscription_tier VARCHAR(50) DEFAULT 'free',
    subscription_expires_at TIMESTAMP,
    preferences JSONB DEFAULT '{}',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    last_login TIMESTAMP
);

-- Portfolios table
CREATE TABLE portfolios (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    name VARCHAR(255) NOT NULL,
    is_default BOOLEAN DEFAULT false,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Positions table
CREATE TABLE positions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    portfolio_id UUID REFERENCES portfolios(id) ON DELETE CASCADE,
    symbol VARCHAR(20) NOT NULL,
    name VARCHAR(255),
    sector VARCHAR(100),
    quantity INTEGER NOT NULL,
    avg_price DECIMAL(15, 4) NOT NULL,
    current_price DECIMAL(15, 4),
    added_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Transactions table
CREATE TABLE transactions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    symbol VARCHAR(20) NOT NULL,
    type VARCHAR(10) CHECK (type IN ('BUY', 'SELL')),
    quantity INTEGER NOT NULL,
    price DECIMAL(15, 4) NOT NULL,
    total DECIMAL(15, 4) NOT NULL,
    brokerage DECIMAL(10, 4) DEFAULT 0,
    taxes DECIMAL(10, 4) DEFAULT 0,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Alerts table
CREATE TABLE alerts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    symbol VARCHAR(20) NOT NULL,
    alert_type VARCHAR(50) NOT NULL,
    condition VARCHAR(50) NOT NULL,
    value DECIMAL(15, 4) NOT NULL,
    message TEXT,
    is_active BOOLEAN DEFAULT true,
    notification_methods JSONB DEFAULT '["push"]',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    triggered_at TIMESTAMP
);

-- Alert history table
CREATE TABLE alert_history (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    alert_id UUID REFERENCES alerts(id) ON DELETE CASCADE,
    triggered_value DECIMAL(15, 4) NOT NULL,
    triggered_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Saved scans table
CREATE TABLE saved_scans (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    name VARCHAR(255) NOT NULL,
    criteria JSONB NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    last_run TIMESTAMP,
    result_count INTEGER DEFAULT 0
);

-- Historical data cache
CREATE TABLE stock_data_cache (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    symbol VARCHAR(20) NOT NULL,
    interval VARCHAR(10) NOT NULL,
    data JSONB NOT NULL,
    from_date TIMESTAMP NOT NULL,
    to_date TIMESTAMP NOT NULL,
    cached_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    expires_at TIMESTAMP,
    UNIQUE(symbol, interval, from_date, to_date)
);

-- Analysis history
CREATE TABLE analysis_history (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    symbol VARCHAR(20) NOT NULL,
    interval VARCHAR(10) NOT NULL,
    analysis_result JSONB NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Watchlists
CREATE TABLE watchlists (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    name VARCHAR(255) NOT NULL,
    symbols JSONB DEFAULT '[]',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Indexes
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_positions_portfolio ON positions(portfolio_id);
CREATE INDEX idx_transactions_user ON transactions(user_id);
CREATE INDEX idx_transactions_symbol ON transactions(symbol);
CREATE INDEX idx_alerts_user ON alerts(user_id);
CREATE INDEX idx_alerts_symbol ON alerts(symbol);
CREATE INDEX idx_stock_cache_lookup ON stock_data_cache(symbol, interval);
CREATE INDEX idx_analysis_history_user ON analysis_history(user_id);
```

---

## 19. API INTEGRATION DETAILS

### 19.1 NSE India API
```typescript
// services/api/nseApi.ts
import axios from 'axios';

const NSE_BASE_URL = 'https://www.nseindia.com/api';

class NSEApiService {
  private client = axios.create({
    baseURL: NSE_BASE_URL,
    headers: {
      'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36',
      'Accept': 'application/json',
    },
    timeout: 10000,
  });

  // Get NIFTY 50 stocks
  async getNifty50(): Promise<StockQuote[]> {
    const response = await this.client.get('/marketData/preOpenKeyIndicator?key=NIFTY%2050');
    return response.data.data;
  }

  // Get stock quote
  async getQuote(symbol: string): Promise<StockQuote> {
    const response = await this.client.get(`/quote-equity?symbol=${symbol}`);
    return response.data;
  }

  // Get historical data
  async getHistoricalData(
    symbol: string, 
    series: string = 'EQ',
    from: Date, 
    to: Date
  ): Promise<OHLCV[]> {
    const fromStr = from.toISOString().split('T')[0];
    const toStr = to.toISOString().split('T')[0];
    const response = await this.client.get(
      `/historical/cm/equity?symbol=${symbol}&series=${series}&from=${fromStr}&to=${toStr}`
    );
    return response.data.data;
  }

  // Get intraday data
  async getIntradayData(symbol: string, interval: string = '1m'): Promise<IntradayData[]> {
    const response = await this.client.get(`/chart-databyindex?index=${symbol}&preclose=false&undefined=undefined&intraday=true&resolution=${interval}`);
    return response.data;
  }

  // Get market depth
  async getMarketDepth(symbol: string): Promise<MarketDepth> {
    const response = await this.client.get(`/quote-equity?symbol=${symbol}&section=trade_info`);
    return response.data;
  }

  // Get all symbols
  async getAllSymbols(): Promise<{symbol: string; name: string}[]> {
    const response = await this.client.get('/market-data-pre-open?key=ALL');
    return response.data.data.map((item: any) => ({
      symbol: item.symbol,
      name: item.companyName
    }));
  }
}

export const nseApi = new NSEApiService();
```

### 19.2 Yahoo Finance API
```typescript
// services/api/yahooFinance.ts
import axios from 'axios';

const YAHOO_BASE_URL = 'https://query1.finance.yahoo.com/v8/finance';

class YahooFinanceService {
  private client = axios.create({
    baseURL: YAHOO_BASE_URL,
    timeout: 15000,
  });

  // Convert NSE symbol to Yahoo format
  private formatSymbol(symbol: string): string {
    return `${symbol}.NS`;
  }

  async getQuote(symbol: string): Promise<StockQuote> {
    const formattedSymbol = this.formatSymbol(symbol);
    const response = await this.client.get(`/chart/${formattedSymbol}`);
    const result = response.data.chart.result[0];
    const meta = result.meta;
    
    return {
      symbol,
      currentPrice: meta.regularMarketPrice,
      change: meta.regularMarketChange,
      changePercent: meta.regularMarketChangePercent,
      open: meta.regularMarketOpen,
      high: meta.regularMarketDayHigh,
      low: meta.regularMarketDayLow,
      close: meta.previousClose,
      volume: meta.regularMarketVolume,
      // ... other fields
    };
  }

  async getHistoricalData(
    symbol: string,
    period1: number,
    period2: number,
    interval: string = '1d'
  ): Promise<OHLCV[]> {
    const formattedSymbol = this.formatSymbol(symbol);
    const response = await this.client.get(
      `/chart/${formattedSymbol}?period1=${period1}&period2=${period2}&interval=${interval}`
    );
    
    const result = response.data.chart.result[0];
    const timestamps = result.timestamp;
    const { open, high, low, close, volume } = result.indicators.quote[0];
    
    return timestamps.map((ts: number, i: number) => ({
      timestamp: ts * 1000,
      open: open[i],
      high: high[i],
      low: low[i],
      close: close[i],
      volume: volume[i],
    }));
  }
}

export const yahooFinance = new YahooFinanceService();
```

---

## 20. TESTING STRATEGY

### 20.1 Unit Tests
```typescript
// Example: tests/unit/indicators/rsi.test.ts
import { calculateRSI } from '../../../src/services/indicators/momentum/rsi';

describe('RSI Calculation', () => {
  const sampleData = [
    { close: 44.34 }, { close: 44.09 }, { close: 44.15 },
    { close: 43.61 }, { close: 44.33 }, { close: 44.83 },
    // ... more data
  ];

  it('should calculate RSI correctly for 14-period', () => {
    const rsi = calculateRSI(sampleData, 14);
    expect(rsi.values).toHaveLength(sampleData.length);
    expect(rsi.currentValue).toBeGreaterThan(0);
    expect(rsi.currentValue).toBeLessThan(100);
  });

  it('should identify overbought conditions', () => {
    const overboughtData = Array(15).fill({ close: 100 });
    const rsi = calculateRSI(overboughtData, 14);
    expect(rsi.currentValue).toBeGreaterThan(70);
  });

  it('should identify oversold conditions', () => {
    const oversoldData = Array(15).fill({ close: 10 });
    const rsi = calculateRSI(oversoldData, 14);
    expect(rsi.currentValue).toBeLessThan(30);
  });
});
```

### 20.2 Integration Tests
```typescript
// Example: tests/integration/api.test.ts
import { nseApi } from '../../src/services/api/nseApi';

describe('NSE API Integration', () => {
  it('should fetch NIFTY 50 data', async () => {
    const data = await nseApi.getNifty50();
    expect(data).toBeDefined();
    expect(Array.isArray(data)).toBe(true);
    expect(data.length).toBeGreaterThan(0);
  });

  it('should fetch historical data', async () => {
    const from = new Date('2024-01-01');
    const to = new Date('2024-01-31');
    const data = await nseApi.getHistoricalData('RELIANCE', 'EQ', from, to);
    expect(data).toBeDefined();
    expect(data.length).toBeGreaterThan(0);
  });
});
```

### 20.3 E2E Tests (Cypress)
```typescript
// cypress/e2e/analysis.cy.ts
describe('Stock Analysis Flow', () => {
  beforeEach(() => {
    cy.visit('/');
  });

  it('should complete full analysis flow', () => {
    // Splash screen
    cy.contains('Indian Trade Analysis').should('be.visible');
    cy.wait(3000);
    
    // Home screen
    cy.url().should('include', '/home');
    cy.get('[data-testid="symbol-input"]').type('RELIANCE');
    cy.get('[data-testid="interval-dropdown"]').select('1d');
    cy.get('[data-testid="analyze-button"]').click();
    
    // Loading screen
    cy.contains('Fetching market data').should('be.visible');
    cy.contains('Calculating technical indicators').should('be.visible');
    
    // Result screen
    cy.url().should('include', '/result');
    cy.contains('RELIANCE').should('be.visible');
    cy.get('[data-testid="signal-card"]').should('be.visible');
    
    // Navigate to chart
    cy.get('[data-testid="view-chart-button"]').click();
    cy.url().should('include', '/chart');
    cy.get('[data-testid="candlestick-chart"]').should('be.visible');
  });
});
```

---

## 21. DEPLOYMENT CONFIGURATION

### 21.1 Docker Configuration
```dockerfile
# Dockerfile
FROM node:18-alpine AS builder

WORKDIR /app
COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

### 21.2 Nginx Configuration
```nginx
# nginx.conf
server {
    listen 80;
    server_name localhost;
    root /usr/share/nginx/html;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }

    location /api {
        proxy_pass http://backend:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }

    location /ws {
        proxy_pass http://websocket:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }

    # Enable gzip compression
    gzip on;
    gzip_types text/plain text/css application/json application/javascript text/xml;
}
```

### 21.3 CI/CD Pipeline (GitHub Actions)
```yaml
# .github/workflows/deploy.yml
name: Deploy

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
          cache: 'npm'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Run linter
        run: npm run lint
      
      - name: Run type check
        run: npm run typecheck
      
      - name: Run tests
        run: npm run test:ci
      
      - name: Build
        run: npm run build

  deploy:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Deploy to Vercel
        uses: vercel/action-deploy@v1
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          vercel-org-id: ${{ secrets.VERCEL_ORG_ID }}
          vercel-project-id: ${{ secrets.VERCEL_PROJECT_ID }}
```

---

## 22. PERFORMANCE OPTIMIZATION

### 22.1 Code Splitting
```typescript
// routes.tsx with lazy loading
import { lazy, Suspense } from 'react';
import { Route, Routes } from 'react-router-dom';
import { LoadingScreen } from './screens/Loading';

const SplashScreen = lazy(() => import('./screens/Splash/SplashScreen'));
const HomeScreen = lazy(() => import('./screens/Home/HomeScreen'));
const ResultScreen = lazy(() => import('./screens/Result/ResultScreen'));
const ChartScreen = lazy(() => import('./screens/Chart/ChartScreen'));

export const AppRoutes = () => (
  <Suspense fallback={<LoadingScreen />}>
    <Routes>
      <Route path="/" element={<SplashScreen />} />
      <Route path="/home" element={<HomeScreen />} />
      <Route path="/result" element={<ResultScreen />} />
      <Route path="/chart" element={<ChartScreen />} />
    </Routes>
  </Suspense>
);
```

### 22.2 Data Caching Strategy
```typescript
// hooks/useStockData.ts with caching
import { useQuery } from 'react-query';
import { nseApi } from '../services/api/nseApi';

const STALE_TIME = 5 * 60 * 1000; // 5 minutes
const CACHE_TIME = 30 * 60 * 1000; // 30 minutes

export const useStockData = (symbol: string, interval: string) => {
  return useQuery(
    ['stockData', symbol, interval],
    () => nseApi.getHistoricalData(symbol, 'EQ', from, to),
    {
      staleTime: STALE_TIME,
      cacheTime: CACHE_TIME,
      retry: 3,
      retryDelay: (attemptIndex) => Math.min(1000 * 2 ** attemptIndex, 30000),
      onError: (error) => {
        console.error('Failed to fetch stock data:', error);
      },
    }
  );
};
```

### 22.3 Web Workers for Heavy Computations
```typescript
// workers/indicatorWorker.ts
self.onmessage = (event) => {
  const { type, data, params } = event.data;
  
  switch (type) {
    case 'RSI':
      const rsi = calculateRSI(data, params.period);
      self.postMessage({ type: 'RSI', result: rsi });
      break;
    case 'MACD':
      const macd = calculateMACD(data, params.fast, params.slow, params.signal);
      self.postMessage({ type: 'MACD', result: macd });
      break;
    // ... other indicators
  }
};

// hooks/useWorker.ts
export const useIndicatorWorker = () => {
  const workerRef = useRef<Worker | null>(null);

  useEffect(() => {
    workerRef.current = new Worker(
      new URL('../workers/indicatorWorker.ts', import.meta.url)
    );
    
    return () => {
      workerRef.current?.terminate();
    };
  }, []);

  const calculateIndicator = useCallback((type: string, data: any, params: any) => {
    return new Promise((resolve) => {
      workerRef.current?.postMessage({ type, data, params });
      workerRef.current?.addEventListener('message', (e) => {
        if (e.data.type === type) {
          resolve(e.data.result);
        }
      }, { once: true });
    });
  }, []);

  return { calculateIndicator };
};
```

---

## 23. ERROR HANDLING & MONITORING

### 23.1 Error Boundary
```typescript
// components/common/Error/ErrorBoundary.tsx
import React, { Component, ErrorInfo, ReactNode } from 'react';

interface Props {
  children: ReactNode;
  fallback?: ReactNode;
}

interface State {
  hasError: boolean;
  error?: Error;
}

export class ErrorBoundary extends Component<Props, State> {
  public state: State = {
    hasError: false
  };

  public static getDerivedStateFromError(error: Error): State {
    return { hasError: true, error };
  }

  public componentDidCatch(error: Error, errorInfo: ErrorInfo) {
    console.error('Uncaught error:', error, errorInfo);
    // Send to error tracking service (Sentry, etc.)
    // sentry.captureException(error);
  }

  public render() {
    if (this.state.hasError) {
      return this.props.fallback || (
        <div className="error-fallback">
          <h2>Something went wrong</h2>
          <p>We're working on fixing this issue. Please try again later.</p>
          <button onClick={() => window.location.reload()}>
            Reload Page
          </button>
        </div>
      );
    }

    return this.props.children;
  }
}
```

### 23.2 API Error Handler
```typescript
// utils/errorHandlers/apiErrorHandler.ts
export class APIError extends Error {
  constructor(
    message: string,
    public code: string,
    public status: number,
    public data?: any
  ) {
    super(message);
    this.name = 'APIError';
  }
}

export const handleApiError = (error: any): APIError => {
  if (error.response) {
    // Server responded with error
    const { status, data } = error.response;
    return new APIError(
      data.message || 'An error occurred',
      data.code || 'UNKNOWN_ERROR',
      status,
      data
    );
  } else if (error.request) {
    // Request made but no response
    return new APIError(
      'Network error. Please check your connection.',
      'NETWORK_ERROR',
      0
    );
  } else {
    // Something else happened
    return new APIError(
      error.message || 'An unexpected error occurred',
      'UNKNOWN_ERROR',
      500
    );
  }
};
```

---

## 24. AUTHENTICATION & AUTHORIZATION

### 24.1 Auth Context
```typescript
// context/AuthContext.tsx
import React, { createContext, useContext, useState, useEffect } from 'react';
import { User, SubscriptionTier } from '../types/user';

interface AuthContextType {
  user: User | null;
  isAuthenticated: boolean;
  isLoading: boolean;
  login: (email: string, password: string) => Promise<void>;
  logout: () => void;
  register: (email: string, password: string, name: string) => Promise<void>;
  hasFeature: (feature: string) => boolean;
}

const AuthContext = createContext<AuthContextType | undefined>(undefined);

export const AuthProvider: React.FC<{ children: React.ReactNode }> = ({ children }) => {
  const [user, setUser] = useState<User | null>(null);
  const [isLoading, setIsLoading] = useState(true);

  useEffect(() => {
    // Check for existing session
    const token = localStorage.getItem('auth_token');
    if (token) {
      validateToken(token);
    } else {
      setIsLoading(false);
    }
  }, []);

  const login = async (email: string, password: string) => {
    const response = await fetch('/api/auth/login', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ email, password }),
    });
    
    if (!response.ok) throw new Error('Login failed');
    
    const { user, token } = await response.json();
    localStorage.setItem('auth_token', token);
    setUser(user);
  };

  const logout = () => {
    localStorage.removeItem('auth_token');
    setUser(null);
  };

  const hasFeature = (feature: string): boolean => {
    if (!user) return false;
    const tierFeatures: Record<SubscriptionTier, string[]> = {
      free: ['basic_charts', 'basic_indicators'],
      basic: ['basic_charts', 'basic_indicators', 'scanner'],
      pro: ['all_charts', 'all_indicators', 'scanner', 'alerts', 'ai_predictions'],
      enterprise: ['all_features', 'api_access', 'priority_support'],
    };
    return tierFeatures[user.subscription.tier].includes(feature);
  };

  return (
    <AuthContext.Provider value={{
      user,
      isAuthenticated: !!user,
      isLoading,
      login,
      logout,
      register: async () => {},
      hasFeature,
    }}>
      {children}
    </AuthContext.Provider>
  );
};

export const useAuth = () => {
  const context = useContext(AuthContext);
  if (!context) throw new Error('useAuth must be used within AuthProvider');
  return context;
};
```

### 24.2 Protected Route Guard
```typescript
// guards/AuthGuard.tsx
import { Navigate } from 'react-router-dom';
import { useAuth } from '../context/AuthContext';

interface AuthGuardProps {
  children: React.ReactNode;
  requiredFeature?: string;
}

export const AuthGuard: React.FC<AuthGuardProps> = ({ children, requiredFeature }) => {
  const { isAuthenticated, isLoading, hasFeature } = useAuth();

  if (isLoading) {
    return <div>Loading...</div>;
  }

  if (!isAuthenticated) {
    return <Navigate to="/login" replace />;
  }

  if (requiredFeature && !hasFeature(requiredFeature)) {
    return <Navigate to="/upgrade" replace />;
  }

  return <>{children}</>;
};
```

---

## 25. ENVIRONMENT CONFIGURATION

### 25.1 Environment Files
```bash
# .env.example
# API Configuration
REACT_APP_NSE_API_URL=https://www.nseindia.com/api
REACT_APP_YAHOO_API_URL=https://query1.finance.yahoo.com/v8/finance
REACT_APP_BACKEND_API_URL=https://api.indiantradeanalysis.com

# AI/ML Configuration
REACT_APP_TENSORFLOW_MODELS_PATH=/models
REACT_APP_ENABLE_AI_FEATURES=true

# Feature Flags
REACT_APP_ENABLE_PAPER_TRADING=true
REACT_APP_ENABLE_BACKTESTING=true
REACT_APP_ENABLE_SOCIAL_FEATURES=false

# Analytics & Monitoring
REACT_APP_SENTRY_DSN=
REACT_APP_GOOGLE_ANALYTICS_ID=
REACT_APP_HOTJAR_ID=

# App Configuration
REACT_APP_APP_NAME=Indian Trade Analysis
REACT_APP_DEFAULT_THEME=dark
REACT_APP_CACHE_DURATION=300000
REACT_APP_API_TIMEOUT=10000

# WebSocket
REACT_APP_WS_URL=wss://ws.indiantradeanalysis.com
```

---

## 26. EXTENDED IMPLEMENTATION PHASES

### Phase 7: Authentication & User Management (Week 11)
- [ ] User registration/login
- [ ] JWT token management
- [ ] Password reset
- [ ] User profile management
- [ ] Subscription tiers

### Phase 8: Advanced Features (Week 12)
- [ ] Stock scanner
- [ ] Portfolio tracking
- [ ] Alerts system
- [ ] Market overview
- [ ] Backtesting engine

### Phase 9: Paper Trading (Week 13)
- [ ] Virtual wallet
- [ ] Order management
- [ ] Position tracking
- [ ] Performance analytics
- [ ] Trade history

### Phase 10: Production Ready (Week 14)
- [ ] Security audit
- [ ] Performance optimization
- [ ] Load testing
- [ ] Documentation
- [ ] Deployment setup

**Updated Timeline:** 14 weeks  
**Updated Team Size:** 3-4 developers

---

## 27. CONCLUSION

This comprehensive project plan for **Indian Trade Analysis** provides a complete roadmap for building a production-ready technical analysis platform for Indian stock markets (NSE). 

**Key Highlights:**
- 10+ screens with detailed designs
- 20+ technical indicators
- AI/ML integration with TensorFlow.js
- Complete authentication & subscription system
- Real-time data via WebSockets
- Advanced features: Scanner, Portfolio, Alerts, Backtesting, Paper Trading
- Production-ready architecture with testing, CI/CD, and monitoring

**Next Steps:**
1. Review and approve the plan
2. Set up development environment
3. Initialize project with Vite + React + TypeScript
4. Begin Phase 1 implementation
5. Weekly progress reviews

**Success Metrics:**
- Page load time < 2 seconds
- Chart rendering < 500ms
- 99.9% uptime
- Support for 1000+ concurrent users
- Mobile-responsive design

---

*Document Version: 2.0 - ENHANCED*  
*Created: February 2026*  
*For: Indian Stock Market Technical Analysis Platform*  
*Total Sections: 27*  
*Complexity: Advanced*
