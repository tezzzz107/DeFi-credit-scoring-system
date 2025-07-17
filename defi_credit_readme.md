# DeFi Credit Scoring System for Aave V2

## Overview
This system analyzes Aave V2 transaction data to generate credit scores (0-1000) for wallet addresses, identifying reliable users and flagging risky or bot-like behavior. The scoring methodology combines behavioral analysis, risk assessment, and machine learning to provide transparent, actionable credit evaluations.

## Quick Start
```bash
# Install dependencies
pip install pandas numpy scikit-learn

# Run the scorer
python defi_credit_scorer.py
```

## Scoring Methodology

### Feature Engineering (25+ Features)
The system extracts comprehensive behavioral indicators from raw transaction data:

**Activity Metrics**
- Transaction volume and frequency
- Average/median transaction sizes
- Activity duration and consistency
- Time between transactions

**Behavioral Patterns**
- Action distribution (deposit/borrow/repay/redeem/liquidation ratios)
- Asset diversification score
- User type classification (balanced, lender-only, etc.)
- Transaction regularity analysis

**Risk Indicators**
- Liquidation event frequency
- Volume concentration risk
- Transaction size volatility
- Bot-like behavior detection

### Credit Score Components

**Positive Factors (+150 to +200 points)**
- Balanced lending/borrowing activity
- Regular repayment behavior
- High transaction volume
- Long-term protocol engagement
- Asset diversification
- Consistent activity patterns

**Negative Factors (-100 to -200 points)**
- High liquidation risk
- Bot-like behavior patterns
- Extreme volume concentration
- High transaction volatility
- Irregular or suspicious patterns

### Bot Detection Algorithm
The system identifies potential bot behavior through:
- **Timing Analysis**: Detecting unnaturally regular transaction intervals
- **Pattern Recognition**: Identifying repetitive transaction amounts
- **Frequency Analysis**: Flagging unusually high transaction rates
- **Diversity Metrics**: Assessing limited action variety

### Score Interpretation

| Score Range | Tier | Description |
|-------------|------|-------------|
| 800-1000 | Excellent | Highly reliable, diverse, long-term users |
| 700-799 | Good | Responsible users with good repayment history |
| 600-699 | Fair | Average users with some positive indicators |
| 500-599 | Poor | Limited activity or some risk factors |
| 0-499 | Very Poor | High risk, bot-like, or exploitative behavior |

## Model Architecture

**Algorithm**: Random Forest Regressor
- **Rationale**: Handles non-linear relationships and feature interactions well
- **Interpretability**: Provides feature importance rankings
- **Robustness**: Resistant to outliers and missing values

**Training Process**:
1. Feature engineering from transaction data
2. Synthetic target generation based on DeFi best practices
3. Model training with cross-validation
4. Performance evaluation (RMSE, R²)

## Key Features

### 1. Transaction Analysis
- **Volume Metrics**: Total and average transaction values
- **Frequency Patterns**: Time-based activity analysis
- **Asset Diversity**: Multi-asset engagement scoring

### 2. Behavioral Classification
- **Balanced Users**: Active in multiple DeFi activities
- **Lender-Only**: Primarily deposit/lending focused
- **High-Risk**: Frequent liquidations or suspicious patterns

### 3. Risk Assessment
- **Liquidation Risk**: Based on historical liquidation events
- **Volatility Risk**: Transaction size and timing variations
- **Concentration Risk**: Over-reliance on single assets or large transactions

### 4. Bot Detection
- **Temporal Patterns**: Identifying mechanical timing
- **Amount Patterns**: Detecting repetitive transaction sizes
- **Behavioral Anomalies**: Flagging non-human-like activity

## Output Format
```json
{
  "userWallet": "0x...",
  "credit_score": 750,
  "score_tier": "Good",
  "key_metrics": {
    "total_transactions": 45,
    "total_volume_usd": 125000.50,
    "activity_duration_days": 120.5,
    "unique_assets": 4,
    "bot_score": 0.1
  },
  "risk_factors": ["High transaction volatility"],
  "positive_factors": ["Balanced lending/borrowing", "Regular repayments"]
}
```

## Validation & Extensibility

### Model Validation
- **Cross-validation**: 80/20 train-test split
- **Performance Metrics**: RMSE and R² scoring
- **Feature Importance**: Ranked feature contributions
- **Outlier Detection**: Automated anomaly flagging

### Extensibility Options
1. **Additional Protocols**: Extend to Compound, MakerDAO, etc.
2. **Multi-chain Support**: Add Ethereum, BSC, Arbitrum data
3. **Real-time Scoring**: Implement streaming updates
4. **Advanced Models**: Gradient boosting, neural networks
5. **External Data**: Incorporate token prices, market conditions

### Production Considerations
- **Labeled Data**: Replace synthetic targets with real credit outcomes
- **Model Retraining**: Regular updates with new transaction data
- **Monitoring**: Track score distribution and model drift
- **Explainability**: Enhanced feature contribution analysis

## Limitations & Assumptions
- **Synthetic Targets**: Uses rule-based scoring for training (replace with real labels)
- **Limited History**: Scores based solely on Aave V2 transactions
- **Static Features**: No real-time market condition integration
- **No Identity**: Cannot link wallets to real-world identities

## Technical Requirements
- Python 3.7+
- pandas, numpy, scikit-learn
- Input: JSON file with transaction data
- Output: Ranked credit scores with explanations

This system provides a foundation for DeFi credit assessment that can be adapted and extended for various protocols and use cases while maintaining transparency and interpretability.