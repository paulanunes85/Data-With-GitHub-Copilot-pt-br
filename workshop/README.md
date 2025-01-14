<h1 align="center">Dados + GitHub Copilot para soluções avançadas de dados</h1>
<em align="center">A combinação perfeita ™</em>

<h5 align="center">Elaborado por @pamelafox @alfredodeza</h5>
<h5 align="center">Revisão para Português Brasil @paulanunes85</h5>

## Introdução

Este repositório contém o código-fonte completo do workshop. Você seguirá o guia passo a passo abaixo, completando todas as etapas enquanto trabalha com dados e o GitHub Copilot dentro do Codespaces.

> [!NOTA]
> Este repositório tem como objetivo apresentar vários recursos do **GitHub Copilot**, como **Copilot Chat** e **chat inline**. Portanto, os guias passo a passo abaixo contêm a descrição geral do que precisa ser feito, e o Copilot Chat ou o chat inline podem ajudar você a gerar os comandos necessários.
>
> Cada etapa (quando aplicável) também contém um `Cheatsheet` que pode ser usado para validar as sugestões do Copilot em relação ao comando correto.
>
> 💡 Experimente diferentes prompts para ver como isso afeta a precisão das sugestões do GitHub Copilot. Por exemplo, ao usar o chat inline, você pode usar um prompt adicional para refinar a resposta sem precisar refazer todo o prompt.

## Funcionalidades do Projeto de Dados

Neste workshop, você trabalhará com dados de um arquivo CSV incluído neste repositório, além de um script em Python que interage com esse arquivo CSV. Aqui estão algumas das funcionalidades do projeto:

1. Consumir um dataset em CSV e realizar transformações
2. Identificar e implementar validações
3. Criar uma ferramenta de linha de comando que pode ser usada em ambientes de CI/CD

## Preparação

Este repositório está pronto para Codespaces e já está pré-configurado para que você tenha todas as dependências instaladas, incluindo as extensões do Visual Studio Code necessárias para trabalhar com GitHub Copilot e Python:

- GitHub Copilot
- Extensão Python
- Dependências Python pré-instaladas com um Ambiente Virtual ativado

> [!NOTA]
> Se você estiver usando este repositório na sua conta ou em uma organização que não seja do GitHub Universe, pode haver custos ou consumo de sua cota gratuita para Codespaces.

### 1. Crie um novo repositório a partir deste template

Progresso: [🟢⚪⚪⚪⚪⚪⚪⚪⚪⚪⚪⚪] 1/12 (8%)

⏳ **~2min**

- Clique em `Use this template` :point_right: `Create a new repository`
- Defina o proprietário como a organização GitHub Workshop: `githubuniverseworkshop`
- Dê um nome
- Defina a visibilidade como `Private`
- Clique em `Create repository`

### 2. Crie um Codespace usando o template fornecido

Progresso: [🟢🟢⚪⚪⚪⚪⚪⚪⚪⚪⚪⚪] 2/12 (16%)

⏳ **~3min**

- No repositório recém-criado, clique em `Code` :point_right: `Codespaces` :point_right: `[ellipsis menu]` :point_right: `New with options` :point_right: _Certifique-se de que `Dev container configuration` esteja definido como `Default project configuration`_ :point_right: `Create codespace`

- ❗Se você estiver tendo problemas para iniciar o Codespace, também pode clonar o repositório e continuar do seu IDE:

    ```sh
    git clone https://github.com/<SEU_NAMESPACE>/<SEU_REPO>.git
    cd <SEU_REPO>
    ```

    > 📝 **Nota:** Não há necessidade de enviar (push) as alterações de volta ao repositório durante o workshop

### 3. Verifique se o Python está instalado e configurado corretamente

Progresso: [🟢🟢🟢⚪⚪⚪⚪⚪⚪⚪⚪⚪] 3/12 (25%)

⏳ **~2min**

- Use o palette de comandos para abrir o terminal (procure por "Create new terminal")
- Execute `which python` e certifique-se de que ele aponte para o Ambiente Virtual (`home/vscode/venv/bin/python`)
- Execute `which pip` e confirme que ele também aponte para o Ambiente Virtual (`home/vscode/venv/bin/pip`)

### 4. Execute os scripts Python

Progresso: [🟢🟢🟢🟢⚪⚪⚪⚪⚪⚪⚪⚪] 4/12 (33%)

⏳ **~2min**

- Execute o script `main.py` e confirme se não ocorrem erros:

    ```shell
    python main.py
    ```

- Execute o script `check.py` e confirme se não ocorrem erros:

    ```shell
    python check.py
    ```

    Deve haver algumas linhas de OK e outras de FAIL:

    ```shell
    [OK  ]   verify_drop_notes
    [FAIL]   verify_high_ratings - Not all ratings are 90 or higher.
    [FAIL]   verify_one_hot_encoding - The 'Red Wine' column was not one-hot encoded correctly.
    [OK  ]   verify_remove_newlines_carriage_returns
    [FAIL]   verify_ratings_to_int - The 'ratings' column was not converted to integers correctly.
    ```

### 5. Abra os arquivos relevantes

Progresso: [🟢🟢🟢🟢🟢⚪⚪⚪⚪⚪⚪⚪] 5/12 (41%)

⏳ **~2min**

O GitHub Copilot se beneficia de ter contexto disponível. Uma forma de aprimorar o contexto é abrir os arquivos relevantes.

- Abra os arquivos `main.py`, `check.py`, `train.csv` e `transformed_train.csv`


## Desenvolvimento

### 1. Veja quanto você pode aprender sobre o projeto e os dados

Progresso: [🟢🟢🟢🟢🟢🟢⚪⚪⚪⚪⚪⚪] 6/12 (50%) - Metade do caminho!

⏳ **~5min**

- Abra o GitHub Copilot Chat
- Use o agente `@workspace` para perguntar ao Copilot o que os arquivos `main.py` e `check.py` fazem
- Novamente, com o agente `@workspace`, pergunte ao Copilot qual é a natureza dos dados com os quais você vai trabalhar

#### 2. Corrija a função de avaliações altas

Progresso: [🟢🟢🟢🟢🟢🟢🟢⚪⚪⚪⚪⚪] 7/12 (58%)

⏳ **~3min**

- Em `main.py`, localize a função `select_high_ratings()`
- Posicione seu cursor na assinatura ou em algum lugar do corpo da função
- Abra o chat inline com `Ctrl-i` ou `Cmd-i` (no Mac)
- Prefixe seu prompt com o comando `/explain`
- Pergunte por que essa função pode não estar funcionando e implemente as possíveis correções
- Recrie o arquivo `transformed_train.csv` executando `python main.py`
- Verifique a correção executando `python check.py`, certificando-se de que essa função retorne um `OK`

<details>
<summary>Cheatsheet</summary>

##### Prompt

```sh
/explain why this function might not be working correctly?

##### Output esperado

```sh
Based on the provided code, there are a few potential reasons why the `select_high_ratings` function might not be working correctly:

1. Erro de digitação no Nome da Coluna: A função verifica se o nome da coluna 'ratings' existe em df.columns. Se houver um erro de digitação, como 'rating' em vez de 'ratings', a condição `if 'ratings' in df.columns`
```

</details>

> [!NOTA]
> Sinta-se à vontade para usar o GitHub Copilot Chat para implementar ou confirmar a correção

#### 3. Fix the one-hot encoding problem

Progresso: [🟢🟢🟢🟢🟢🟢🟢🟢⚪⚪⚪⚪] 8/12 (66%)

⏳ **~3min**
- Selecione a função `drop_and_one_hot_encode_red_wine()` e abra o chat inline (Ctrl-i/ Cmd-i)  
- Use o comando `/fix` para solicitar ao GitHub Copilot que sugira uma possível correção  
- Gere novamente o arquivo `transformed_train.csv` executando `python main.py`  
- Verifique a correção executando `python check.py`, certificando-se de que a função retorne `OK`  

<details>
<summary>Cheatsheet</summary>

##### Prompt

```sh
This function is not doing one-hot encoding on the variety column
```

##### Expected output

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

#### 4. Corrija a conversão da coluna de avaliação para inteiro

Progresso: [🟢🟢🟢🟢🟢🟢🟢🟢🟢⚪⚪⚪] 9/12 (75%)

⏳ **~3min**

- Se o check `verify_ratings_to_int` já estiver "OK", o Copilot pode ter solucionado o problema. Caso contrário, siga os passos.  
- Selecione a função `convert_ratings_to_int()` e abra o chat inline (Ctrl-i / Cmd-i).  
- Use o comando `/explain` para perguntar ao GitHub Copilot por que a função pode não funcionar corretamente.  
- Identifique o problema e implemente a correção.  
- Regere `transformed_train.csv` executando `python main.py`.  
- Verifique a correção executando `python check.py` e certifique-se de que a função retorna `OK`.  

<details>
<summary>Cheatsheet</summary>

##### Prompt

```sh
Esta função não está convertendo as avaliações para inteiros
```

##### Saída Esperada

```python
def convert_ratings_to_int(df):
    """
    Converte a coluna 'rating' de float para inteiro.
    """
    if 'rating' in df.columns:
        df['rating'] = df['rating'].astype(int)
    return df
```

</details>
## Testes

Um projeto Python robusto pode se beneficiar de testes. Você adicionará alguns testes unitários e descobrirá mais sobre como executar esses testes com a ajuda do GitHub Copilot.

Certifique-se de ter o terminal aberto executando o comando palette e digitando `toggle terminal`.

### 1. Teste sua CLI

Progresso: [🟢🟢🟢🟢🟢🟢🟢🟢🟢🟢⚪⚪] 10/12 (83%)

⏳ **~5min**

- Este projeto tem o Pytest test runner e framework pré-instalados, certifique-se de que está disponível executando `pytest --version`.
- Execute os testes enquanto estiver no diretório `workshop` usando o seguinte comando: `pytest -v`.

A saída deve mostrar uma falha.

#### 2. Corrija o teste com falha

Progresso: [🟢🟢🟢🟢🟢🟢🟢🟢🟢🟢🟢⚪] 11/12 (91%)

⏳ **~5min**

- Selecione a saída no terminal e cole-a no GitHub Copilot Chat, prefixando com uma solicitação de correção e explicação.
- Use a saída do chat para implementar uma correção em `test_main.py`.

<details>
<summary>Cheatsheet</summary>

##### Prompt

```sh
Corrija o teste e explique sua correção:
// Copie e cole a saída do terminal aqui
```

##### Saída Esperada

O erro ocorre porque a função drop_notes provavelmente está modificando o DataFrame no local, em vez de retornar um novo DataFrame com a coluna 'notes' removida. Para corrigir o teste, precisamos garantir que a função drop_notes retorne um novo DataFrame sem a coluna 'notes' e, em seguida, verificar as colunas desse novo DataFrame.

Aqui está a função de teste corrigida:

```python
def test_drop_notes_column_dropped():
    # Crie um DataFrame de amostra com a coluna 'notes'
    df = pd.DataFrame({'A': [1, 2, 3], 'B': [4, 5, 6], 'notes': ['note1', 'note2', 'note3']})

    # Chame a função drop_notes e obtenha o resultado
    result = main.drop_notes(df)
    
    # Verifique se a coluna 'notes' no DataFrame resultante foi removida
    columns = result.columns.to_list()
    assert columns == ['A', 'B']
```

Armazenando o resultado da função drop_notes em uma nova variável e verificando suas colunas, garantimos que o teste verifique corretamente o comportamento da função.

</details>

#### 3. Adicione testes para a função de one hot encoding

Progresso: [🟢🟢🟢🟢🟢🟢🟢🟢🟢🟢🟢🟢] 12/12 (100%) - 🎉 Celebre!

⏳ **~5min**

- Certifique-se de que o `python check.py` tenha todas as saídas OK, caso contrário, esta etapa pode não funcionar.
- Selecione a função `drop_and_one_hot_encode_red_wine` em `main.py`.
- Abra o chat inline com `Ctrl-i`/`Cmd-i`.
- Use o comando `/tests` para obter sugestões de testes.
- Revise a saída, aceite-a e verifique com o comando `pytest -v`. Todos os testes devem passar, e você deve ter mais testes do que antes. Às vezes, o Copilot indenta os testes sugeridos incorretamente (aninhando-os dentro de uma função de teste existente), então certifique-se de que os testes estão corretamente indentados antes de executá-los.

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
# CLI de Manipulação de DataFrame

Este projeto fornece uma interface de linha de comando (CLI) para manipular um DataFrame usando várias operações. A CLI é construída usando a biblioteca padrão do Python e não requer dependências externas.

## Índice

- [Instalação](#instalação)
- [Uso](#uso)
    - [Comandos](#comandos)
- [Dados](#dados)
- [Contribuição](#contribuição)
- [Licença](#licença)

## Instalação

1. Clone o repositório:
        ```sh
        git clone https://github.com/seuusuario/seu-repo.git
        cd seu-repo
        ```

2. Configure um ambiente virtual:
        ```sh
        python3 -m venv venv
        source venv/bin/activate
        ```

3. Instale os pacotes necessários:
        ```sh
        pip install -r workshop/requirements.txt
        ```

## Uso

Para usar a CLI, navegue até o diretório `workshop` e execute o script `main.py` com o comando desejado.

### Comandos

- `drop_notes`: Remove a coluna 'notes' do DataFrame.
- `select_high_ratings`: Seleciona linhas onde a coluna 'rating' é 90 ou maior.
- `drop_and_one_hot_encode_red_wine`: Codifica 'Red Wine' como one-hot e remove a coluna 'variety'.
- `remove_newlines_carriage_returns`: Remove quebras de linha e retornos de carro das colunas de string.
- `convert_ratings_to_int`: Converte a coluna 'rating' de float para inteiro.

### Exemplos

1. Remover a coluna 'notes':
        ```sh
        python main.py drop_notes
        ```

2. Selecionar linhas com altas avaliações:
        ```sh
        python main.py select_high_ratings
        ```

3. Codificar 'Red Wine' como one-hot e remover a coluna 'variety':
        ```sh
        python main.py drop_and_one_hot_encode_red_wine
        ```

4. Remover quebras de linha e retornos de carro das colunas de string:
        ```sh
        python main.py remove_newlines_carriage_returns
        ```

5. Converter a coluna 'rating' para inteiro:
        ```sh
        python main.py convert_ratings_to_int
        ```

## Dados

Os dados usados neste projeto estão armazenados em arquivos CSV localizados no diretório `workshop`. O arquivo principal é `train.csv`, que contém as seguintes colunas:

- `notes`: Notas de texto sobre os dados.
- `ratings`: Avaliações numéricas dos dados.
- `variety`: A variedade dos dados (por exemplo, 'Red Wine').

Os dados transformados são salvos em `transformed_train.csv` após a aplicação dos comandos da CLI.

## Contribuindo

Contribuições são bem-vindas! Por favor, siga estes passos para contribuir:

1. Faça um fork do repositório.
2. Crie um novo branch (`git checkout -b feature-branch`).
3. Faça suas alterações.
4. Faça commit das suas alterações (`git commit -m 'Adicionar nova funcionalidade'`).
5. Faça push para o branch (`git push origin feature-branch`).
6. Abra um pull request.

## Licença

Este projeto está licenciado sob a Licença MIT. Veja o arquivo [LICENSE](../LICENSE) para mais detalhes.

</details>

## Clean-up

### 1. Delete your Codespace

⏳ **~1min**

Before deleting, if you wish, you can push your changes. Remember workshop repositories are temporary too.

Go to [https://github.com/codespaces](https://github.com/codespaces) and find your current running Codespace and delete it.

## Additional resources

If you want to learn more about using GitHub Copilot, check out these resources:

* [GitHub Copilot Documentation](https://docs.github.com/copilot)
* [VS Code video series: GitHub Copilot](https://www.youtube.com/playlist?list=PLj6YeMhvp2S7rQaCLRrMnzRdkNdKnMVwg)
* [Blog: Best practices for prompting Copilot](http://blog.pamelafox.org/2023/06/best-practices-for-prompting-github.html)

Also check out the [GitHub Foundations learning path](https://learn.microsoft.com/training/paths/github-foundations/) for more resources on GitHub and GitHub Copilot.
