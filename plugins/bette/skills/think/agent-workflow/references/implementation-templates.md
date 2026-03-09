# Agent Implementation Templates

## System Prompt Templates

### Template 1: Research Agent

```
You are a research specialist agent focused on [DOMAIN].

ROLE: Gather comprehensive information from multiple sources to answer specific research questions.

TOOLS AVAILABLE:
- web_search: Search the web for information
- fetch_url: Retrieve full content from URLs
- database_query: Search internal knowledge base
- extract_data: Parse structured data from documents

RESEARCH PROCESS:
1. Understand the research question thoroughly
2. Identify 3-5 relevant sources to check
3. Gather information from each source
4. Cross-reference facts for accuracy
5. Synthesize findings into coherent summary
6. Cite all sources used

OUTPUT FORMAT:
{
  "summary": "2-3 sentence overview of findings",
  "key_findings": [
    {
      "finding": "Specific fact or insight",
      "source": "URL or citation",
      "confidence": "high | medium | low"
    }
  ],
  "gaps": ["Information not found"],
  "sources_checked": ["list of URLs/databases"]
}

QUALITY STANDARDS:
- Always verify facts from 2+ sources when possible
- Flag contradictory information
- Indicate confidence levels
- Never fabricate information
- If information not found, explicitly state it

EXAMPLE:
Question: "What are the benefits of meditation?"
Research: Web search → Medical journals → Health sites
Output: Summary with 5-7 benefits, each cited, confidence levels noted
```

### Template 2: Decision Agent

```
You are a decision-making agent for [USE CASE].

ROLE: Analyze situations and make decisions based on predefined rules and context.

DECISION FRAMEWORK:
1. Gather all relevant context
2. Identify the decision to be made
3. Apply decision rules in priority order
4. Consider edge cases and exceptions
5. Calculate confidence in recommendation
6. Provide clear reasoning

DECISION RULES (Priority Order):
[Rule 1]: IF [condition] THEN [action]
[Rule 2]: IF [condition] THEN [action]
[Rule 3]: IF [condition] THEN [action]

When rules conflict: [Tie-breaking logic]

OUTPUT FORMAT:
{
  "decision": "approve | deny | escalate",
  "confidence": 0-100,
  "reasoning": "Explain which rules applied and why",
  "factors_considered": ["list"],
  "alternatives": [
    {
      "option": "Alternative decision",
      "rationale": "Why it was not chosen"
    }
  ],
  "escalation_reason": "Only if decision=escalate"
}

ESCALATION TRIGGERS:
- Confidence < 70%
- [Specific condition that requires human review]
- [High-stakes scenario threshold]

EXAMPLE:
Context: Refund request for $150 order, purchased 45 days ago
Decision: Deny (outside 30-day policy)
Confidence: 90%
Reasoning: Violates time-based rule, no exceptions apply
Alternative: Offer store credit (customer retention consideration)
```

### Template 3: Content Generation Agent

```
You are a content creation agent specializing in [CONTENT TYPE].

ROLE: Generate high-quality [content type] that matches brand voice and meets quality standards.

BRAND VOICE:
- Tone: [Professional/Casual/Conversational/etc.]
- Perspective: [First/Second/Third person]
- Style: [Data-driven/Storytelling/Educational/etc.]
- Vocabulary level: [Grade level or audience description]
- Avoid: [Specific words/phrases/patterns to avoid]

CONTENT STRUCTURE:
1. [Opening section]: [Purpose and requirements]
2. [Body section 1]: [Purpose and requirements]
3. [Body section 2]: [Purpose and requirements]
4. [Closing section]: [Purpose and requirements]

QUALITY CHECKLIST:
- [ ] Matches brand voice and tone
- [ ] Appropriate length ([X] words)
- [ ] Includes [required elements]
- [ ] Clear structure with subheadings
- [ ] Actionable and specific
- [ ] No grammatical errors
- [ ] Engaging and readable

OUTPUT FORMAT:
{
  "content": "Full content text",
  "metadata": {
    "word_count": number,
    "reading_time": "X minutes",
    "quality_score": 0-100,
    "checklist_passed": boolean
  },
  "suggestions": ["Optional improvements"]
}

EXAMPLE INPUT: "Write a product announcement email"
EXAMPLE OUTPUT: 
- Subject line: Compelling hook
- Opening: Problem statement
- Body: Solution benefits (3-4 bullets)
- CTA: Clear next step
- Length: 150-200 words
- Tone: Excited but professional
```

### Template 4: Quality Assurance Agent

```
You are a quality assurance agent reviewing [OUTPUT TYPE].

ROLE: Review outputs from other agents or processes and verify they meet quality standards.

REVIEW DIMENSIONS:
1. Accuracy: Facts correct, logic sound, no hallucinations
2. Completeness: All required elements present
3. Format: Follows specified structure
4. Style: Matches guidelines and brand voice
5. Technical: No errors, proper syntax
6. Context: Appropriate for audience and purpose

REVIEW PROCESS:
1. Load quality criteria for this output type
2. Review output against each criterion
3. Assign scores (0-100) for each dimension
4. Calculate overall quality score
5. Identify specific issues with severity levels
6. Provide actionable improvement suggestions
7. Make pass/fail recommendation

OUTPUT FORMAT:
{
  "overall_score": 0-100,
  "dimension_scores": {
    "accuracy": 0-100,
    "completeness": 0-100,
    "format": 0-100,
    "style": 0-100,
    "technical": 0-100,
    "context": 0-100
  },
  "issues": [
    {
      "severity": "critical | high | medium | low",
      "dimension": "which dimension",
      "description": "What's wrong",
      "location": "Where in the output",
      "suggestion": "How to fix"
    }
  ],
  "recommendation": "approve | request_revision | reject",
  "revision_notes": "Guidance for revision if needed"
}

SEVERITY DEFINITIONS:
- Critical: Factual errors, security issues, broken functionality
- High: Significant quality problems, missing key elements
- Medium: Minor issues that reduce quality
- Low: Nitpicks, style preferences

EXAMPLE:
Reviewing blog post:
- Accuracy: 95 (one unsupported claim)
- Completeness: 100 (all sections present)
- Format: 90 (one heading formatting issue)
- Style: 85 (some sentences too complex)
Overall: 92 (pass with minor revisions)
```

---

## Multi-Agent Orchestration Patterns

### Pattern 1: Sequential Pipeline

**Use When:** Each step depends on previous step's output

```python
# Orchestrator logic

def sequential_pipeline(input_data):
    """
    Step 1 → Step 2 → Step 3 → Output
    Each step must complete before next begins
    """
    
    # Step 1: Research
    research_output = research_agent.run(input_data)
    
    # Step 2: Analysis (uses research output)
    analysis_output = analysis_agent.run(research_output)
    
    # Step 3: Writing (uses both)
    final_output = writing_agent.run({
        "research": research_output,
        "analysis": analysis_output
    })
    
    return final_output

# Error handling
def sequential_pipeline_with_retry(input_data, max_retries=3):
    for step in [research_agent, analysis_agent, writing_agent]:
        retries = 0
        while retries < max_retries:
            try:
                output = step.run(current_data)
                current_data = output
                break
            except Exception as e:
                retries += 1
                if retries >= max_retries:
                    return escalate_to_human(step, e)
                log_error(step, e, retries)
    
    return current_data
```

### Pattern 2: Parallel Processing

**Use When:** Sub-tasks are independent and can run simultaneously

```python
# Orchestrator logic

def parallel_processing(input_data):
    """
    Input → [Agent A, Agent B, Agent C] → Synthesis → Output
    All agents run concurrently, results combined
    """
    
    # Start all agents simultaneously
    import asyncio
    
    async def run_all():
        research_task = research_agent.run_async(input_data)
        competitor_task = competitor_agent.run_async(input_data)
        market_task = market_agent.run_async(input_data)
        
        # Wait for all to complete
        results = await asyncio.gather(
            research_task,
            competitor_task,
            market_task
        )
        
        return results
    
    # Get all results
    research, competitors, market = asyncio.run(run_all())
    
    # Synthesis agent combines results
    final_output = synthesis_agent.run({
        "research": research,
        "competitors": competitors,
        "market": market
    })
    
    return final_output

# Partial failure handling
async def parallel_with_fallback(input_data):
    tasks = {
        "research": research_agent.run_async(input_data),
        "competitors": competitor_agent.run_async(input_data),
        "market": market_agent.run_async(input_data)
    }
    
    results = {}
    for name, task in tasks.items():
        try:
            results[name] = await task
        except Exception as e:
            log_error(name, e)
            results[name] = None  # Partial failure OK
    
    # Synthesis works with available data
    return synthesis_agent.run(results)
```

### Pattern 3: Iterative Refinement

**Use When:** Output quality improves with multiple passes

```python
# Orchestrator logic

def iterative_refinement(input_data, max_iterations=3):
    """
    Draft → Review → Revise → Review → Revise → Final
    Continue until quality threshold met or max iterations reached
    """
    
    # Initial draft
    current_draft = writing_agent.run(input_data)
    
    for iteration in range(max_iterations):
        # Review current draft
        review = qa_agent.run(current_draft)
        
        # Check if quality threshold met
        if review["overall_score"] >= 90:
            return {
                "final_output": current_draft,
                "iterations": iteration + 1,
                "final_score": review["overall_score"]
            }
        
        # Revise based on feedback
        current_draft = writing_agent.run({
            "original_input": input_data,
            "previous_draft": current_draft,
            "feedback": review["issues"],
            "revision_notes": review["revision_notes"]
        })
    
    # Max iterations reached, return best attempt
    return {
        "final_output": current_draft,
        "iterations": max_iterations,
        "warning": "Max iterations reached",
        "final_score": review["overall_score"]
    }
```

### Pattern 4: Conditional Routing

**Use When:** Different inputs need different processing paths

```python
# Orchestrator logic

def conditional_routing(input_data):
    """
    Input → Classifier → Route to appropriate agent(s) → Output
    Classification determines which workflow to follow
    """
    
    # Classify input
    classification = classifier_agent.run(input_data)
    
    # Route based on classification
    if classification["type"] == "simple_inquiry":
        # Simple path: Direct answer
        return simple_response_agent.run(input_data)
    
    elif classification["type"] == "research_required":
        # Research path: Multi-step investigation
        research = research_agent.run(input_data)
        analysis = analysis_agent.run(research)
        return response_agent.run({
            "query": input_data,
            "research": research,
            "analysis": analysis
        })
    
    elif classification["type"] == "complex_decision":
        # Decision path: Multiple experts + consensus
        expert_opinions = []
        for expert in [expert_a, expert_b, expert_c]:
            opinion = expert.run(input_data)
            expert_opinions.append(opinion)
        
        consensus = consensus_agent.run(expert_opinions)
        return consensus
    
    else:
        # Unknown type: Escalate to human
        return escalate_to_human(input_data, classification)

# With confidence-based routing
def confidence_routing(input_data):
    # Try simple agent first
    result = simple_agent.run(input_data)
    
    # If confidence low, escalate to advanced agent
    if result["confidence"] < 0.7:
        result = advanced_agent.run({
            "input": input_data,
            "simple_attempt": result
        })
    
    # If still low confidence, human review
    if result["confidence"] < 0.85:
        result["human_review_required"] = True
    
    return result
```

---

## Tool Integration Implementation Patterns

### Pattern 1: REST API Integration

```python
# Tool definition for API integration

class CRMTool:
    """
    Tool for interacting with CRM (Salesforce, HubSpot, etc.)
    """
    
    def __init__(self, api_key, base_url):
        self.api_key = api_key
        self.base_url = base_url
        self.session = requests.Session()
        self.session.headers.update({
            "Authorization": f"Bearer {api_key}",
            "Content-Type": "application/json"
        })
    
    def get_customer(self, email):
        """
        Retrieve customer data by email
        
        Returns:
        {
            "customer_id": "string",
            "name": "string",
            "company": "string",
            "lifetime_value": number,
            "status": "active | inactive",
            "interactions": [...]
        }
        """
        try:
            response = self.session.get(
                f"{self.base_url}/customers",
                params={"email": email},
                timeout=10
            )
            response.raise_for_status()
            return response.json()
        
        except requests.exceptions.Timeout:
            return {"error": "API timeout", "use_cached": True}
        
        except requests.exceptions.HTTPError as e:
            if e.response.status_code == 404:
                return {"error": "Customer not found"}
            elif e.response.status_code == 429:
                # Rate limit: wait and retry
                time.sleep(2)
                return self.get_customer(email)
            else:
                return {"error": f"API error: {e}"}
    
    def create_opportunity(self, customer_id, details):
        """
        Create new sales opportunity
        """
        try:
            response = self.session.post(
                f"{self.base_url}/opportunities",
                json={
                    "customer_id": customer_id,
                    "name": details["name"],
                    "amount": details["amount"],
                    "stage": "discovery"
                },
                timeout=10
            )
            response.raise_for_status()
            return response.json()
        
        except Exception as e:
            return {"error": f"Failed to create opportunity: {e}"}

# Agent system prompt referencing this tool
"""
You have access to CRM data via the get_customer and create_opportunity tools.

USING get_customer:
- Input: customer email address
- Output: Customer profile with history
- Handle errors: If customer not found, proceed with limited info

USING create_opportunity:
- Input: customer_id and opportunity details
- Only call after qualifying the lead
- Verify customer_id exists before calling
"""
```

### Pattern 2: Database Query Tool

```python
# Tool for database access

class DatabaseTool:
    """
    Safe database query tool with query validation
    """
    
    def __init__(self, connection_string):
        self.engine = create_engine(connection_string)
    
    def execute_query(self, query, params=None):
        """
        Execute read-only query safely
        
        Security:
        - Only SELECT statements allowed
        - Parameterized queries prevent SQL injection
        - Query timeout prevents long-running queries
        - Row limit prevents excessive data retrieval
        """
        
        # Validate query is read-only
        query_upper = query.upper().strip()
        if not query_upper.startswith("SELECT"):
            return {"error": "Only SELECT queries allowed"}
        
        if any(keyword in query_upper for keyword in ["DROP", "DELETE", "UPDATE", "INSERT"]):
            return {"error": "Modifying queries not allowed"}
        
        try:
            with self.engine.connect() as conn:
                # Set timeout
                conn = conn.execution_options(timeout=30)
                
                # Execute with parameters
                result = conn.execute(text(query), params or {})
                
                # Fetch with row limit
                rows = result.fetchmany(1000)
                
                return {
                    "columns": list(result.keys()),
                    "rows": [dict(row) for row in rows],
                    "row_count": len(rows),
                    "truncated": len(rows) == 1000
                }
        
        except Exception as e:
            return {"error": f"Query failed: {e}"}
    
    def get_schema(self, table_name=None):
        """
        Retrieve table schema information
        """
        if table_name:
            query = """
                SELECT column_name, data_type, is_nullable
                FROM information_schema.columns
                WHERE table_name = :table_name
                ORDER BY ordinal_position
            """
            return self.execute_query(query, {"table_name": table_name})
        else:
            query = """
                SELECT table_name
                FROM information_schema.tables
                WHERE table_schema = 'public'
                ORDER BY table_name
            """
            return self.execute_query(query)

# Agent system prompt
"""
You have access to the company database via execute_query.

AVAILABLE TABLES:
- customers: customer_id, name, email, created_at, status
- orders: order_id, customer_id, amount, order_date, status
- products: product_id, name, category, price

QUERY GUIDELINES:
1. Always use parameterized queries
2. Limit results to necessary rows
3. Join tables efficiently
4. Handle NULL values appropriately

EXAMPLE:
To find high-value customers:
SELECT customer_id, name, SUM(amount) as total
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY customer_id, name
HAVING SUM(amount) > 10000
ORDER BY total DESC
LIMIT 10
"""
```

### Pattern 3: Document Processing Tool

```python
# Tool for document analysis

class DocumentTool:
    """
    Extract and analyze content from documents
    """
    
    def extract_text(self, file_path):
        """
        Extract text from various document formats
        """
        file_extension = file_path.split('.')[-1].lower()
        
        try:
            if file_extension == 'pdf':
                return self._extract_pdf(file_path)
            elif file_extension in ['docx', 'doc']:
                return self._extract_docx(file_path)
            elif file_extension == 'txt':
                with open(file_path, 'r', encoding='utf-8') as f:
                    return {"text": f.read(), "pages": 1}
            else:
                return {"error": f"Unsupported file type: {file_extension}"}
        
        except Exception as e:
            return {"error": f"Extraction failed: {e}"}
    
    def _extract_pdf(self, file_path):
        """Extract text from PDF"""
        import pdfplumber
        
        text_by_page = []
        with pdfplumber.open(file_path) as pdf:
            for page in pdf.pages:
                text_by_page.append(page.extract_text())
        
        return {
            "text": "\n\n".join(text_by_page),
            "pages": len(text_by_page),
            "text_by_page": text_by_page
        }
    
    def _extract_docx(self, file_path):
        """Extract text from DOCX"""
        from docx import Document
        
        doc = Document(file_path)
        paragraphs = [p.text for p in doc.paragraphs if p.text.strip()]
        
        return {
            "text": "\n\n".join(paragraphs),
            "pages": len(doc.sections),
            "paragraphs": paragraphs
        }
    
    def analyze_document(self, text):
        """
        Analyze document structure and extract key information
        """
        return {
            "word_count": len(text.split()),
            "character_count": len(text),
            "estimated_reading_time": len(text.split()) / 200,  # 200 wpm average
            "sections": self._identify_sections(text),
            "key_terms": self._extract_key_terms(text)
        }
    
    def _identify_sections(self, text):
        """Identify document sections based on headings"""
        # Simplified: Look for lines that could be headings
        lines = text.split('\n')
        sections = []
        
        for i, line in enumerate(lines):
            # Heuristic: Short lines in all caps or title case might be headings
            if len(line.split()) <= 10 and (line.isupper() or line.istitle()):
                sections.append({
                    "heading": line,
                    "line_number": i
                })
        
        return sections
    
    def _extract_key_terms(self, text):
        """Extract potentially important terms"""
        # Simplified: Find capitalized multi-word phrases
        import re
        
        # Pattern: Consecutive capitalized words
        pattern = r'\b[A-Z][a-z]+(?:\s+[A-Z][a-z]+)+\b'
        key_terms = re.findall(pattern, text)
        
        # Count frequency
        from collections import Counter
        term_freq = Counter(key_terms)
        
        # Return top 10
        return [
            {"term": term, "count": count}
            for term, count in term_freq.most_common(10)
        ]

# Agent system prompt
"""
You have access to document processing via extract_text and analyze_document tools.

WORKFLOW FOR DOCUMENT ANALYSIS:
1. Call extract_text with file path
2. Review extracted text
3. Call analyze_document for structure analysis
4. Answer user's question about the document

HANDLING ERRORS:
- If extraction fails, inform user and request different format
- If document is too long, analyze in sections
- Always cite page numbers when referencing specific content
"""
```

---

## Memory Implementation Patterns

### Pattern 1: Conversation Memory

```python
# Simple conversation history management

class ConversationMemory:
    """
    Maintains conversation history for context
    """
    
    def __init__(self, max_messages=20):
        self.messages = []
        self.max_messages = max_messages
    
    def add_message(self, role, content):
        """
        Add message to history
        
        Args:
            role: 'user' or 'assistant'
            content: message content
        """
        self.messages.append({
            "role": role,
            "content": content,
            "timestamp": datetime.now()
        })
        
        # Keep only recent messages to manage context length
        if len(self.messages) > self.max_messages:
            self.messages = self.messages[-self.max_messages:]
    
    def get_context(self):
        """
        Return formatted conversation history
        """
        return [
            {"role": msg["role"], "content": msg["content"]}
            for msg in self.messages
        ]
    
    def get_recent_messages(self, n=5):
        """Get last n messages"""
        return self.messages[-n:]
    
    def clear(self):
        """Clear conversation history"""
        self.messages = []
```

### Pattern 2: User Preference Memory

```python
# Persistent user preferences and context

class UserMemory:
    """
    Store and retrieve user preferences and historical context
    """
    
    def __init__(self, user_id, storage_backend):
        self.user_id = user_id
        self.storage = storage_backend
        self.cache = self._load_user_data()
    
    def _load_user_data(self):
        """Load user data from storage"""
        data = self.storage.get(f"user:{self.user_id}")
        return data or {
            "preferences": {},
            "interaction_history": [],
            "learned_context": {}
        }
    
    def save(self):
        """Persist changes to storage"""
        self.storage.set(f"user:{self.user_id}", self.cache)
    
    def set_preference(self, key, value):
        """Store user preference"""
        self.cache["preferences"][key] = value
        self.save()
    
    def get_preference(self, key, default=None):
        """Retrieve user preference"""
        return self.cache["preferences"].get(key, default)
    
    def record_interaction(self, interaction_type, details):
        """Record user interaction for learning"""
        self.cache["interaction_history"].append({
            "type": interaction_type,
            "details": details,
            "timestamp": datetime.now().isoformat()
        })
        
        # Keep last 100 interactions
        self.cache["interaction_history"] = \
            self.cache["interaction_history"][-100:]
        
        self.save()
    
    def update_learned_context(self, key, value):
        """Update learned information about user"""
        self.cache["learned_context"][key] = value
        self.save()
    
    def get_full_context(self):
        """Return all user context for agent"""
        return {
            "user_id": self.user_id,
            "preferences": self.cache["preferences"],
            "recent_interactions": self.cache["interaction_history"][-10:],
            "learned_context": self.cache["learned_context"]
        }

# System prompt integration
"""
You have access to user context:
{user_memory.get_full_context()}

Use this information to personalize your responses:
- Respect user preferences
- Reference past interactions when relevant
- Build on learned context
- Ask for preferences if not set
"""
```

### Pattern 3: Knowledge Retrieval Memory

```python
# Vector database for semantic search

class KnowledgeMemory:
    """
    Semantic search over knowledge base
    """
    
    def __init__(self, vector_db):
        self.db = vector_db
    
    def add_document(self, text, metadata=None):
        """
        Add document to knowledge base
        
        Args:
            text: document content
            metadata: optional metadata (title, source, date, etc.)
        """
        # Chunk document into smaller pieces
        chunks = self._chunk_text(text, chunk_size=500, overlap=50)
        
        # Store each chunk with metadata
        for i, chunk in enumerate(chunks):
            chunk_metadata = metadata.copy() if metadata else {}
            chunk_metadata["chunk_index"] = i
            chunk_metadata["total_chunks"] = len(chunks)
            
            self.db.add(
                text=chunk,
                metadata=chunk_metadata
            )
    
    def search(self, query, top_k=5):
        """
        Search for relevant documents
        
        Returns:
            List of relevant text chunks with metadata
        """
        results = self.db.search(query, limit=top_k)
        
        return [
            {
                "text": result.text,
                "metadata": result.metadata,
                "relevance_score": result.score
            }
            for result in results
        ]
    
    def _chunk_text(self, text, chunk_size=500, overlap=50):
        """Split text into overlapping chunks"""
        words = text.split()
        chunks = []
        
        for i in range(0, len(words), chunk_size - overlap):
            chunk = ' '.join(words[i:i + chunk_size])
            chunks.append(chunk)
        
        return chunks

# Agent integration
def agent_with_knowledge_retrieval(query, knowledge_memory):
    """
    Agent that retrieves relevant knowledge before responding
    """
    
    # Retrieve relevant context
    relevant_docs = knowledge_memory.search(query, top_k=3)
    
    # Build context for agent
    context = "\n\n".join([
        f"[Source: {doc['metadata'].get('title', 'Unknown')}]\n{doc['text']}"
        for doc in relevant_docs
    ])
    
    # Agent prompt with retrieved context
    prompt = f"""
    Answer the question using the provided context.
    
    Context:
    {context}
    
    Question: {query}
    
    Instructions:
    - Base your answer on the provided context
    - Cite sources when making claims
    - If context doesn't contain the answer, say so
    """
    
    return agent.run(prompt)
```

---

## Testing and Validation Patterns

### Pattern 1: Unit Testing Individual Agents

```python
# Test framework for agent behavior

import pytest

class TestResearchAgent:
    """
    Test suite for research agent
    """
    
    def test_basic_query(self):
        """Test agent handles basic research query"""
        agent = ResearchAgent()
        query = "What is machine learning?"
        
        result = agent.run(query)
        
        assert result["summary"] is not None
        assert len(result["key_findings"]) > 0
        assert all(f["confidence"] in ["high", "medium", "low"] 
                   for f in result["key_findings"])
    
    def test_handles_no_results(self):
        """Test agent handles queries with no results"""
        agent = ResearchAgent()
        query = "sdfjksldjfklsdjfklsjdfkl"  # Gibberish
        
        result = agent.run(query)
        
        assert "no information found" in result["summary"].lower()
        assert len(result["gaps"]) > 0
    
    def test_citation_quality(self):
        """Test agent properly cites sources"""
        agent = ResearchAgent()
        query = "Benefits of exercise"
        
        result = agent.run(query)
        
        for finding in result["key_findings"]:
            assert finding["source"] is not None
            assert finding["source"].startswith("http") or "database" in finding["source"]
    
    def test_error_handling(self):
        """Test agent handles API errors gracefully"""
        agent = ResearchAgent()
        agent.web_search_tool = MockToolWithError()  # Mock failing tool
        
        result = agent.run("test query")
        
        assert result["error"] is not None
        assert "fallback" in result or "retry" in result

# Performance testing
def test_agent_response_time():
    """Ensure agent responds within acceptable time"""
    agent = ResearchAgent()
    
    start = time.time()
    result = agent.run("Quick fact query")
    end = time.time()
    
    response_time = end - start
    assert response_time < 10  # Should respond within 10 seconds
```

### Pattern 2: Integration Testing Multi-Agent Systems

```python
# Test multi-agent orchestration

class TestMultiAgentPipeline:
    """
    Test complete multi-agent workflow
    """
    
    def test_complete_pipeline(self):
        """Test full pipeline from input to output"""
        orchestrator = MultiAgentOrchestrator()
        
        input_data = {
            "task": "Research and write report",
            "topic": "AI trends 2024"
        }
        
        result = orchestrator.run(input_data)
        
        # Verify each agent contributed
        assert result["research_completed"] == True
        assert result["analysis_completed"] == True
        assert result["writing_completed"] == True
        assert result["qa_passed"] == True
        
        # Verify final output quality
        assert len(result["final_output"]) > 1000  # Substantial content
        assert result["quality_score"] >= 80
    
    def test_agent_handoff(self):
        """Test data flows correctly between agents"""
        orchestrator = MultiAgentOrchestrator()
        
        # Track data flow
        orchestrator.enable_logging()
        
        result = orchestrator.run({"task": "test"})
        
        logs = orchestrator.get_logs()
        
        # Verify each agent received correct input
        assert logs["research_agent_input"] is not None
        assert logs["analysis_agent_input"]["research_data"] is not None
        assert logs["writing_agent_input"]["analysis_data"] is not None
    
    def test_partial_failure_recovery(self):
        """Test system handles agent failures"""
        orchestrator = MultiAgentOrchestrator()
        
        # Make analysis agent fail
        orchestrator.analysis_agent = MockFailingAgent()
        
        result = orchestrator.run({"task": "test"})
        
        # Should complete with degraded functionality
        assert result["status"] == "partial_success"
        assert result["failed_agents"] == ["analysis_agent"]
        assert result["final_output"] is not None  # Still produces output
```

### Pattern 3: Quality Validation

```python
# Validate agent output quality

class QualityValidator:
    """
    Automated quality checks for agent outputs
    """
    
    def validate_research_output(self, output):
        """
        Validate research agent output meets standards
        """
        issues = []
        
        # Check required fields
        required_fields = ["summary", "key_findings", "sources_checked"]
        for field in required_fields:
            if field not in output:
                issues.append(f"Missing required field: {field}")
        
        # Check quality standards
        if len(output.get("key_findings", [])) < 3:
            issues.append("Insufficient findings (need at least 3)")
        
        for finding in output.get("key_findings", []):
            if not finding.get("source"):
                issues.append(f"Finding lacks source: {finding.get('finding')}")
            
            if finding.get("confidence") not in ["high", "medium", "low"]:
                issues.append(f"Invalid confidence level: {finding.get('confidence')}")
        
        # Check citation quality
        sources = output.get("sources_checked", [])
        if len(sources) < 2:
            issues.append("Too few sources checked (need at least 2)")
        
        return {
            "valid": len(issues) == 0,
            "issues": issues,
            "quality_score": max(0, 100 - len(issues) * 10)
        }
    
    def validate_content_output(self, output, requirements):
        """
        Validate content meets specified requirements
        """
        issues = []
        
        # Word count
        word_count = len(output["content"].split())
        min_words = requirements.get("min_words", 500)
        max_words = requirements.get("max_words", 3000)
        
        if word_count < min_words:
            issues.append(f"Too short: {word_count} words (need {min_words}+)")
        elif word_count > max_words:
            issues.append(f"Too long: {word_count} words (max {max_words})")
        
        # Required sections
        required_sections = requirements.get("required_sections", [])
        for section in required_sections:
            if section.lower() not in output["content"].lower():
                issues.append(f"Missing required section: {section}")
        
        # Readability
        if requirements.get("readability_check"):
            # Simplified readability check
            avg_sentence_length = word_count / output["content"].count('.')
            if avg_sentence_length > 25:
                issues.append("Sentences too long (avg > 25 words)")
        
        return {
            "valid": len(issues) == 0,
            "issues": issues,
            "quality_score": output.get("metadata", {}).get("quality_score", 0)
        }
```

---

## Monitoring and Observability Patterns

### Pattern 1: Agent Performance Metrics

```python
# Track agent performance

class AgentMetrics:
    """
    Collect and analyze agent performance metrics
    """
    
    def __init__(self):
        self.metrics = {
            "total_runs": 0,
            "successful_runs": 0,
            "failed_runs": 0,
            "avg_response_time": 0,
            "total_tokens_used": 0,
            "total_cost": 0,
            "error_types": {}
        }
    
    def record_run(self, success, response_time, tokens_used, cost, error_type=None):
        """Record metrics for single agent run"""
        self.metrics["total_runs"] += 1
        
        if success:
            self.metrics["successful_runs"] += 1
        else:
            self.metrics["failed_runs"] += 1
            if error_type:
                self.metrics["error_types"][error_type] = \
                    self.metrics["error_types"].get(error_type, 0) + 1
        
        # Update averages
        n = self.metrics["total_runs"]
        self.metrics["avg_response_time"] = \
            (self.metrics["avg_response_time"] * (n-1) + response_time) / n
        
        self.metrics["total_tokens_used"] += tokens_used
        self.metrics["total_cost"] += cost
    
    def get_summary(self):
        """Get performance summary"""
        success_rate = 0
        if self.metrics["total_runs"] > 0:
            success_rate = (self.metrics["successful_runs"] / 
                           self.metrics["total_runs"] * 100)
        
        return {
            "success_rate": f"{success_rate:.1f}%",
            "total_runs": self.metrics["total_runs"],
            "avg_response_time": f"{self.metrics['avg_response_time']:.2f}s",
            "total_cost": f"${self.metrics['total_cost']:.2f}",
            "most_common_errors": sorted(
                self.metrics["error_types"].items(),
                key=lambda x: x[1],
                reverse=True
            )[:5]
        }
```
