# Lab_Azure_ML_AI_Search


**Nota:**
Esse laboratório foi realizado com base nas instruções do link a seguir: https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/11-ai-search.html

---

### **Criação do Recurso Azure AI Search**
1. Acesse o **Portal do Azure**.
2. Clique em **+ Create a resource**, pesquise por **Azure AI Search** e crie o recurso com as seguintes configurações:
   - **Subscription:** Sua assinatura do Azure.
   - **Resource group:** Selecione ou crie um grupo de recursos com um nome exclusivo.
   - **Service name:** Nome para o serviço.
   - **Location:** East US ou outra região disponível.
   - **Pricing tier:** Basic.
3. Clique em **Review + create** e, após a validação, selecione **Create**.
4. Após a conclusão da implantação, clique em **Go to resource**.

---

### **Criação do Recurso Azure AI Services**
1. Retorne à página inicial do portal.
2. Clique em **+ Create a resource** e pesquise por **Azure AI Services**.
3. Configure com as seguintes opções:
   - **Subscription:** Sua assinatura do Azure.
   - **Resource group:** O mesmo grupo de recursos do Azure AI Search.
   - **Region:** East US (ou região correspondente ao AI Search).
   - **Name:** Nome exclusivo.
   - **Pricing tier:** Standard S0.
4. Aceite os termos, clique em **Review + create** e, após a validação, selecione **Create**.
5. Aguarde a conclusão da implantação.

---

### **Criação do Azure Storage Account**
1. Retorne à página inicial do portal.
2. Clique em **+ Create a resource** e procure por **Storage Account**.
3. Configure com as seguintes opções:
   - **Subscription:** Sua assinatura do Azure.
   - **Resource group:** O mesmo usado anteriormente.
   - **Storage account name:** Nome único.
   - **Location:** East US.
   - **Performance:** Standard.
   - **Redundancy:** Locally redundant storage (LRS).
4. Clique em **Review + create** e, após a implantação, acesse o recurso.
5. No menu esquerdo, selecione **Configuration** e habilite **Allow Blob anonymous access**.

---

### **Criação do Container**
1. No menu esquerdo, clique em **Containers**.
2. Selecione **+ Container** e configure:
   - **Name:** coffeereviews.
   - **Public access level:** Container (anonymous read access).
3. Clique em **Create**.

---

### **Upload de Dados**
1. Baixe o arquivo compactado das avaliações de café em [este link](https://aka.ms/mslearn-coffee-reviews) e extraia os arquivos.
2. No portal do Azure, selecione o container **coffee-reviews**.
3. Clique em **Upload**, selecione todos os arquivos extraídos e clique em **Upload**.

---

### **Importação de Dados no Azure AI Search**
1. No portal do Azure, acesse o recurso **Azure AI Search**.
2. Na aba **Overview**, selecione **Import data**.
3. Configure:
   - **Data Source:** Azure Blob Storage.
   - **Data source name:** coffee-customer-data.
   - **Data to extract:** Content and metadata.
   - **Parsing mode:** Default.
   - **Connection string:** Escolha a conexão existente.
   - **Managed identity authentication:** None.
   - **Container name:** Preenchido automaticamente.
   - **Description:** Reviews for Fourth Coffee shops.
4. Clique em **Next: Add cognitive skills (Optional)**.

---

### **Adição de Habilidades Cognitivas**
1. Em **Attach AI Services**, selecione o recurso criado anteriormente.
2. Preencha:
   - **Skillset name:** coffee-skillset.
   - Ative **Enable OCR and merge all text into merged_content field**.
   - **Source data field:** merged_content.
   - **Enrichment granularity level:** Pages (5000 character chunks).
   - Selecione os campos:
     - **Extract location names:** locations.
     - **Extract key phrases:** keyphrases.
     - **Detect sentiment:** sentiment.
     - **Generate tags from images:** imageTags.
     - **Generate captions from images:** imageCaption.
   - **Knowledge Store:** Selecione o storage criado anteriormente.
   - Crie um novo container chamado **knowledge-store** com nível **Private**.

---

### **Personalização do Índice**
1. Selecione **Azure blob projections: Document**.
2. Altere o nome do índice para **coffee-index**.
3. Certifique-se de que a chave está como **metadata_storage_path**.
4. Clique em **Next: Create an indexer**.

---

### **Criação do Indexador**
1. Nomeie o indexador como **coffee-indexer**.
2. **Schedule:** Once.
3. Ative **Base-64 Encode Keys**.
4. Clique em **Submit**.

---

### **Realização de Consultas no Search Explorer**
1. Acesse **Azure AI Search > Search Explorer**.
2. Execute as seguintes consultas:
   - Todos os documentos: `search=*&$count=true`.
   - Filtrar por sentimentos negativos: `search=sentiment:'negative'`.
   - Filtrar por localizações: `search=locations:'Chicago'`.

---

Seguindo este passo a passo, você conseguirá realizar com sucesso uma pesquisa usando o Azure AI Search.

