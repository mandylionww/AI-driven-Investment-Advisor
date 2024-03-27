# AI-driven-Investment-Advisor
開発AIを利用した投資アドバイザーは、市場データを分析し、個々の投資家にパーソナライズされた推奨事項を提供します。
import numpy as np
import pandas as pd

# Simulate some market data
np.random.seed(0)  # For reproducibility
dates = pd.date_range('20240101', periods=100)
symbols = ['AAPL', 'GOOGL', 'MSFT', 'AMZN', 'TSLA']
data = np.random.randn(100, 5).cumsum(axis=0) + 100
market_data = pd.DataFrame(data, index=dates, columns=symbols)

# A simplistic AI model for investment recommendations
def simple_investment_advisor(market_data, user_profile):
    """
    Generates investment recommendations based on market data and the user's profile.
    
    :param market_data: DataFrame with market data.
    :param user_profile: Dict with user profile information, including 'risk_tolerance' and 'investment_goal'.
    :return: Dict with recommended investments and reasons.
    """
    recommendations = {}
    
    # Example rule: if user is risk-averse, recommend the stock with the least volatility
    if user_profile['risk_tolerance'] == 'low':
        volatility = market_data.std()
        least_volatile_stock = volatility.idxmin()
        recommendations[least_volatile_stock] = 'Recommended for its low volatility.'
    
    # Example rule: if user is seeking growth, recommend the stock with the highest growth
    elif user_profile['risk_tolerance'] == 'high' and user_profile['investment_goal'] == 'growth':
        growth = market_data.iloc[-1] - market_data.iloc[0]
        highest_growth_stock = growth.idxmax()
        recommendations[highest_growth_stock] = 'Recommended for its high growth potential.'
    
    return recommendations

# Example user profile
user_profile = {
    'risk_tolerance': 'low',
    'investment_goal': 'safety',
    'capital': 10000
}

# Generate recommendations
recommendations = simple_investment_advisor(market_data, user_profile)
print("Investment Recommendations:", recommendations)
