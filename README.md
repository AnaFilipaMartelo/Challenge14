# Mastering Dynamic Trading: Integrating Machine Learning Algorithms
 
In this project, you'll use your expertise in financial Python programming and machine learning to achieve the following:
Implement an algorithmic trading strategy that leverages machine learning to automate trade decisions.
Fine-tune the input parameters of the trading algorithm for optimal performance.
Train and evaluate machine learning models to compare their effectiveness against a baseline model. Lastly, we'll generate cumulative strategy return plots to visualize and compare the performance of the models.

---

## Technologies

The technologies used in this project include:

   * Python 3.7
   * JupyterLab 3.4.4
   * Pandas 1.3.5
   * Scikit-Learn 1.0.2 
   * Matplotlib 3.5.2
  
---

## Installation Guide

Open your terminal and run the command:

```python
  pip install -r requirements.txt
```

---

## Usage

Clone the repository and Launch Jupyter Notebook by executing the following command in your terminal:

```python
  jupyter lab
```

In the Jupyter Notebook interface, navigate to the project directory and open the machine_learning_trading_bot.ipynb file.

Run each cell in the notebook sequentially to prepare the data, build the machine learning model, and evaluate the models' performance for comparison. 

The cumulative return plot of the trading algorithm serving as baseline obtained is the following:

<img src="Images/cumulative_returns_plot_baseline.png" alt="Baseline Plot" width="400" height="300">

The strategy returns underperforms the actual returns between the third quarter of 2017 until the third quarter of 2018. Then it starts outperforming, and it does so consistently. The underperformance during the initial period could be due to the trading algorithm adapting to new market conditions. It might take time for the model to adjust its signals to align with the changing behavior of the asset. Also, the period of underperformance could coincide with overfitting or over-optimization of the strategy to specific historical data.    

- First refinement was increasing the training window as follows:

<img src="Images/tune1.png" alt="Increase Training Window" width="500" height="400">


Classification Report: 

<img src="Images/Classification_Report_tune1.png" alt="Classification Report - tune 1" width="400" height="300">

Cumulative return plot:

<img src="Images/cumulative_returns_plot_tune1.png" alt="Classification Report - tune 1" width="400" height="300">

Increasing the training window to 8 months made the trading algorithm perform worse. It underperforms the actual returns starting on mid-2017. One possible reason is overfitting. With a larger training window, the model might start capturing not only the genuine market trends but also short-term fluctuations, irregularities, or noise. As a result, the model might become overly sensitive to the specific historical data in the training window, leading to overfitting.

- Second tuning: Tune the trading algorithm by adjusting the SMA input features

<img src="Images/tune2.png" alt="Increase Training Window" width="500" height="400">


Classification Report: 

<img src="Images/Classification_Report_tune2.png" alt="Classification Report - tune 1" width="400" height="300">

Cumulative return plot:

<img src="Images/cumulative_returns_plot_tune2.png" alt="Classification Report - tune 1" width="400" height="300">

Increasing the SMA short window made the trading algorithm perfom worse. The two lines (actual returns and strategy returns) are in sync suggests that the algorithm has not been effective in generating profitable trading decisions. This scenario is an indication that the algorithm's buy signals are not aligned with the actual market movements and price trends.

Precision 0.00, Recall 0.00: Precision and recall of 0.00 for class -1 (Sell) suggests that the model is not effectively identifying and predicting this class. This means that when the model predicts a sell signal, it rarely correctly predicts an actual sell event.

Precision 0.56, Recall 1.00: Precision of 0.56 for class 1 (Buy) indicates that when the model predicts a buy signal, it is correct about 56% of the time. Recall of 1.00 means that the model is correctly identifying all actual buy events.

This could happen if the model predictes all signals as 1(buy).
Increasing the SMA short window might have smoothed out signals to the point where certain short-term trends are lost. The longer window might not capture quick fluctuations, leading to missed sell signals.. Also, since our dataset is imbalanced (e.g., fewer sell signals compared to buy signals), the model might be biased towards the majority class (buy signals), affecting precision and recall metrics.

None of the set of parameters improved the trading algorithm returns. The original trading algorithm is the best.

---


## Contributors

* Ana Martelo (anafilipamartelo@gmail.com)

---

## License

MIT