# 🐧 Caderno Temático Inteligente: Administração Linux e Automação Avançada com Python

## 📝 Contexto e Objetivos
Este repositório foi desenvolvido como a entrega final para o Desafio de Projeto da plataforma [DIO.me](https://www.dio.me/). O objetivo principal foi criar e consolidar um **Caderno Temático de Estudos** utilizando a inteligência artificial do **Google NotebookLM**, atuando como um parceiro analítico no domínio de infraestrutura, sistemas operacionais e automação de processos (DevOps).

### Objetivos de Estudo:
* Aprofundar os conhecimentos em administração de sistemas GNU/Linux, manipulação de processos e segurança de servidores.
* Explorar o ecossistema Python (módulos nativos e bibliotecas de alto nível) para substituir rotinas manuais e scripts complexos de Shell.
* Dominar a Engenharia de Prompts de forma prática, analisando criticamente as respostas geradas a partir de uma base de conhecimento curada.

---

## 📚 Curadoria de Fontes (Base de Conhecimento do NotebookLM)
Para municiar o NotebookLM com o mais alto rigor técnico, foram selecionadas e carregadas as seguintes fontes públicas, manuais oficiais e repositórios de engenharia:

1.  **Adventures with the Linux Command Line (William Shotts):** Manual focado no uso avançado do terminal Linux, automação em Bash e gerenciamento de arquivos.
2.  **GuiaFoca GNU/Linux:** Referência nacional em documentação didática sobre infraestrutura, configuração e segurança de servidores Linux.
3.  **Documentação Oficial de Módulos Core e Ferramentas Multiplataforma:**
    * *Módulo Subprocess (Python Standard Library):* Guias técnicos e análises de segurança (`Codiga` e `Stack Overflow`) focados na execução segura de comandos de sistema.
    * *Biblioteca psutil:* Documentação oficial de monitoramento e perfilamento de recursos de hardware (CPU, memória, discos e redes).
    * *Biblioteca watchdog:* Artigos técnicos (`JCharisTech` e discussões no `Reddit`) sobre monitoramento reativo de eventos no sistema de arquivos.

---

## 🧠 Engenharia de Prompts e "Cicatrizes" (Troubleshooting)
Esta seção registra as interações estratégicas realizadas com o NotebookLM para extrair o melhor nível de resposta técnica, documentando os erros e refinamentos.

### ❌ Teste de Prompt 1: Abordagem Ingênua (Resultado Superficial)
* **Prompt:** *Como rodar comandos do Linux dentro do Python?*
* **Resposta da IA:** Sugeriu o uso simples do módulo `subprocess` ou `os.system` sem detalhar boas práticas.
* **Cicatriz/Dificuldade:** A resposta falhou em demonstrar os riscos críticos de segurança que envolvem o uso do Shell no ambiente de produção.

### 🎯 Teste de Prompt 2: Engenharia de Prompt Estruturada (Resultado "Nota 10")
* **Prompt (Restrito pelas Fontes):** *Atuando como um Engenheiro DevOps Sênior focado em segurança (CWE-78), analise os artigos da Codiga e a documentação do subprocess presentes nas fontes. Explique por que o argumento 'shell=True' deve ser bloqueado em rotinas de integração contínua (CI/CD) e forneça o padrão correto utilizando listas/vetores de argumentos para o comando 'ls -l'.*
* **Resposta da IA:** Apresentou uma justificativa sólida explicando que o `shell=True` expõe o sistema a ataques de injeção de comandos. Entregou o código estruturado de forma segura:
    ```python
    import subprocess
    # Forma correta e segura de execução sem invocar o shell do SO
    subprocess.run(["ls", "-l"], check=True)
    ```
* **Lição Aprendida:** Restringir o escopo da IA citando as fontes específicas inseridas no caderno e exigir uma justificativa pautada em vulnerabilidades reais do mercado altera completamente a maturidade da resposta obtida.

---

## 🚀 Miniguia de Estudo (Entrega Final)

### 1. Resumos Estruturados do Aprendizado

#### 🔒 Segurança no Módulo Subprocess
A engenharia de automação moderna exige a erradicação do Shell em chamadas do módulo `subprocess`. Ao utilizar strings puras combinadas com `shell=True`, abre-se espaço para manipulação maliciosa de argumentos. A recomendação padrão é estruturar os argumentos sempre em formato de listas e vetores estritos, impedindo que caracteres especiais de controle do Shell sejam interpretados.

#### 📊 Monitoramento de Performance com psutil
Diferente dos comandos nativos do Linux (como `top` e `ps`), a biblioteca `psutil` abstrai chamadas de baixo nível e fornece uma API multiplataforma em Python para coleta de métricas de telemetria. Funções como `psutil.virtual_memory()` e `psutil.net_io_counters()` coletam dados de uso em bytes, permitindo construir dashboards de monitoramento robustos e scripts automáticos de alerta de consumo de hardware.

#### 👁️ Monitoramento do Sistema de Arquivos com watchdog
Para criar rotinas automatizadas que reagem a modificações em múltiplos diretórios de forma assíncrona, a biblioteca `watchdog` utiliza as APIs nativas do Kernel (como o `inotify` no Linux). Isso substitui loops infinitos ineficientes (polling) por um modelo baseado em eventos reais (criação, modificação ou deleção de arquivos), otimizando o uso de CPU.

---

### 2. Glossário de Conceitos Chave

* **Inotify:** Subsistema do Kernel Linux que monitora alterações no sistema de arquivos e notifica os aplicativos imediatamente.
* **psutil (Process and System Utilities):** Biblioteca open-source multiplataforma para recuperação de informações sobre processos em execução e utilização de hardware em Python.
* **CWE-78 (Command Injection):** Vulnerabilidade de segurança caracterizada pela neutralização incorreta de elementos especiais usados em um comando do Sistema Operacional.
* **Daemon / Worker:** Processo ou script que roda continuamente em segundo plano (background) aguardando eventos ou requisições para agir.
* **check_call / run:** Funções do módulo `subprocess` utilizadas para disparar processos garantindo que o interpretador Python lance uma exceção caso o comando termine com erro (retorno diferente de zero).

---

### 3. Prompts Reutilizáveis para Revisões Futuras

Salve e execute estes prompts dentro do seu NotebookLM para fixar os conceitos ou gerar simulações de desafios reais:

> 🖥️ **Prompt para Simulação de Entrevista DevOps:**
> *"Com base nas fontes fornecidas sobre administração de sistemas, aja como um tech lead de infraestrutura. Me faça 3 perguntas técnicas de nível intermediário sobre gerenciamento de processos no Linux e monitoramento usando psutil. Avalie minhas respostas com base estritamente no conteúdo das fontes."*

> 🚨 **Prompt para Troubleshooting de Código:**
> *"Analise os documentos técnicos do watchdog e psutil anexados e elabore um roteiro estruturado passo a passo de como eu deveria planejar um script em Python para monitorar uma pasta específica e disparar um alerta se o consumo de disco ultrapassar 85%."*

---

## 🛠️ Como Clonar e Replicar este Notebook
1. Acesse o [Google NotebookLM](https://notebooklm.google.com/notebook/5d66bba8-608e-4203-a93f-bf79777b2212).
2. Crie um novo projeto/caderno com o nome `Estudos Linux e Automação`.
3. Faça o upload dos artigos, manuais e PDFs listados na seção de [Curadoria de Fontes](#-curadoria-de-fontes).
4. Utilize os prompts refinados da seção de [Engenharia de Prompts](#-engenharia-de-prompts-e-cicatrizes-troubleshooting) para interagir com a base e dar continuidade aos seus estudos de administração de sistemas.
