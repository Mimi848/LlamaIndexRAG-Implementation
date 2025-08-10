# LlamaIndex RAG Implementation

A local Retrieval-Augmented Generation (RAG) system built with LlamaIndex, using Ollama for local LLM inference and Hugging Face embeddings.

## 🚀 Features

- **Local LLM Integration**: Uses Ollama to run language models locally
- **Vector Search**: Implements semantic search using Hugging Face embeddings
- **Document Processing**: Automatically chunks and indexes documents
- **TypeScript Support**: Full TypeScript implementation with type safety
- **Privacy-First**: All processing happens locally - no data sent to external APIs

## 📋 Prerequisites

- **Node.js** (v16 or higher)
- **Yarn** package manager
- **Ollama** installed and running locally

## 🛠️ Installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/Mimi848/LlamaIndexRAG-Implementation.git
   cd LlamaIndexRAG-Implementation
   ```

2. **Install dependencies:**

   ```bash
   yarn install
   ```

3. **Install and setup Ollama:**

   ```bash
   # Install Ollama (macOS)
   brew install ollama

   # Or download from https://ollama.com

   # Pull the required model
   ollama pull mistral
   ```

## 🚀 Quick Start

1. **Start Ollama service:**

   ```bash
   ollama serve
   ```

2. **Run the RAG system:**
   ```bash
   yarn start
   # or
   npx tsx vectorIndexLocal.ts
   ```

The script will:

- Load the example document (`abramov.txt`)
- Create embeddings and build a vector index
- Query the document with: "What did the author do in college?"
- Return an AI-generated response based on the document content

## 📁 Project Structure

```
├── vectorIndexLocal.ts    # Main RAG implementation
├── package.json          # Dependencies and scripts
├── yarn.lock            # Dependency lock file
├── .gitignore           # Git ignore rules
└── README.md            # This file
```

## ⚙️ Configuration

### LLM Model

The system uses Mistral by default. To change the model:

```typescript
Settings.llm = new Ollama({
  model: "mistral", // Change to your preferred model
});
```

Available models (pull with `ollama pull <model>`):

- `mistral` (default)
- `llama2`
- `codellama`
- `mixtral:8x7b`

### Embedding Model

Uses Hugging Face's `BAAI/bge-small-en-v1.5` for embeddings:

```typescript
Settings.embedModel = new HuggingFaceEmbedding({
  modelType: "BAAI/bge-small-en-v1.5",
});
```

## 📖 Usage Examples

### Basic Document Query

```typescript
const queryEngine = index.asQueryEngine();
const response = await queryEngine.query({
  query: "What is the main topic of the document?",
});
console.log(response.toString());
```

### Custom Document Processing

```typescript
// Load your own document
const essay = await fs.readFile("path/to/your/document.txt", "utf-8");
const document = new Document({ text: essay, id_: "custom-doc" });

// Create index
const index = await VectorStoreIndex.fromDocuments([document]);
```

## 🔧 Troubleshooting

### Common Issues

1. **Ollama Connection Error:**

   - Ensure Ollama service is running: `ollama serve`
   - Check if the model is available: `ollama list`

2. **Missing Model Error:**

   - Pull the required model: `ollama pull mistral`

3. **Memory Issues:**
   - Use smaller models like `mistral` instead of `mixtral:8x7b`
   - Reduce document size for processing

### Warning Messages

You may see deprecation warnings about `@llamaindex/cloud` - these are harmless and don't affect functionality for local usage.

## 📚 Dependencies

- **llamaindex**: Core LlamaIndex library
- **@llamaindex/ollama**: Ollama integration
- **@llamaindex/huggingface**: Hugging Face embeddings
- **typescript**: TypeScript support
- **tsx**: TypeScript execution runtime

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes
4. Run tests: `yarn test` (if available)
5. Commit changes: `git commit -m 'Add feature'`
6. Push to branch: `git push origin feature-name`
7. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🔗 Links

- [LlamaIndex Documentation](https://docs.llamaindex.ai/)
- [Ollama Models](https://ollama.com/library)
- [Hugging Face Models](https://huggingface.co/models)

## 📞 Support

If you encounter any issues or have questions:

1. Check the [troubleshooting section](#-troubleshooting)
2. Review [LlamaIndex documentation](https://docs.llamaindex.ai/)
3. Open an issue in this repository
