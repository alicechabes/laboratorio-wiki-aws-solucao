# 📚 Wiki Inteligente com IA Generativa na AWS

Projeto de arquitetura em nuvem desenvolvido para o desafio de projeto do bootcamp na **DIO**. O objetivo é transformar documentos não estruturados e dispersos em uma base de conhecimento consultável via linguagem natural usando serviços gerenciados da AWS.

---

## 🎯 Problema Resolvido

Empresas frequentemente possuem documentos importantes espalhados em diferentes formatos (PDFs nativos, imagens digitalizadas com manuscritos e planilhas/CSVs de CRM). Essa dispersão impede a consulta rápida e centralizada de informações. 

Esta solução automatiza a ingestão, o processamento de OCR, a organização de metadados e a busca semântica por meio de um pipeline de **RAG (Retrieval-Augmented Generation)** na AWS.

---

## 🏗️ Arquitetura da Solução

```text
[ Documentos Brutos ] (PDF, Imagem, CSV)
         │
         ▼
  [ Amazon S3 ] ──(Trigger Event)──► [ AWS Lambda ]
                                            │
               ┌────────────────────────────┼────────────────────────────┐
               ▼                            ▼                            ▼
      (PDFs e Imagens)                   (CSV/CRM)               (Textos Processados)
   [ Amazon Textract ]              [ AWS Lambda / Glue ]               │
 (OCR e Leitura Manuscrita)        (Formatação de Tabelas)               │
               │                            │                            │
               └────────────────────────────┴────────────────────────────┘
                                            │
                                            ▼
                                  [ Amazon S3 Processed ]
                                            │
                                            ▼
                             [ Amazon Bedrock Embeddings ]
                                            │
                                            ▼
                         [ Amazon Bedrock Knowledge Bases ]
                             (OpenSearch Serverless)
                                            │
                                            ▼
                             [ Consulta em Linguagem Natural ]
