# ParentRAG-Rocketseat

Este projeto implementa um **sistema de busca inteligente (RAG – Retrieval-Augmented Generation)** com **LangChain**, **OpenAI** e **ChromaDB**.  
Com ele, é possível **carregar um PDF**, **dividir o texto em partes**, **criar embeddings vetoriais** e **realizar perguntas** para obter respostas com base no conteúdo do documento.

---

##  Tecnologias Utilizadas

-  **LangChain** — Framework de orquestração de LLMs  
-  **OpenAI API** — Geração de embeddings e respostas  
-  **ChromaDB** — Banco de vetores para busca semântica  
-  **PyPDFLoader** — Leitura e divisão de documentos PDF  

---

## Instalação

###  Clone o repositório

- git clone https://github.com/seuusuario/seurepositorio.git
- cd seurepositorio
###  Crie um ambiente virtual

- python -m venv .venv
- .venv\Scripts\activate    # Windows
- source .venv/bin/activate # Linux/Mac
### Instale as dependências

- pip install -r requirements.txt

### Configuração da Chave da OpenAI
- os.environ['OPENAI_API_KEY'] = "sua_chave_api_aqui"
##  Como Funciona o Código
### Carregamento do PDF

- loader = PyPDFLoader(pdf_link, extract_images=False)
- pages = loader.load_and_split()
### Divisão dos textos
- Usando dois níveis de divisão:

- child_splitter: pequenos trechos (chunk_size = 200)

- parent_splitter: blocos maiores (chunk_size = 4000)

### Criação do Vetorstore e Retriever

- vectorstore = Chroma(embedding_function=embeddings, persist_directory="childVectorDB")
- parent_document_retriever = ParentDocumentRetriever(
    vectorstore=vectorstore,
    docstore=store,
    child_splitter=child_splitter,
    parent_splitter=parent_splitter
)
### Criação do Prompt e Execução da Query

- TEMPLATE = """
  Escreva o seu template
  Query: {question}

  Context: {context}
"""
parent_chain_retrival.invoke("Escreva sua pergunta aqui")
