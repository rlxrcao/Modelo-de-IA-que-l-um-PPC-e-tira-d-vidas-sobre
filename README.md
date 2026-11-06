Agente Assistente Acadêmico - IFNMG 🤖📚

Este repositório contém o Trabalho Prático Final da disciplina de Aplicações de Modelos de Linguagem Natural do Curso Técnico em Inteligência Artificial do CE-ADI/IFNMG.

O projeto implementa um Agente Assistente baseado em IA totalmente local, projetado para interagir com alunos do curso, responder dúvidas gerais, consultar o Projeto Pedagógico do Curso (PPC) via RAG e manter o contexto das conversas.

🚀 Funcionalidades (Features)

O agente atende a 5 requisitos arquiteturais complexos:

Guardrail de Entrada: Utiliza um modelo classificador na porta de entrada para detectar e bloquear tentativas de injeção de prompt (Prompt Injection) antes de acionar o LLM principal.

Sistema de Skills (Roteamento): O agente decide qual habilidade (Tool) carregar com base na intenção do aluno:

perguntas_simples: Lê um arquivo Markdown local para responder dúvidas básicas.

duvidas_ppc: Aciona o RAG para buscar regras específicas do curso.

quadro_de_disciplinas: Busca as disciplinas do módulo do aluno e formata em tabela.

RAG Agêntico (Retrieval-Augmented Generation): Busca semântica no documento PDF do curso (PPC_do_curso.pdf) utilizando embeddings e um banco de dados vetorial FAISS.

Memória de Curto Prazo: O agente mantém o histórico recente da conversa para entender perguntas de continuação (ex: "E se eu não alcançar essa nota?").

Memória de Longo Prazo: Utiliza Expressões Regulares (Regex) para identificar, extrair e salvar o nome e o módulo do aluno em um arquivo perfil_aluno.json, lembrando do usuário em interações futuras.

🧠 Modelos Utilizados (Hugging Face)

A arquitetura orquestra três modelos com funções específicas:

LLM Principal (Agente): Qwen/Qwen3.8-Flash-Next (Rodando com quantização de 4-bits via bitsandbytes para otimização de VRAM).

Embeddings (RAG): sentence-transformers/all-MiniLM-L6-v2 (Para vetorização do PDF).

Guardrail: guardion/ModernGuard-1 (Classificação de segurança e injeções).

🛠️ Tecnologias e Bibliotecas

transformers & torch (Inferência de Modelos)

langchain, langchain-community, langchain-huggingface (Orquestração e RAG)

faiss-cpu (Vector Store)

pypdf (Leitura de PDF)

bitsandbytes (Quantização)

⚙️ Como Executar

Recomenda-se a execução deste projeto no Goog

Recomenda-se a execução deste projeto no Google Colab utilizando um ambiente de execução com GPU (ex: T4 GPU) para garantir o processamento eficiente do LLM.

Clone o repositório ou faça upload do arquivo .ipynb para o Google Colab.

Certifique-se de que o arquivo PPC_do_curso.pdf esteja no diretório raiz de execução.

Instale as dependências executando o primeiro bloco do notebook:

pip install transformers torch accelerate bitsandbytes sentence-transformers faiss-cpu pypdf langchain langchain-community langchain-huggingface



Execute os blocos sequencialmente. O último bloco executará a rotina de testes demonstrando as conversas, bloqueio do guardrail e acionamento de ferramentas.

📝 Observações de Desenvolvimento

Durante o desenvolvimento, a otimização de memória foi um fator crucial. Modelos maiores não foram capazes de rodar no hardware disponível sem estourar o limite de VRAM (OOM). O Qwen3.8-Flash-Next com quantização NF4 (4-bits) apresentou o melhor equilíbrio: coube na memória da GPU, acionou as ferramentas corretamente e apresentou o menor índice de alucinação entre as alternativas testadas.

Desenvolvido por: Rafael Arueira
