<h1 align="center">Datos + GitHub Copilot para soluciones avanzadas de datos</h1>
<em align="center">La combinación perfecta ™</em>

<h5 align="center">Elaborado por @pamelafox @alfredodeza</h5>
<h5 align="center">Revisión para Español @paulanunes85</h5>

## Introducción

Este repositorio contiene el código fuente completo del taller. Seguirás la guía paso a paso a continuación, completando todas las etapas mientras trabajas con datos y GitHub Copilot dentro de Codespaces.

> [!NOTA]
> Este repositorio tiene como objetivo presentar varias características de **GitHub Copilot**, como **Copilot Chat** y **chat inline**. Por lo tanto, las guías paso a paso a continuación contienen la descripción general de lo que debe hacerse, y Copilot Chat o el chat inline pueden ayudarte a generar los comandos necesarios.
>
> Cada etapa (cuando aplica) también contiene un `Cheatsheet` que puede usarse para validar las sugerencias de Copilot frente al comando correcto.
>
> 💡 Prueba diferentes prompts para ver cómo afecta esto a la precisión de las sugerencias de GitHub Copilot. Por ejemplo, al usar el chat inline, puedes usar un prompt adicional para refinar la respuesta sin necesidad de rehacer todo el prompt.

## Características del Proyecto de Datos

En este taller, trabajarás con datos de un archivo CSV incluido en este repositorio, además de un script en Python que interactúa con ese archivo CSV. Aquí están algunas de las características del proyecto:

1. Consumir un dataset en CSV y realizar transformaciones
2. Identificar e implementar validaciones
3. Crear una herramienta de línea de comando que puede ser usada en entornos de CI/CD

## Preparación

Este repositorio está listo para Codespaces y ya está preconfigurado para que tengas todas las dependencias instaladas, incluidas las extensiones de Visual Studio Code necesarias para trabajar con GitHub Copilot y Python:

- GitHub Copilot
- Extensión Python
- Dependencias Python preinstaladas con un Entorno Virtual activado

> [!NOTA]
> Si estás usando este repositorio en tu cuenta o en una organización que no sea de GitHub Universe, puede haber costos o consumo de tu cuota gratuita para Codespaces.

### 1. Crea un nuevo repositorio a partir de esta plantilla

Progreso: [🟢⚪⚪⚪⚪⚪⚪⚪⚪⚪⚪⚪] 1/12 (8%)

⏳ **~2min**

- Haz clic en `Use this template` :point_right: `Create a new repository`
- Establece el propietario como la organización GitHub Workshop: `githubuniverseworkshop`
- Dale un nombre
- Establece la visibilidad como `Private`
- Haz clic en `Create repository`

### 2. Crea un Codespace usando la plantilla proporcionada

Progreso: [🟢🟢⚪⚪⚪⚪⚪⚪⚪⚪⚪⚪] 2/12 (16%)

⏳ **~3min**

- En el repositorio recién creado, haz clic en `Code` :point_right: `Codespaces` :point_right: `[ellipsis menu]` :point_right: `New with options` :point_right: _Asegúrate de que `Dev container configuration` esté configurado como `Default project configuration`_ :point_right: `Create codespace`

- ❗Si estás teniendo problemas para iniciar el Codespace, también puedes clonar el repositorio y continuar desde tu IDE:

    ```sh
    git clone https://github.com/<TU_NAMESPACE>/<TU_REPO>.git
    cd <TU_REPO>
    ```

    > 📝 **Nota:** No hay necesidad de enviar (push) los cambios de vuelta al repositorio durante el taller

### 3. Verifica que Python esté instalado y configurado correctamente

Progreso: [🟢🟢🟢⚪⚪⚪⚪⚪⚪⚪⚪⚪] 3/12 (25%)

⏳ **~2min**

- Usa la paleta de comandos para abrir el terminal (busca "Create new terminal")
- Ejecuta `which python` y asegúrate de que apunte al Entorno Virtual (`home/vscode/venv/bin/python`)
- Ejecuta `which pip` y confirma que también apunte al Entorno Virtual (`home/vscode/venv/bin/pip`)

### 4. Ejecuta los scripts Python

Progreso: [🟢🟢🟢🟢⚪⚪⚪⚪⚪⚪⚪⚪] 4/12 (33%)

⏳ **~2min**

- Ejecuta el script `main.py` y confirma que no ocurran errores:

    ```shell
    python main.py
    ```

- Ejecuta el script `check.py` y confirma que no ocurran errores:

    ```shell
    python check.py
    ```

    Debe haber algunas líneas de OK y otras de FAIL:

    ```shell
    [OK  ]   verify_drop_notes
    [FAIL]   verify_high_ratings - Not all ratings are 90 or higher.
    [FAIL]   verify_one_hot_encoding - The 'Red Wine' column was not one-hot encoded correctly.
    [OK  ]   verify_remove_newlines_carriage_returns
    [FAIL]   verify_ratings_to_int - The 'ratings' column was not converted to integers correctly.
    ```

### 5. Abre los archivos relevantes

Progreso: [🟢🟢🟢🟢🟢⚪⚪⚪⚪⚪⚪⚪] 5/12 (41%)

⏳ **~2min**

GitHub Copilot se beneficia de tener contexto disponible. Una forma de mejorar el contexto es abrir los archivos relevantes.

- Abre los archivos `main.py`, `check.py`, `train.csv` y `transformed_train.csv`


## Desarrollo

### 1. Ve cuánto puedes aprender sobre el proyecto y los datos

Progreso: [🟢🟢🟢🟢🟢🟢⚪⚪⚪⚪⚪⚪] 6/12 (50%) - ¡La mitad del camino!

⏳ **~5min**

- Abre GitHub Copilot Chat
- Usa el agente `@workspace` para preguntar a Copilot qué hacen los archivos `main.py` y `check.py`
- Nuevamente, con el agente `@workspace`, pregunta a Copilot cuál es la naturaleza de los datos con los que vas a trabajar

#### 2. Corrige la función de calificaciones altas

Progreso: [🟢🟢🟢🟢🟢🟢🟢⚪⚪⚪⚪⚪] 7/12 (58%)

⏳ **~3min**

- En `main.py`, localiza la función `select_high_ratings()`
- Posiciona tu cursor en la firma o en algún lugar del cuerpo de la función
- Abre el chat inline con `Ctrl-i` o `Cmd-i` (en Mac)
- Prefija tu prompt con el comando `/explain`
- Pregunta por qué esta función puede no estar funcionando y implementa las posibles correcciones
- Vuelve a crear el archivo `transformed_train.csv` ejecutando `python main.py`
- Verifica la corrección ejecutando `python check.py`, asegurándote de que esta función devuelva un `OK`

<details>
<summary>Cheatsheet</summary>

##### Prompt

```sh
/explain why this function might not be working correctly?

##### Salida esperada

```sh
Based on the provided code, there are a few potential reasons why the `select_high_ratings` function might not be working correctly:

1. Error de digitación en el Nombre de la Columna: La función verifica si el nombre de la columna 'ratings' existe en df.columns. Si hay un error de digitación, como 'rating' en vez de 'ratings', la condición `if 'ratings' in df.columns`
```

</details>

> [!NOTA]
> Siéntete libre de usar GitHub Copilot Chat para implementar o confirmar la corrección

#### 3. Corrige el problema de codificación one-hot

Progreso: [🟢🟢🟢🟢🟢🟢🟢🟢⚪⚪⚪⚪] 8/12 (66%)

⏳ **~3min**
- Selecciona la función `drop_and_one_hot_encode_red_wine()` y abre el chat inline (Ctrl-i/ Cmd-i)  
- Usa el comando `/fix` para solicitar a GitHub Copilot que sugiera una posible corrección  
- Genera nuevamente el archivo `transformed_train.csv` ejecutando `python main.py`  
- Verifica la corrección ejecutando `python check.py`, asegurándote de que la función devuelva `OK`  

<details>
<summary>Cheatsheet</summary>

##### Prompt

```sh
This function is not doing one-hot encoding on the variety column
```

##### Salida esperada

```python
def drop_and_one_hot_encode_red_wine(df):
    """
    Create a 'Red_Wine' column that is 1 if 'variety' is 'Red Wine' and 0 otherwise.
    Drop the original 'variety' column.
    """
    if 'variety' in df.columns:
        df['Red_Wine'] = df['variety'].apply(lambda x: 1 if x == 'Red Wine' else 0)
        df = df.drop(columns=['variety'])
    return df
```

</details>

#### 4. Corrige la conversión de la columna de calificación a entero

Progreso: [🟢🟢🟢🟢🟢🟢🟢🟢🟢⚪⚪⚪] 9/12 (75%)

⏳ **~3min**

- Si la verificación `verify_ratings_to_int` ya está "OK", Copilot puede haber solucionado el problema. De lo contrario, sigue los pasos.  
- Selecciona la función `convert_ratings_to_int()` y abre el chat inline (Ctrl-i / Cmd-i).  
- Usa el comando `/explain` para preguntar a GitHub Copilot por qué la función puede no funcionar correctamente.  
- Identifica el problema e implementa la corrección.  
- Regenera `transformed_train.csv` ejecutando `python main.py`.  
- Verifica la corrección ejecutando `python check.py` y asegúrate de que la función devuelva `OK`.  

<details>
<summary>Cheatsheet</summary>

##### Prompt

```sh
Esta función no está convirtiendo las calificaciones a enteros
```

##### Salida Esperada

```python
def convert_ratings_to_int(df):
    """
    Convierte la columna 'rating' de float para entero.
    """
    if 'rating' in df.columns:
        df['rating'] = df['rating'].astype(int)
    return df
```

</details>
## Pruebas

Un proyecto Python robusto puede beneficiarse de pruebas. Añadirás algunas pruebas unitarias y descubrirás más sobre cómo ejecutar estas pruebas con la ayuda de GitHub Copilot.

Asegúrate de tener el terminal abierto ejecutando el comando palette y escribiendo `toggle terminal`.

### 1. Prueba tu CLI

Progreso: [🟢🟢🟢🟢🟢🟢🟢🟢🟢🟢⚪⚪] 10/12 (83%)

⏳ **~5min**

- Este proyecto tiene el Pytest test runner y framework preinstalados, asegúrate de que está disponible ejecutando `pytest --version`.
- Ejecuta las pruebas mientras estás en el directorio `workshop` usando el siguiente comando: `pytest -v`.

La salida debe mostrar un fallo.

#### 2. Corrige la prueba fallida

Progreso: [🟢🟢🟢🟢🟢🟢🟢🟢🟢🟢🟢⚪] 11/12 (91%)

⏳ **~5min**

- Selecciona la salida en el terminal y pégala en GitHub Copilot Chat, prefijando con una solicitud de corrección y explicación.
- Usa la salida del chat para implementar una corrección en `test_main.py`.

<details>
<summary>Cheatsheet</summary>

##### Prompt

```sh
Corrige la prueba y explica tu corrección:
// Copia y pega la salida del terminal aquí
```

##### Salida Esperada

El error ocurre porque la función drop_notes probablemente está modificando el DataFrame en el lugar, en vez de devolver un nuevo DataFrame con la columna 'notes' eliminada. Para corregir la prueba, necesitamos asegurar que la función drop_notes devuelva un nuevo DataFrame sin la columna 'notes' y, luego, verificar las columnas de ese nuevo DataFrame.

Aquí está la función de prueba corregida:

```python
def test_drop_notes_column_dropped():
    # Cree un DataFrame de muestra con la columna 'notes'
    df = pd.DataFrame({'A': [1, 2, 3], 'B': [4, 5, 6], 'notes': ['note1', 'note2', 'note3']})

    # Llame a la función drop_notes y obtenga el resultado
    result = main.drop_notes(df)
    
    # Verifique si la columna 'notes' en el DataFrame resultante fue eliminada
    columns = result.columns.to_list()
    assert columns == ['A', 'B']
```

Almacenando el resultado de la función drop_notes en una nueva variable y verificando sus columnas, aseguramos que la prueba verifique correctamente el comportamiento de la función.

</details>

#### 3. Añade pruebas para la función de codificación one hot

Progreso: [🟢🟢🟢🟢🟢🟢🟢🟢🟢🟢🟢🟢] 12/12 (100%) - 🎉 ¡Celebra!

⏳ **~5min**

- Asegúrate de que el `python check.py` tenga todas las salidas OK, de lo contrario, este paso puede no funcionar.
- Selecciona la función `drop_and_one_hot_encode_red_wine` en `main.py`.
- Abre el chat inline con `Ctrl-i`/`Cmd-i`.
- Usa el comando `/tests` para obtener sugerencias de pruebas.
- Revisa la salida, acéptala y verifica con el comando `pytest -v`. Todas las pruebas deberían pasar, y deberías tener más pruebas que antes. A veces, Copilot indenta incorrectamente las pruebas sugeridas (anidándolas dentro de una función de prueba existente), así que asegúrate de que las pruebas estén correctamente indentadas antes de ejecutarlas.

<details>
<summary>Cheatsheet</summary>

##### Prompt

```sh
/tests
```

```python
def test_drop_and_one_hot_encode_red_wine_coluna_red_wine_criada():
    # Crie um DataFrame de amostra com a coluna 'variety'
    df = pd.DataFrame({'A': [1, 2, 3], 'B': [4, 5, 6], 'variety': ['Red Wine', 'White Wine', 'Red Wine']})

    # Chame a função drop_and_one_hot_encode_red_wine
    result = main.drop_and_one_hot_encode_red_wine(df)

    # Verifique se a coluna 'Red_Wine_Red Wine' foi criada
    assert 'Red_Wine_Red Wine' in result.columns

def test_drop_and_one_hot_encode_red_wine_coluna_red_wine_codificada():
    # Crie um DataFrame de amostra com a coluna 'variety'
    df = pd.DataFrame({'A': [1, 2, 3], 'B': [4, 5, 6], 'variety': ['Red Wine', 'White Wine', 'Red Wine']})

    # Chame a função drop_and_one_hot_encode_red_wine
    result = main.drop_and_one_hot_encode_red_wine(df)

    # Verifique se a coluna 'Red_Wine_Red Wine' foi codificada corretamente
    assert result['Red_Wine_Red Wine'].tolist() == [1, 0, 1]

def test_drop_and_one_hot_encode_red_wine_coluna_variety_removida():
    # Crie um DataFrame de amostra com a coluna 'variety'
    df = pd.DataFrame({'A': [1, 2, 3], 'B': [4, 5, 6], 'variety': ['Red Wine', 'White Wine', 'Red Wine']})

    # Chame a função drop_and_one_hot_encode_red_wine
    result = main.drop_and_one_hot_encode_red_wine(df)

    # Verifique se a coluna 'variety' foi removida
    assert 'variety' not in result.columns

def test_drop_and_one_hot_encode_red_wine_dataframe_inalterado():
    # Crie um DataFrame de amostra com a coluna 'variety'
    df = pd.DataFrame({'A': [1, 2, 3], 'B': [4, 5, 6], 'variety': ['Red Wine', 'White Wine', 'Red Wine']})

    # Chame a função drop_and_one_hot_encode_red_wine
    result = main.drop_and_one_hot_encode_red_wine(df)

    # Verifique se a forma do DataFrame não foi alterada
    assert result.shape == (3, 3)

    # Verifique se o DataFrame original não foi modificado
    assert 'variety' in df.columns
    assert df.shape == (3, 3)
```

```python
def main():
    parser = argparse.ArgumentParser(description="CLI de manipulação de DataFrame")
    subparsers = parser.add_subparsers(dest="command")

    subparsers.add_parser("drop_notes", help="Remove a coluna 'notes' do DataFrame")
    subparsers.add_parser("select_high_ratings", help="Seleciona linhas onde a coluna 'rating' é 90 ou maior")
    subparsers.add_parser("drop_and_one_hot_encode_red_wine", help="Codifica 'Red Wine' como one-hot e remove a coluna 'variety'")
    subparsers.add_parser("remove_newlines_carriage_returns", help="Remove quebras de linha e retornos de carro das colunas de string")
    subparsers.add_parser("convert_ratings_to_int", help="Converte a coluna 'rating' de float para inteiro")

    args = parser.parse_args()

    # Carregue seu DataFrame aqui
    df = pd.read_csv('workshop/train.csv')

    if args.command == "drop_notes":
        df = drop_notes(df)
    elif args.command == "select_high_ratings":
        df = select_high_ratings(df)
    elif args.command == "drop_and_one_hot_encode_red_wine":
        df = drop_and_one_hot_encode_red_wine(df)
    elif args.command == "remove_newlines_carriage_returns":
        df = remove_newlines_carriage_returns(df)
    elif args.command == "convert_ratings_to_int":
        df = convert_ratings_to_int(df)
    else:
        parser.print_help()

    # Salva o DataFrame transformado
    df.to_csv('workshop/transformed_train.csv', index=False)

if __name__ == "__main__":
    main()
```
# CLI de Manipulación de DataFrame

Este proyecto proporciona una interfaz de línea de comandos (CLI) para manipular un DataFrame usando varias operaciones. La CLI está construida usando la biblioteca estándar de Python y no requiere dependencias externas.

## Índice

- [Instalación](#instalación)
- [Uso](#uso)
    - [Comandos](#comandos)
- [Datos](#datos)
- [Contribución](#contribución)
- [Licencia](#licencia)

## Instalación

1. Clona el repositorio:
        ```sh
        git clone https://github.com/tuusuario/tu-repo.git
        cd tu-repo
        ```

2. Configura un entorno virtual:
        ```sh
        python3 -m venv venv
        source venv/bin/activate
        ```

3. Instala los paquetes necesarios:
        ```sh
        pip install -r workshop/requirements.txt
        ```

## Uso

Para usar la CLI, navega hasta el directorio `workshop` y ejecuta el script `main.py` con el comando deseado.

### Comandos

- `drop_notes`: Elimina la columna 'notes' del DataFrame.
- `select_high_ratings`: Selecciona filas donde la columna 'rating' es 90 o mayor.
- `drop_and_one_hot_encode_red_wine`: Codifica 'Red Wine' como one-hot y elimina la columna 'variety'.
- `remove_newlines_carriage_returns`: Elimina saltos de línea y retornos de carro de las columnas de texto.
- `convert_ratings_to_int`: Convierte la columna 'rating' de float a entero.

### Ejemplos

1. Eliminar la columna 'notes':
        ```sh
        python main.py drop_notes
        ```

2. Seleccionar filas con altas calificaciones:
        ```sh
        python main.py select_high_ratings
        ```

3. Codificar 'Red Wine' como one-hot y eliminar la columna 'variety':
        ```sh
        python main.py drop_and_one_hot_encode_red_wine
        ```

4. Eliminar saltos de línea y retornos de carro de las columnas de texto:
        ```sh
        python main.py remove_newlines_carriage_returns
        ```

5. Convertir la columna 'rating' a entero:
        ```sh
        python main.py convert_ratings_to_int
        ```

## Datos

Los datos utilizados en este proyecto están almacenados en archivos CSV ubicados en el directorio `workshop`. El archivo principal es `train.csv`, que contiene las siguientes columnas:

- `notes`: Notas de texto sobre los datos.
- `ratings`: Calificaciones numéricas de los datos.
- `variety`: La variedad de los datos (por ejemplo, 'Red Wine').

Los datos transformados se guardan en `transformed_train.csv` después de aplicar los comandos de la CLI.

## Contribución

¡Las contribuciones son bienvenidas! Por favor, sigue estos pasos para contribuir:

1. Haz un fork del repositorio.
2. Crea una nueva rama (`git checkout -b feature-branch`).
3. Haz tus cambios.
4. Haz commit de tus cambios (`git commit -m 'Añadir nueva funcionalidad'`).
5. Haz push a la rama (`git push origin feature-branch`).
6. Abre un pull request.

## Licencia

Este proyecto está licenciado bajo la Licencia MIT. Ver el archivo [LICENSE](../LICENSE) para más detalles.

</details>

## Limpieza

### 1. Elimina tu Codespace

⏳ **~1min**

Antes de eliminar, si lo deseas, puedes enviar tus cambios. Recuerda que los repositorios del taller también son temporales.

Ve a [https://github.com/codespaces](https://github.com/codespaces) y encuentra tu Codespace en ejecución para eliminarlo.

## Recursos Adicionales

Si deseas aprender más sobre cómo usar GitHub Copilot, consulta estos recursos:

* [Documentación de GitHub Copilot](https://docs.github.com/es/copilot)
* [Serie de videos de VS Code: GitHub Copilot](https://www.youtube.com/playlist?list=PLj6YeMhvp2S7rQaCLRrMnzRdkNdKnMVwg)
* [Blog: Mejores prácticas para guiar a Copilot](http://blog.pamelafox.org/2023/06/best-practices-for-prompting-github.html)

Consulta también la [ruta de aprendizaje GitHub Foundations](https://learn.microsoft.com/es-es/training/paths/github-foundations/) para más recursos sobre GitHub y GitHub Copilot.

## Avisos Legales
 
Microsoft y cualquier colaborador te otorgan una licencia para la documentación de Microsoft y otros contenidos en este repositorio bajo la [Licencia Pública Internacional Creative Commons Attribution 4.0](https://creativecommons.org/licenses/by/4.0/legalcode.es),
consulta [LICENSE](LICENSE) y te otorgan una licencia para cualquier código en el repositorio bajo la [Licencia MIT](https://opensource.org/licenses/MIT), consulta
[LICENSE-CODE](LICENSE-CODE)
 
Microsoft, Windows, Microsoft Azure y/u otros productos y servicios de Microsoft mencionados en la documentación pueden ser marcas comerciales o marcas registradas de Microsoft en Estados Unidos y/u otros países. Las licencias para este proyecto no te otorgan derechos para usar nombres, logotipos o marcas comerciales de Microsoft. Las directrices generales de marcas comerciales de Microsoft pueden encontrarse en http://go.microsoft.com/fwlink/?LinkID=254653.
 
La información de privacidad puede encontrarse en https://privacy.microsoft.com/es-es/
 
Microsoft y cualquier colaborador se reservan todos los demás derechos, ya sea bajo sus respectivos derechos de autor, patentes, o marcas comerciales, sea por implicación, impedimento o de otro modo. 