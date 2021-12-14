# Tutorial: Integração do Power BI – Criar o modelo preditivo com um Jupyter Notebook (parte 1 de 2)

- Artigo - 11/10/2021 - 7 minutos para o fim da leitura
- - [![img](https://github.com/samuel100.png?size=32)](https://github.com/samuel100)
  - [![img](https://github.com/olprod.png?size=32)](https://github.com/olprod)



Na parte 1 deste tutorial, você treinará e implantará um modelo de machine learning preditivo usando o código em um Jupyter Notebook. Você também deverá criar um script de pontuação para definir o esquema de entrada e saída do modelo para integração ao Power BI. Na parte 2, você usará o modelo para prever resultados no Microsoft Power BI.

Neste tutorial, você:

- Criar um Jupyter Notebook.
- Criar uma instância de computação do Azure Machine Learning.
- Treinar um modelo de regressão usando o Scikit-learn.
- Escreva um script de pontuação que defina a entrada e a saída para fácil integração ao Microsoft Power BI.
- Implantar o modelo em um ponto de extremidade de pontuação em tempo real.

Há três maneiras de criar e implantar o modelo que você usará no Power BI. Este artigo aborda a "Opção A: treinar e implantar modelos usando notebooks". Essa opção é uma experiência de criação que começa pela codificação. Ela usa Jupyter Notebooks hospedados no Estúdio do Azure Machine Learning.

Mas, em vez disso, você pode usar uma das outras opções:

- [Opção B: treinar e implantar modelos usando o designer do Azure Machine Learning](https://docs.microsoft.com/pt-br/azure/machine-learning/tutorial-power-bi-designer-model). Essa experiência de criação com pouco código usa uma interface do usuário do tipo "arrastar e soltar".
- [Opção C: treinar e implantar modelos usando o machine learning automatizado](https://docs.microsoft.com/pt-br/azure/machine-learning/tutorial-power-bi-automated-model). Essa experiência de criação sem codificação automatiza totalmente a preparação de dados e o treinamento do modelo.

## Pré-requisitos

- Uma assinatura do Azure. Se você ainda não tiver uma assinatura, poderá usar uma [avaliação gratuita](https://azure.microsoft.com/free/).
- Um Workspace do Azure Machine Learning. Se você ainda não tiver um workspace, confira [Criar e gerenciar workspaces do Azure Machine Learning](https://docs.microsoft.com/pt-br/azure/machine-learning/how-to-manage-workspace#create-a-workspace).
- Conhecimento introdutório da linguagem Python e dos fluxos de trabalho de machine learning.

## Criar um notebook e uma instância de computação

Na home page do [**Estúdio do Azure Machine Learning**](https://ml.azure.com/), selecione **Criar** > **Notebook**:

![Captura de tela mostrando como criar um notebook.](https://docs.microsoft.com/pt-br/azure/machine-learning/media/tutorial-power-bi/create-new-notebook.png)

Na página **Criar um arquivo**:

1. Dê um nome ao notebook (por exemplo, *my_model_notebook*).
2. Altere o **Tipo de arquivo** para **Notebook**.
3. Selecione **Criar**.

Em seguida, para executar as células de código, crie uma instância de computação e anexe-a ao notebook. Comece selecionando o ícone de adição, na parte superior do notebook:

![Captura de tela mostrando como criar uma instância de computação.](https://docs.microsoft.com/pt-br/azure/machine-learning/media/tutorial-power-bi/create-compute.png)

Na página **Criar instância de computação**:

1. Escolha o tamanho da máquina virtual da CPU. Para este tutorial, você pode escolher um **Standard_D11_v2** com 2 núcleos e 14 GB de RAM.
2. Selecione **Avançar**.
3. Na página **Definir configurações**, forneça um **Nome de Computação** válido. Os caracteres válidos são letras maiúsculas e minúsculas, dígitos e hifens (–).
4. Selecione **Criar**.

No notebook, você poderá notar o círculo ao lado da **Computação** ficar ciano. Essa alteração de cor indica que a instância de computação está sendo criada:

![Captura de tela mostrando a instância de computação sendo criada.](https://docs.microsoft.com/pt-br/azure/machine-learning/media/tutorial-power-bi/creating.png)

 Observação

A instância de computação pode levar de 2 a 4 minutos para ser provisionada.

Depois que a instância de computação for provisionada, use o notebook para executar as células de código. Por exemplo, na célula, você pode digitar o seguinte código:

PythonCopiar

```python
import numpy as np

np.sin(3)
```

Em seguida, selecione Shift + Enter (ou Ctrl + Entre ou ainda o botão **Reproduzir**, ao lado da célula). Você deve ver o seguinte resultado:

![Captura de tela mostrando a saída de uma célula.](https://docs.microsoft.com/pt-br/azure/machine-learning/media/tutorial-power-bi/simple-sin.png)

Agora você está pronto para criar um modelo de machine learning.

## Criar um modelo usando o Scikit-learn

Neste tutorial, você usará o [conjunto de dados de Diabetes](https://www4.stat.ncsu.edu/~boos/var.select/diabetes.html). Esse conjunto de dados está disponível nos [Azure Open Datasets](https://azure.microsoft.com/services/open-datasets/).

### Importar dados

Para importar os dados, copie e cole o código abaixo em uma nova *célula de código* do notebook.

PythonCopiar

```python
from azureml.opendatasets import Diabetes

diabetes = Diabetes.get_tabular_dataset()
X = diabetes.drop_columns("Y")
y = diabetes.keep_columns("Y")
X_df = X.to_pandas_dataframe()
y_df = y.to_pandas_dataframe()
X_df.info()
```

O quadro de dados do Pandas `X_df` contém 10 variáveis de entrada de linha de base. Essas variáveis incluem idade, sexo, índice de massa corporal, pressão sanguínea média e seis medidas de soro sanguíneo. O quadro de dados do Pandas `y_df` é a variável de destino. Ele contém uma medida quantitativa de progressão de doença um ano após a linha de base. O quadro de dados contém 442 registros.

### Treinar o modelo

Crie uma *célula de código* no notebook. Então, copie o código a seguir e cole-o na célula. Esse snippet de código constrói um modelo de regressão de cume e serializa o modelo usando o formato pickle do Python.

PythonCopiar

```python
import joblib
from sklearn.linear_model import Ridge

model = Ridge().fit(X_df,y_df)
joblib.dump(model, 'sklearn_regression_model.pkl')
```

### Registre o modelo

Além do conteúdo do próprio arquivo de modelo, o modelo registrado armazenará metadados. Os metadados incluem a descrição do modelo, as marcas e as informações da estrutura.

Os metadados são úteis quando você está gerenciando e implantando modelos no workspace. Usando marcas, por exemplo, você pode categorizar os modelos e aplicar filtros ao listar os modelos no workspace. Além disso, se você marcar esse modelo com a estrutura do Scikit-learn, isso simplificará a implantação do modelo como um serviço Web.

Copie e cole o código abaixo em uma nova *célula de código* do notebook.

PythonCopiar

```python
import sklearn

from azureml.core import Workspace
from azureml.core import Model
from azureml.core.resource_configuration import ResourceConfiguration

ws = Workspace.from_config()

model = Model.register(workspace=ws,
                       model_name='my-sklearn-model',                # Name of the registered model in your workspace.
                       model_path='./sklearn_regression_model.pkl',  # Local file to upload and register as a model.
                       model_framework=Model.Framework.SCIKITLEARN,  # Framework used to create the model.
                       model_framework_version=sklearn.__version__,  # Version of scikit-learn used to create the model.
                       sample_input_dataset=X,
                       sample_output_dataset=y,
                       resource_configuration=ResourceConfiguration(cpu=2, memory_in_gb=4),
                       description='Ridge regression model to predict diabetes progression.',
                       tags={'area': 'diabetes', 'type': 'regression'})

print('Name:', model.name)
print('Version:', model.version)
```

Você também pode ver o modelo no Estúdio do Azure Machine Learning. No menu à esquerda, selecione **Modelos**:

![Captura de tela mostrando como exibir um modelo.](https://docs.microsoft.com/pt-br/azure/machine-learning/media/tutorial-power-bi/model.png)

## Definir o script de pontuação

Ao implantar um modelo que será integrado ao Power BI, você precisa definir um *script de Pontuação* do Python e um ambiente personalizado. O script de pontuação contém duas funções:

- A função `init()` é executada quando o serviço é iniciado. Ela carrega o modelo (que é baixado automaticamente do registro de modelos) e o desserializa.
- A função `run(data)` é executada quando uma chamada para o serviço inclui dados de entrada que precisam ser pontuados.

 Observação

Os decoradores do Python no código abaixo definem o esquema dos dados de entrada e saída, o que é importante para a integração ao Power BI.

Copie e cole o código abaixo em uma nova *célula de código* do notebook. O snippet de código a seguir tem um magic de célula que grava o código em um arquivo chamado *score.py*.

PythonCopiar

```python
%%writefile score.py

import json
import pickle
import numpy as np
import pandas as pd
import os
import joblib
from azureml.core.model import Model

from inference_schema.schema_decorators import input_schema, output_schema
from inference_schema.parameter_types.numpy_parameter_type import NumpyParameterType
from inference_schema.parameter_types.pandas_parameter_type import PandasParameterType


def init():
    global model
    # Replace filename if needed.
    path = os.getenv('AZUREML_MODEL_DIR') 
    model_path = os.path.join(path, 'sklearn_regression_model.pkl')
    # Deserialize the model file back into a sklearn model.
    model = joblib.load(model_path)


input_sample = pd.DataFrame(data=[{
    "AGE": 5,
    "SEX": 2,
    "BMI": 3.1,
    "BP": 3.1,
    "S1": 3.1,
    "S2": 3.1,
    "S3": 3.1,
    "S4": 3.1,
    "S5": 3.1,
    "S6": 3.1
}])

# This is an integer type sample. Use the data type that reflects the expected result.
output_sample = np.array([0])

# To indicate that we support a variable length of data input,
# set enforce_shape=False
@input_schema('data', PandasParameterType(input_sample))
@output_schema(NumpyParameterType(output_sample))
def run(data):
    try:
        print("input_data....")
        print(data.columns)
        print(type(data))
        result = model.predict(data)
        print("result.....")
        print(result)
    # You can return any data type, as long as it can be serialized by JSON.
        return result.tolist()
    except Exception as e:
        error = str(e)
        return error
```

### Definir o ambiente personalizado

Em seguida, defina o ambiente para pontuar o modelo. No ambiente, defina os pacotes do Python, como Pandas e Scikit-learn, que o script de pontuação (*score.py*) exige.

Para definir o ambiente, copie e cole o código a seguir em uma nova *célula de código* do notebook.

PythonCopiar

```python
from azureml.core.model import InferenceConfig
from azureml.core import Environment
from azureml.core.conda_dependencies import CondaDependencies

environment = Environment('my-sklearn-environment')
environment.python.conda_dependencies = CondaDependencies.create(pip_packages=[
    'azureml-defaults',
    'inference-schema[numpy-support]',
    'joblib',
    'numpy',
    'pandas',
    'scikit-learn=={}'.format(sklearn.__version__)
])

inference_config = InferenceConfig(entry_script='./score.py',environment=environment)
```

### Implantar o modelo

Para implantar o modelo, copie e cole o código seguinte em uma nova *célula de código* do notebook:

PythonCopiar

```python
service_name = 'my-diabetes-model'

service = Model.deploy(ws, service_name, [model], inference_config, overwrite=True)
service.wait_for_deployment(show_output=True)
```

 Observação

O serviço pode levar de 2 a 4 minutos para ser implantado.

Se o serviço for implantado com sucesso, você verá a seguinte saída:

txtCopiar

```txt
Tips: You can try get_logs(): https://aka.ms/debugimage#dockerlog or local deployment: https://aka.ms/debugimage#debug-locally to debug if deployment takes longer than 10 minutes.
Running......................................................................................
Succeeded
ACI service creation operation finished, operation "Succeeded"
```

Você também pode ver o serviço no Estúdio do Azure Machine Learning. No menu à esquerda, selecione **Pontos de extremidade**:

![Captura de tela mostrando como exibir o serviço.](https://docs.microsoft.com/pt-br/azure/machine-learning/media/tutorial-power-bi/endpoint.png)

Recomendamos que você teste o serviço Web para garantir que ele funcione conforme o esperado. Para retornar o bloco de anotações, no Estúdio do Azure Machine Learning, no menu à esquerda, selecione **Notebooks**. Em seguida, copie e cole o código a seguir em uma nova *célula de código* do notebook para testar o serviço.

PythonCopiar

```python
import json

input_payload = json.dumps({
    'data': X_df[0:2].values.tolist()
})

output = service.run(input_payload)

print(output)
```

A saída deve ser semelhante a esta estrutura JSON: `{'predict': [[205.59], [68.84]]}`.

## Próximas etapas

Neste tutorial, você viu como criar e implantar um modelo para que ele possa ser consumido pelo Power BI. Na próxima parte, você aprenderá a consumir esse modelo em um relatório do Power BI.

[Tutorial: Consumir um modelo no Power BI](https://docs.microsoft.com/pt-br/power-bi/connect-data/service-aml-integrate?context=azure/machine-learning/context/ml-context)

------

## Conteúdo recomendado

- [Tutorial: Usar a interface do usuário do tipo "arrastar e soltar" para criar o modelo preditivo (parte 1 de 2) - Azure Machine Learning](https://docs.microsoft.com/pt-br/azure/machine-learning/tutorial-power-bi-designer-model)

  Saiba como criar e implantar um modelo de machine learning preditivo usando o designer. Posteriormente, você poderá usá-lo para prever resultados no Microsoft Power BI.

- [Importar dados no designer - Azure Machine Learning](https://docs.microsoft.com/pt-br/azure/machine-learning/how-to-designer-import-data)

  Saiba como importar dados no designer do Azure Machine Learning usando conjuntos de dados e o componente Importar Dados do Azure Machine Learning.

- [Treinar o modelo Keras de aprendizado profundo - Azure Machine Learning](https://docs.microsoft.com/pt-br/azure/machine-learning/how-to-train-keras)

  Saiba como treinar e registrar um modelo profundo de classificação de rede neural Keras em execução no TensorFlow usando o Azure Machine Learning.

- [Tutorial: Criar o modelo preditivo usando ML automatizado (parte 1 de 2) - Azure Machine Learning](https://docs.microsoft.com/pt-br/azure/machine-learning/tutorial-power-bi-automated-model)

  Saiba como criar e implantar modelos de machine learning automatizado, de modo que você possa usar o melhor modelo para prever resultados no Microsoft Power BI.

Mostrar mais