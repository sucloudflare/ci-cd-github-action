  <header>
        <h1>Projeto Simples com CI/CD no GitHub Actions</h1>
    </header>

  <main>
        <section>
            <h2>Visão Geral</h2>
            <p>Este é um projeto básico que utiliza HTML e CSS para criar uma página web simples, com integração de CI/CD (Continuous Integration/Continuous Delivery) utilizando GitHub Actions. O pipeline verifica automaticamente erros de sintaxe em arquivos HTML e CSS.</p>
        </section>

  <section>
            <h2>Índice</h2>
            <ol>
                <li>Visão Geral</li>
                <li>Estrutura do Projeto</li>
                <li>Configuração do Pipeline CI/CD</li>
                <li>Instalação Local</li>
                <li>Como Funciona o Pipeline</li>
                <li>Contribuições</li>
                <li>Licença</li>
            </ol>
        </section>

 <section>
     <h2>Estrutura do Projeto</h2>
         <pre><code>project-root/
├── index.html          # Página HTML principal
├── styles.css          # Arquivo de estilos CSS
└── .github/
    └── workflows/
        └── ci-cd.yml   # Pipeline de CI/CD configurado para o GitHub Actions
            </code></pre>
        </section>

   <section>
            <h2>Configuração do Pipeline CI/CD</h2>
            <p>O arquivo <code>ci-cd.yml</code>, localizado na pasta <code>.github/workflows/</code>, é usado para configurar o GitHub Actions e executar o linting de arquivos HTML e CSS automaticamente.</p>
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
            <h2>Instalação Local</h2>
            <p>Clone este repositório:</p>
            <pre><code>git clone https://github.com/sucloudflare/ci-cd-github-action/tree/main</code></pre>
            <p>Navegue até a pasta do projeto:</p>
            <pre><code>cd ci-cd-github-action</code></pre>
            <p>Se quiser rodar o projeto localmente, basta abrir o arquivo <code>index.html</code> no navegador.</p>
        </section>

        <section>
            <h2>Como Funciona o Pipeline</h2>
            <p><strong>Triggers:</strong> O pipeline é acionado sempre que um <strong>push</strong> ou <strong>pull request</strong> é feito na branch <code>main</code>.</p>
            <p><strong>Instalação das Dependências:</strong> O Node.js é configurado e as dependências <code>htmlhint</code> (para validar HTML) e <code>stylelint</code> (para validar CSS) são instaladas via npm.</p>
            <p><strong>Linting:</strong></p>
            <ul>
                <li><code>HTMLHint</code> é executado para verificar erros de sintaxe nos arquivos HTML.</li>
                <li><code>Stylelint</code> verifica o código CSS para garantir conformidade com as boas práticas de codificação.</li>
            </ul>
            <p><strong>Resultado:</strong> Se houver erros, o pipeline falhará, e os detalhes do erro poderão ser vistos no log do GitHub Actions. Se não houver erros, o pipeline será concluído com sucesso.</p>
        </section>

        <section>
            <h2>Contribuições</h2>
            <p>Contribuições são bem-vindas! Sinta-se à vontade para abrir <strong>issues</strong> ou enviar <strong>pull requests</strong> para melhorias no projeto.</p>
        </section>

        <section>
            <h2>Licença</h2>
            <p>Este projeto está licenciado sob a <strong>MIT License</strong>.</p>
        </section>
   </main>

   <footer>
        <p>&copy; 2024 Meu Projeto Simples com CI/CD no GitHub Actions</p>
    </footer>
