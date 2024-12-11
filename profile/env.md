## Criar arquivo .env para armazenamento de variáveis sensíveis

### Descrição:
Atualmente, os projetos do CEPAG contêm informações sensíveis diretamente no código-fonte, como chaves de API, URLs de banco de dados, credenciais e outras configurações que devem ser protegidas. Para garantir a segurança e facilitar a manutenção, é necessário criar um arquivo `.env` no repositório para armazenar essas variáveis de forma segura.

### Tarefas:
- Criar um arquivo `.env` na raiz do projeto.
- Mover todas as variáveis sensíveis atualmente hardcoded no código-fonte para o arquivo `.env`.
- Garantir que o arquivo `.env` seja incluído no arquivo `.gitignore` para evitar o versionamento no repositório.
- Substituir as variáveis sensíveis no código por chamadas para as variáveis de ambiente, utilizando as funções adequadas para cada linguagem (por exemplo, `process.env` no Node.js ou `os.getenv` no Python).
- Documentar no README.md ou em outro local apropriado as instruções para configurar o arquivo `.env` no ambiente de desenvolvimento.

### Critérios de aceitação:
- Todas as variáveis sensíveis precisam ser removidas do código-fonte, no caso de projetos existentes já possuírem dados sensíveis.
- O arquivo `.env` deve estar presente no repositório local, mas não é versionado no repositório remoto.

### Notas adicionais:
- Avaliar o uso de bibliotecas para carregar variáveis de ambiente, como `dotenv` para Node.js ou `python-decouple` para Python.
- Caso necessário, auditar o histórico do repositório para verificar se variáveis sensíveis já foram expostas, removendo-as de commits anteriores se for o caso.

## Tutorial para criação e uso do arquivo .env

1. **Criar o arquivo .env automaticamente**
   - No terminal integrado do Visual Studio Code, execute o seguinte comando para criar o arquivo `.env` automaticamente:
     ```bash
     ni .env
     ```

2. **Adicionar variáveis ao arquivo .env**
   - Insira suas variáveis sensíveis no arquivo no formato `CHAVE=valor`. Exemplo:
     ```env
     DATABASE_URL=postgresql://usuario:senha@localhost:5432/nome_do_banco
     API_KEY=123456abcdef
     SECRET_KEY=minha_chave_secreta
     ```

3. **Adicionar variáveis ao arquivo .env.example**
   - No arquivo `.env.example`, inclua as chaves das variáveis, mas sem os valores, para que outros colaboradores saibam quais variáveis precisam ser configuradas:

     ```env
     DATABASE_URL=
     API_KEY=
     SECRET_KEY=
     ```

4. **Configurar o .gitignore**
   - Certifique-se de que o arquivo `.gitignore` inclua a seguinte linha para evitar o versionamento do `.env`:
  
     ```
     .env
     ```

5. **Carregar variáveis no código**
   - Dependendo da linguagem de programação, utilize a biblioteca apropriada para carregar as variáveis de ambiente.
     - **Node.js**: Instale a biblioteca `dotenv` e utilize o seguinte código no seu arquivo principal:
       ```javascript
       require('dotenv').config();
       const apiKey = process.env.API_KEY;
       ```
     - **Python**: Instale a biblioteca `python-decouple` e use o seguinte código:
       ```python
       from decouple import config
       api_key = config('API_KEY')
       ```

6. **Instruções para colaboradores**
   - Informe os colaboradores do projeto que eles precisam criar o próprio arquivo `.env` localmente com as variáveis necessárias. Eles podem usar o arquivo `.env.example` como modelo, preenchendo os valores correspondentes.

7. **Recriar o arquivo .env sempre que necessário**
   - Toda vez que for necessário recriar o arquivo `.env`, execute o comando abaixo no terminal do Visual Studio Code e depois insira as variáveis conforme o arquivo `.env.example`:
  
     ```bash
     ni .env
     ```

