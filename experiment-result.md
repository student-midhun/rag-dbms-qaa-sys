RAG-Based DBMS Question Answering System
Experiment Results & Analysis
Dataset Description
The dataset consists of DBMS academic material extracted from PDF documents. The content includes theoretical explanations, definitions, mappings, normalization concepts, transaction properties, and SQL command classifications.

Domain: Database Management Systems (DBMS)
Format: PDF documents
Preprocessing: Text cleaning using regex-based normalization
Embedding-based retrieval using FAISS
Evaluated using 10 conceptual DBMS questions
The dataset primarily contains definition-based and comparison-based academic content.

Experiment 1: Chunking Strategies
Methodology
We evaluated two chunking approaches:

Fixed-size chunking

Character length: 500
Overlap: 50
Sentence-based chunking

Split using sentence boundaries
Preserved semantic integrity
Evaluation Criteria:

Retrieval relevance (Low / Partial / High)
Answer quality (Low / Medium / High)
Structural coherence
Context preservation
Tested using the same 10 DBMS questions.

Results
Strategy	Avg Retrieval	Avg Answer Quality	Pros	Cons
Fixed-size	Medium	Medium	Simple, fast	Breaks sentences, context loss
Sentence-based	High	High	Preserves meaning, better alignment	Slightly larger chunks
Key Observations
Fixed-size chunking sometimes split definitions mid-sentence.
Sentence-based chunking preserved conceptual boundaries.
Retrieval precision improved significantly with sentence-based chunks.
Answer completeness improved due to better contextual alignment.
Conclusion – Chunking
Sentence-based chunking performed better for the DBMS dataset.

Reason:

DBMS content is definition-heavy and structured.
Breaking sentences reduces conceptual clarity.
Sentence-based chunks preserved academic flow and improved answer grounding.
Experiment 2: Prompting Techniques
Prompts Compared
1. Basic Prompt
The model was instructed to answer only using the given context without any structural guidance.

2. Structured Prompt
The model was instructed to:

Provide clear definitions when required
Use bullet points for comparisons
Use numbered steps for processes
Respond with "Not found in context" if unavailable
Results
Question Type	Basic Quality	Structured Quality	Improvement
Definitions	Medium	High	Clearer and complete explanations
Comparisons	Medium	High	Better formatting and clarity
Concept Explanations	Medium	High	Structured presentation
Key Observations
Retrieval remained the same in both approaches.
Structured prompting improved answer readability and completeness.
Academic clarity significantly improved.
Comparison-based questions benefited the most from structured formatting.
Conclusion – Prompting
Structured prompting performed better than basic prompting.

Reason:

DBMS is a theoretical subject requiring clear definitions.
Structured outputs align with exam-style expectations.
The model responded more consistently when given formatting instructions.
Real-World Challenges
Challenge 1: Inconsistent PDF Formatting
Problem
Extracted text had:

Broken sentences
Missing spaces
Irregular numbering
Merged headings
This reduced chunk quality and retrieval precision.

Solution
Applied regex-based text cleaning before chunking:

Normalized whitespace
Fixed numbering formats
Restored sentence boundaries
Limitations
Regex-based cleaning cannot fully reconstruct tables.
Complex layouts may still produce noise.
Challenge 2: Domain-Specific Terminology
Problem
Technical DBMS terms sometimes resulted in:

Incomplete explanations
Over-generalized responses
Solution
Implemented structured prompting to enforce:

Clear definitions
Step-wise explanations
Proper comparison formatting
Limitations
If context was missing, structured prompting could not recover information.
Retrieval quality remains critical.
Final System Decision
Final configuration selected:

Chunking: Sentence-based
Retriever top-k: 3
Prompt Type: Structured prompting
Text Cleaning: Regex normalization
LLM: Gemini-based model using generate_content()
Reason for selection:

Best balance of relevance and clarity
Improved academic structure
Reduced context fragmentation
Better alignment with DBMS conceptual questions
Cost Analysis
Assumptions:

100 users
10 questions per day
1000 queries/day
Approx 1300 tokens per query
Estimated total tokens per day: ~1.3 million tokens

If using an average cost of $0.01 per 1000 tokens:

Estimated daily cost ≈ $13
Estimated monthly cost ≈ $390

Cost optimization strategies:

Reduce context size
Cache repeated queries
Use smaller LLM for simple definitions
Optimize chunk size
Critical Reflection
What worked well?
Sentence-based chunking improved retrieval consistency.
Structured prompting improved clarity significantly.
RAG architecture worked well for theoretical DBMS questions.
What didn’t work?
Questions not present in dataset completely failed.
PDF text extraction quality affects overall system performance.
Tables and diagrams remain difficult to process.
If more time?
Implement semantic chunking.
Use layout-aware PDF parsing.
Add hybrid retrieval (keyword + embedding).
Production Considerations
Additional Testing:

Edge-case questions
Ambiguous queries
Long-form reasoning queries
Monitoring:

Log retrieval failures
Track hallucinated responses
Monitor token usage
Metrics to Track:

Retrieval relevance score
Answer accuracy
Response latency
Cost per query
Failure Modes:

Missing context
Hallucinated definitions
Partial retrieval
Token truncation
Theory vs Practice
Retrieval quality impacts performance more than model size.
Real-world PDFs are messy compared to tutorial datasets.
Prompt sensitivity significantly affects answer presentation.
RAG requires more system-level design than typical academic ML projects.
Final Remarks
This project demonstrated that effective chunking and structured prompting significantly improve RAG performance for academic domains like DBMS. While retrieval remains the backbone of the system, prompt design plays a crucial role in answer quality and clarity.

The final system achieves strong performance for definition-based and comparison-based DBMS questions, with clear opportunities for further improvement in handling complex document structures.
