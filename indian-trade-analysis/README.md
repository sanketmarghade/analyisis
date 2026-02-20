# Indian Trade Analysis

A comprehensive TypeScript-based Technical Analysis Platform for NSE (National Stock Exchange of India).

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue.svg)
![React](https://img.shields.io/badge/React-18.0-blue.svg)

## Features

### Core Features
- **Real-time Stock Analysis**: Analyze any NSE stock with comprehensive technical indicators
- **Interactive Charts**: Professional candlestick charts with overlays and indicators
- **AI-Powered Predictions**: Machine learning models for price prediction and pattern recognition
- **Technical Indicators**: SMA, EMA, RSI, MACD, Bollinger Bands, and more
- **Pattern Recognition**: Automatic detection of candlestick and chart patterns

### Screens
- **Splash Screen**: Animated loading with brand introduction
- **Home Screen**: Stock symbol search with autocomplete
- **Loading Screen**: Progress tracking for analysis
- **Result Screen**: Comprehensive analysis summary with indicators
- **Chart Screen**: Interactive technical charts with overlays

### Technical Indicators
- **Trend**: SMA, EMA, VWAP, ADX, Supertrend, Parabolic SAR
- **Momentum**: RSI, MACD, Stochastic, Williams %R, CCI
- **Volatility**: Bollinger Bands, ATR, Keltner Channels
- **Volume**: OBV, MFI, Volume Profile, Chaikin Money Flow

### AI/ML Components
- **Price Prediction**: LSTM-based time series forecasting
- **Pattern Recognition**: CNN for detecting candlestick patterns
- **Sentiment Analysis**: Market sentiment from various sources
- **Signal Generation**: Ensemble model for trading signals

## Tech Stack

- **Framework**: React 18+ with TypeScript
- **State Management**: Redux Toolkit
- **Styling**: Tailwind CSS
- **Charts**: Lightweight Charts (TradingView)
- **Animations**: Framer Motion
- **AI/ML**: TensorFlow.js
- **Build Tool**: Vite

## Getting Started

### Prerequisites
- Node.js 18+ 
- npm or yarn

### Installation

1. Clone the repository
```bash
git clone https://github.com/yourusername/indian-trade-analysis.git
cd indian-trade-analysis
```

2. Install dependencies
```bash
npm install
```

3. Start the development server
```bash
npm run dev
```

4. Open your browser and navigate to `http://localhost:3000`

## Project Structure

```
indian-trade-analysis/
├── public/                  # Static assets
├── src/
│   ├── components/          # Reusable UI components
│   │   ├── common/         # Button, Card, Input, etc.
│   │   ├── charts/         # Chart-related components
│   │   └── indicators/     # Indicator display components
│   ├── screens/            # Main application screens
│   │   ├── Splash/         # Splash screen
│   │   ├── Home/           # Home screen
│   │   ├── Loading/        # Loading screen
│   │   ├── Result/         # Analysis result screen
│   │   └── Chart/          # Interactive chart screen
│   ├── hooks/              # Custom React hooks
│   ├── services/           # API and business logic
│   │   ├── api/            # NSE API, Yahoo Finance
│   │   ├── indicators/     # Technical indicator calculations
│   │   └── ai/             # AI/ML services
│   ├── store/              # Redux store
│   │   ├── slices/         # State slices
│   │   └── thunks/         # Async actions
│   ├── types/              # TypeScript type definitions
│   ├── utils/              # Utility functions
│   │   ├── constants/      # Constants
│   │   ├── formatters/     # Data formatters
│   │   ├── helpers/        # Helper functions
│   │   └── validators/     # Input validators
│   ├── styles/             # Global styles
│   ├── config/             # Configuration files
│   ├── constants/          # App constants
│   └── context/            # React contexts
├── ml-models/              # ML model files
└── package.json
```

## Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build
- `npm run lint` - Run ESLint
- `npm run lint:fix` - Fix ESLint errors
- `npm run typecheck` - Run TypeScript type checking
- `npm test` - Run tests

## API Integration

### NSE India API
The application integrates with NSE India APIs for real-time market data. Note that in development mode, mock data is used.

### Yahoo Finance
Yahoo Finance API is used as a backup data source.

## Technical Indicators Implementation

All technical indicators are implemented in pure TypeScript:

### Trend Indicators
- **SMA (Simple Moving Average)**: Calculates average price over a period
- **EMA (Exponential Moving Average)**: Weighted moving average

### Momentum Indicators
- **RSI (Relative Strength Index)**: Measures speed and magnitude of price movements
- **MACD (Moving Average Convergence Divergence)**: Trend-following momentum indicator

### Volatility Indicators
- **Bollinger Bands**: Volatility bands placed above and below a moving average

### Volume Indicators
- **OBV (On Balance Volume)**: Cumulative total of volume

## AI/ML Models

### Price Prediction
Uses an LSTM (Long Short-Term Memory) neural network trained on historical price data to predict future price movements.

### Pattern Recognition
Uses a CNN (Convolutional Neural Network) to detect candlestick patterns like:
- Doji
- Hammer/Hanging Man
- Engulfing patterns
- Morning/Evening Star

## Customization

### Adding New Indicators
1. Create a new file in `src/services/indicators/`
2. Implement the calculation logic
3. Export from `src/services/indicators/index.ts`
4. Add type definitions in `src/types/indicators.ts`

### Theming
The application uses Tailwind CSS for styling. Customize colors in `tailwind.config.js`.

## Data Sources

- NSE India Official API
- Yahoo Finance API
- Mock data (development mode)

## Browser Support

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

## Performance

- Lazy loading for screens
- Code splitting with React.lazy()
- Optimized chart rendering with Lightweight Charts
- Redux state management for efficient data flow

## Security

- Input validation for stock symbols
- XSS protection through React's built-in escaping
- No sensitive data stored in localStorage

## Roadmap

### Phase 1 (Completed)
- [x] Project setup with TypeScript + React
- [x] Basic routing and navigation
- [x] Splash screen implementation
- [x] Home screen with input components
- [x] API integration structure

### Phase 2 (Completed)
- [x] Loading screen with progress
- [x] Chart library integration
- [x] Candlestick chart display
- [x] Timeframe switching

### Phase 3 (Completed)
- [x] SMA, EMA calculations
- [x] RSI implementation
- [x] MACD calculation
- [x] Bollinger Bands
- [x] Chart overlay system

### Phase 4 (In Progress)
- [ ] TensorFlow.js integration
- [ ] Pattern recognition model
- [ ] Price prediction LSTM
- [ ] Signal generation engine

### Future Enhancements
- [ ] Stock scanner
- [ ] Portfolio tracking
- [ ] Alerts system
- [ ] Market overview
- [ ] Backtesting engine
- [ ] Paper trading

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Disclaimer

This application is for educational and research purposes only. It does not constitute financial advice. Always consult with a qualified financial advisor before making investment decisions. Past performance does not guarantee future results.

## Acknowledgments

- NSE India for market data APIs
- TradingView for Lightweight Charts library
- TensorFlow.js team for ML capabilities
- Contributors and testers

## Contact

For questions or feedback, please open an issue on GitHub.

---

Built with passion for the Indian stock market.
