# Agatha
![alt-text](https://img.shields.io/hexpm/l/plug.svg)  
Agatha is a tool to help you predict future close prices for any given stock tickers.

<p align="center">
<img src="https://github.com/driemworks/agatha/blob/master/resources/images/full.PNG?raw=true" alt="full" width="400" height="400">|<img src="https://github.com/driemworks/agatha/blob/master/resources/images/prediction.PNG?raw=true" alt="full" width="400" height="400">
</p>

## Should I have faith in the predictions?
Probably not. 

## How it works
Agatha uses an LSTM network to predict close prices for a user-specified number of days in the future. The training data is downloaded via [Alpha Vantage](https://www.alphavantage.co/).

## Requirements
- python 3.5 or higher

## Installation
Clone this repository. Inside the Agatha folder, create the agatha package using
``` python
python setup.py sdist
```
Then install using pip. If you are using windows
``` python
pip install ./dist/agatha-1.0-dev.zip
```
If you are using a unix based OS
``` python
pip install ./dist/agatha-1.0-dev.tar.gz
```
If you use anaconda, you can load the conda environment using the environment.yml file in `resources/conda`
and running ```conda env create -f environment.yml```

## Usage
First get an API key from Alpha Vantage. 
To train a model for a  particular ticker, use
``` python
model = getOrTrainModel(alpha_vantage_api_key, ticker, attribute, alphavantage_data,
						model_data, weights_data, epochs=epochs, look_back=look_back)
```
where 
- ticker is the stock ticker
- attribute is the stock attribute to predict (open, close, volume),
- alphavantage data is downloaded as a csv and then pickled (saved as .pkl)
- the model_data is saved as json
- the weights file is saved as .h5

Predictions for future close prices for a stock can have output type as `json` or `plot` (will show pyplot)  
``` python
prediction_output = predictFuture(model, num_days_to_predict, ouptut_type)
```

Example:

```python
model = getOrTrainModel('adsfadsfasdf', 'GE', 'GE.pkl', 'open', 'model.json', 'weights.h5')
prediction_output = predictFuture(model, 2, 'json')
```

then `predition_output` is the following JSON:
```
{
   "ticker":"GE",
   "column":"open",
   "predictions":[
      {
         "day":"1",
         "price":"8.009521"
      },
      {
         "day":"2",
         "price":"8.117293"
      }
}
```
Refer to [app.py](https://github.com/driemworks/agatha/blob/master/examples/app.py), for a working example.

## Future Enhancements
- Allow other sources of historical data (including cryptocurrencies)
- Any suggestions?
  
