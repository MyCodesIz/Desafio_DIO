
# Azure Cognitive Search: Utilizando AI Search para Indexação e Consulta de Dados

## Introdução
O **Azure Cognitive Search** é um serviço de pesquisa hospedado na nuvem da Microsoft que permite indexação e busca inteligente em grandes volumes de dados. Com recursos de inteligência artificial (AI Search), ele permite a criação de experiências de busca mais relevantes e eficientes.

Este documento descreve os passos para configurar uma pesquisa utilizando o Azure Cognitive Search, além de insights, possibilidades de aplicação e aprendizados adquiridos no processo.

---

## Imagens

### ## Upload Documents to Azure Storage
![## Upload Documents to Azure Storage](./Imagens/storage-blob-1.png)
![## Upload Documents to Azure Storage](./Imagens/storage-blob-2.png)
![## Upload Documents to Azure Storage](./Imagens/6a-azure-container-upload-files-3.png)
![## Upload Documents to Azure Storage](./Imagens/azure-search-wizard-4.png)

## Passo a Passo para Configuração do Azure Cognitive Search

### 1. Criar um Serviço de Pesquisa no Azure
1. Acesse o [Portal do Azure](https://portal.azure.com/).
2. No menu lateral, clique em **Criar um recurso**.
3. Busque por **Azure Cognitive Search** e selecione a opção correspondente.
4. Clique em **Criar**.
5. Escolha um nome único para o serviço.
6. Defina a **Região** onde o serviço será hospedado.
7. Escolha o **Plano de Preços** (Free, Basic, Standard, etc.).
8. Confirme e clique em **Criar**.

### 2. Criar e Configurar um Índice
1. Acesse o serviço recém-criado no Portal do Azure.
2. Vá até a aba **Indexers** e clique em **Criar um índice**.
3. Defina um nome para o índice.
4. Configure os campos do índice (ex: ID, Nome, Descrição, Categoria, etc.).
5. Escolha o **Tipo de Dados** de cada campo.
6. Defina os atributos de pesquisa para cada campo:
   - `Retrievable`: Indica se o campo pode ser recuperado na consulta.
   - `Filterable`: Permite filtros nas pesquisas.
   - `Sortable`: Permite ordenação.
   - `Searchable`: Habilita a pesquisa textual completa.
   - `Facetable`: Permite categorização e filtros interativos.
7. Clique em **Criar** para finalizar.

### 3. Importar e Indexar Dados
1. Vá para a aba **Data Sources** e clique em **Criar um novo Data Source**.
2. Escolha a fonte dos dados (ex: Azure Blob Storage, Azure SQL Database, CosmosDB, etc.).
3. Configure as credenciais de acesso à fonte de dados.
4. Selecione o índice criado anteriormente.
5. Defina a frequência de indexação (manual ou automática).
6. Salve e execute a indexação.

### 4. Criar um Indexador (Opcional)
Se os dados forem dinâmicos e mudarem com frequência, criar um indexador pode automatizar a atualização dos índices.
1. Vá para a aba **Indexers** e clique em **Criar um indexador**.
2. Associe o indexador à fonte de dados e ao índice.
3. Defina a periodicidade da indexação.
4. Salve e execute o indexador.

### 5. Explorar um Índice no Azure AI Search (UI)
O **Azure AI Search** fornece uma interface gráfica para explorar e testar os dados indexados.
1. Acesse o serviço de pesquisa no Portal do Azure.
2. No menu lateral, clique em **Search Explorer**.
3. Selecione o índice que deseja explorar.
4. Utilize a interface para realizar buscas com diferentes filtros e parâmetros.
5. Visualize os resultados e ajuste a configuração do índice conforme necessário.
6. Utilize expressões de consulta para refinar os resultados.

### 6. Realizar Consultas no Índice via API
Uma vez que os dados foram indexados, podemos realizar buscas via API REST ou SDKs.

#### Exemplo de Consulta via API REST
```bash
GET https://<nome-do-servico>.search.windows.net/indexes/<nome-do-indice>/docs?search=palavra-chave&api-version=2020-06-30
api-key: <chave-de-api>
```

#### Exemplo de Consulta usando Python (SDK)
```python
from azure.search.documents import SearchClient
from azure.core.credentials import AzureKeyCredential

service_name = "<nome-do-servico>"
index_name = "<nome-do-indice>"
api_key = "<chave-de-api>"

search_client = SearchClient(endpoint=f"https://{service_name}.search.windows.net",
                             index_name=index_name,
                             credential=AzureKeyCredential(api_key))

results = search_client.search("palavra-chave")
for result in results:
    print(result)
```

---

## Insights e Possibilidades
### Aplicações que se Beneficiam do Azure Cognitive Search
- **E-commerce**: Melhor experiência de busca de produtos com filtros inteligentes.
- **Sistemas de Suporte**: Indexação e recuperação rápida de documentos e FAQs.
- **Análise de Dados**: Busca inteligente em grandes conjuntos de dados não estruturados.
- **Mídia e Entretenimento**: Pesquisa avançada em acervos de vídeos, imagens e áudio.
- **Compliance e Auditoria**: Busca de documentos internos para conformidade regulatória.

### Recursos Avançados
- **Habilidades Cognitivas**: Extração de entidades, tradução automática, OCR para imagens e mais.
- **Boosting e Relevância**: Ajuste de pesos para priorizar resultados mais importantes.
- **Integração com OpenAI**: Combinação com ChatGPT para buscas semânticas.
- **Suporte a Filtros e Facetas**: Melhor organização dos resultados de pesquisa.

---

## Aprendizados
- **Modelagem de Índice é Essencial**: A estrutura correta do índice impacta diretamente na performance e relevância dos resultados.
- **Otimização de Consultas**: Aplicar filtros, boosting e facetas melhora a experiência do usuário.
- **Indexação Contínua**: Criar indexadores para atualizar os dados periodicamente evita inconsistências.
- **Segurança e Controle de Acesso**: Definir permissões apropriadas para proteger os dados indexados.

---

## Conclusão
O **Azure Cognitive Search** é uma ferramenta poderosa para criar experiências de busca inteligentes e escaláveis. Combinando AI Search, indexação eficiente e consultas avançadas, ele possibilita melhorar significativamente a recuperação de informações em diversas aplicações.

Para mais detalhes, consulte a [documentação oficial](https://learn.microsoft.com/en-us/azure/search/).
