  <header>
        <h1>Como Ativar GitHub Actions para Pipelines CI/CD</h1>
    </header>

  <main>
        <section>
            <h2>Visão Geral</h2>
            <p>O GitHub Actions permite automatizar fluxos de trabalho, como integração contínua (CI) e entrega contínua (CD), diretamente em seu repositório. Esta página explica como ativar e configurar pipelines no GitHub Actions para seu projeto.</p>
        </section>

  <section>
          <h2>Índice</h2>
            <ol>
                <li>Ativando GitHub Actions no Repositório</li>
                <li>Criando o Arquivo de Pipeline</li>
                <li>Configurando o Pipeline de CI/CD</li>
                <li>Executando o Pipeline</li>
                <li>Monitorando o Status do Pipeline</li>
            </ol>
        </section>

  <section>
            <h2>1. Ativando GitHub Actions no Repositório</h2>
            <p>Para ativar o GitHub Actions no seu repositório, siga os passos abaixo:</p>
            <ol>
                <li>Vá até seu repositório no GitHub.</li>
                <li>No menu superior, clique em <strong>Actions</strong>.</li>
                <li>Clique em <strong>Set up a workflow yourself</strong> ou escolha um modelo de workflow pré-definido.</li>
            </ol>
            <p>Isso criará automaticamente a pasta <code>.github/workflows</code> no seu repositório, onde os arquivos de configuração do pipeline serão armazenados.</p>
        </section>

   <section>
            <h2>2. Criando o Arquivo de Pipeline</h2>
            <p>Após ativar o GitHub Actions, você precisará criar um arquivo YAML que descreve as etapas do pipeline. O arquivo deve ser colocado no diretório <code>.github/workflows/</code>.</p>
            <p>Por exemplo, crie um arquivo chamado <code>ci-cd.yml</code> com o seguinte conteúdo:</p>
            <pre><code>name: CI/CD Pipeline for HTML/CSS

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  lint:
    runs-on: ubuntu-latest

 steps:
      - name: Checkout code
        uses: actions/checkout@v2

   - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'

      - name: Install dependencies
        run: |
          npm init -y
          npm install htmlhint stylelint stylelint-config-standard --save-dev

      - name: Lint HTML files
        run: npx htmlhint '**/*.html'

      - name: Lint CSS files
        run: |
          echo "module.exports = { extends: 'stylelint-config-standard' };" > .stylelintrc.js
          npx stylelint '**/*.css'
            </code></pre>
        </section>

        <section>
            <h2>3. Configurando o Pipeline de CI/CD</h2>
            <p>O arquivo <code>ci-cd.yml</code> define um pipeline que executa verificações de sintaxe (linting) em arquivos HTML e CSS. Ele é ativado sempre que há um <strong>push</strong> ou <strong>pull request</strong> na branch <code>main</code>.</p>
            <p>Configurações importantes:</p>
            <ul>
                <li><strong>on:</strong> Define quando o pipeline será ativado (por push ou pull request).</li>
                <li><strong>jobs:</strong> Define o trabalho a ser realizado no pipeline. Neste caso, o trabalho de "lint" é executado em um ambiente Ubuntu.</li>
                <li><strong>steps:</strong> Lista as etapas para realizar o linting no código HTML e CSS.</li>
            </ul>
        </section>

        <section>
            <h2>4. Executando o Pipeline</h2>
            <p>Depois de configurar o arquivo <code>ci-cd.yml</code>, o pipeline será executado automaticamente sempre que um novo <strong>push</strong> ou <strong>pull request</strong> for feito na branch principal (main).</p>
            <p>Para forçar a execução do pipeline, basta enviar qualquer alteração para a branch <code>main</code> usando os comandos:</p>
            <pre><code>git add .
git commit -m "Configuração de pipeline"
git push origin main
            </code></pre>
        </section>

   <section>
            <h2>5. Monitorando o Status do Pipeline</h2>
            <p>Você pode monitorar o progresso e o status do pipeline no GitHub:</p>
            <ol>
                <li>Vá até seu repositório no GitHub.</li>
                <li>Clique na aba <strong>Actions</strong>.</li>
                <li>Lá você verá a lista de execuções do pipeline, o status atual (concluído ou com falhas), e poderá inspecionar os logs detalhados de cada etapa.</li>
            </ol>
        </section>
    </main>

   <footer>
        <p>&copy; 2024 Tutorial de CI/CD com GitHub Actions</p>
    </footer>
