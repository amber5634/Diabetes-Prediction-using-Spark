# Diabetes-Prediction-using-Spark
Diabetes Prediction using Logistic Regression Model with accuracy of almost 86 %

## To install OpenJdk and Pyspark on google colab
```
!apt-get install openjdk-8-jdk-headless -qq > /dev/null
!pip install pyspark==2.4.4
```

## To Set environment
```
import os
os.environ["JAVA_HOME"] = "/usr/lib/jvm/java-8-openjdk-amd64"
```

## To Create Sessiom
```
from pyspark.sql import SparkSession
spark=SparkSession.builder.appName("spark").getOrCreate()
```
## Display Data in root fashion
root <br>
 |-- Pregnancies: integer (nullable = true) <br>
 |-- Glucose: integer (nullable = true) <br>
 |-- BloodPressure: integer (nullable = true) <br>
 |-- SkinThickness: integer (nullable = true) <br>
 |-- Insulin: integer (nullable = true)  <br>
 |-- BMI: double (nullable = true)  <br>
 |-- DiabetesPedigreeFunction: double (nullable = true) <br>
 |-- Age: integer (nullable = true) <br>
 |-- Outcome: integer (nullable = true)
 
 ## Correlation for each column
- correlation to outcome for Pregnancies is 0.22443699263363961
- correlation to outcome for Glucose is 0.48796646527321064
- correlation to outcome for BloodPressure is 0.17171333286446713
- correlation to outcome for SkinThickness is 0.1659010662889893
- correlation to outcome for Insulin is 0.1711763270226193
- correlation to outcome for BMI is 0.2827927569760082
- correlation to outcome for DiabetesPedigreeFunction is 0.1554590791569403
- correlation to outcome for Age is 0.23650924717620253

Extracting important featues and importing Logistic Regression. <br>
Splitting the data into 70 % training data and 30 % test data.

## Training the data and displaying the predictions for training data

| summary       | Outcome       | prediction    |
| ------------- | ------------- | ------------- |
| count         | 1408          | 1408          |
| mean          | 0.3451704545  | 0.2563920454  |
| stddev        | 0.4755927428  | 0.4367959125  |
| min           | 0.0           | 0.0           |
| max           | 1.0           | 1.0           |

## Applying the predictions now for the test data set

```
from pyspark.ml.evaluation import BinaryClassificationEvaluator
predictions = model.evaluate(test)
```

## Evaluating the test

```
evaluator = BinaryClassificationEvaluator(rawPredictionCol='rawPrediction',labelCol='Outcome')
evaluator.evaluate(model.transform(test))
# Result 
> 0.8589832333487161
```

## The model is approximately 86 % accurate
