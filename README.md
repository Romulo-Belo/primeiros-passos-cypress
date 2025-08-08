Projeto de Testes Automatizados com Cypress
Este repositório contém testes automatizados end-to-end (e2e) desenvolvidos com Cypress para verificar fluxos de login em aplicações web. O objetivo é garantir a funcionalidade e a estabilidade desses fluxos críticos.

Estrutura do Projeto
A estrutura de diretórios segue a convenção padrão do Cypress, organizada para fácil navegação e manutenção:


Pré-requisitos
Para rodar este projeto, você precisará ter o Node.js e o npm (Node Package Manager) instalados em sua máquina. Você pode baixá-los em nodejs.org.

Instalação
Siga os passos abaixo para configurar o ambiente e instalar as dependências:

Clone o Repositório:

git clone [URL_DO_SEU_REPOSITORIO]
cd [nome-do-seu-repositorio]

Instale as Dependências do Cypress:

npm install

Este comando instalará o Cypress e outras dependências listadas no package.json.

Como Rodar os Testes
Você pode executar os testes de duas maneiras principais:

1. Modo Interativo (Cypress Test Runner)
Este modo é ideal para desenvolvimento e depuração, pois abre a interface gráfica do Cypress, permitindo que você veja os testes sendo executados em tempo real.

npx cypress open

No Cypress Test Runner, selecione E2E Testing e, em seguida, escolha o navegador de sua preferência. Na lista de especificações, clique em login.spec.cy.js para iniciar a execução do teste.

2. Modo Headless (Linha de Comando)
Este modo é recomendado para integração contínua (CI) ou para execuções rápidas, pois executa os testes em segundo plano sem a interface gráfica e gera um relatório.

npx cypress run

Cenários de Teste
O arquivo cypress/e2e/login.spec.cy.js contém os seguintes cenários de teste de login:

Teste de Login no Orange HRM
Descrição: Este teste automatiza o processo de login na plataforma Orange HRM.

Ações:

Visita a URL: https://opensource-demo.orangehrmlive.com/web/index.php/auth/login

Preenche o campo de usuário com "Admin".

Preenche o campo de senha com "admin123".

Clica no botão de login.

Verifica se a URL mudou para o dashboard (/web/index.php/dashboard/index).

Verifica se o texto "Dashboard" está visível no cabeçalho.

Teste de Login no Meu Big Box
Descrição: Este teste automatiza o processo de autenticação na aplicação Meu Big Box.

Ações:

Visita a URL: https://meubigbox.com.br/v1/apps/auth-do-cliente/autenticacao-id?FbOcCl1d=pAZXH0bghVHzW0CMTEa4adftoEimzFaF032RSLMhiZi

Preenche o campo de CPF com um valor de teste (01015025161).

Clica no botão para continuar a autenticação.

Recomendações e Melhorias Futuras
Para tornar este projeto de testes mais robusto e eficiente, considere as seguintes melhorias:

Seletores Mais Robustos: Os seletores cy.get(':nth-child(...)') são frágeis e podem quebrar se a estrutura HTML da página mudar. É altamente recomendável substituí-los por seletores mais estáveis, como:

id (ex: cy.get('#meuId'))

data-testid (ex: cy.get('[data-testid="campo-usuario"]'))

Classes CSS únicas e semânticas (ex: cy.get('.campo-usuario'))

Remoção de cy.wait(): O uso de cy.wait(tempo) não é uma prática recomendada, pois retarda desnecessariamente os testes e pode causar falhas em ambientes com desempenho diferente. Prefira usar asserções para esperar por elementos (cy.get('elemento').should('be.visible')) ou por requisições de rede (cy.intercept()).

Utilização de Fixtures: Para dados de login e outros valores de teste, utilize Cypress.fixture() para armazená-los em arquivos separados (cypress/fixtures/). Isso torna os testes mais limpos e fáceis de manter.

Testes Negativos: Adicione cenários de teste para verificar comportamentos esperados com credenciais inválidas ou campos vazios.

Page Objects: Para projetos maiores, considere implementar o padrão Page Object Model (POM) para organizar melhor os seletores e as ações da página, tornando o código mais legível e reutilizável.

Integração Contínua (CI): Configure um pipeline de CI/CD para executar os testes automaticamente a cada push ou pull request, garantindo a qualidade do código de forma contínua.
