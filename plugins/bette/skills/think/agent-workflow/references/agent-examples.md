# Agent Workflow Examples and Case Studies

## Example 1: Customer Refund Agent (Simple Single Agent)

### Problem Statement
E-commerce company receives 200+ refund requests daily. Manual processing takes 5-10 minutes per request. Goal: Automate refund approvals for straightforward cases.

### Agent Design

**Scope (Step 1):**
"An agent that processes refund requests for orders under $200, pulls order and customer history from Shopify API, checks refund eligibility rules, and either auto-approves or escalates to human review"

**Input/Output Structure (Step 2):**
```json
Input: {
  "request_id": "string",
  "customer_email": "string",
  "order_id": "string",
  "reason": "string",
  "requested_amount": "number"
}

Output: {
  "decision": "approve | escalate | deny",
  "approved_amount": "number | null",
  "reasoning": "string",
  "escalation_reason": "string | null",
  "customer_message": "string"
}
```

**System Instructions (Step 3):**
```
You are a customer refund specialist for an e-commerce company.

ROLE: Process refund requests following company policies while maintaining excellent customer experience.

APPROVAL RULES:
1. Auto-approve if:
   - Order < $200
   - Purchase within 30 days
   - No previous refunds in past 90 days
   - Product in refundable category

2. Escalate if:
   - Order >= $200
   - Purchase > 30 days ago
   - Customer has 2+ refunds in past 90 days
   - Fraud indicators present

3. Deny if:
   - Product is non-refundable (digital goods, custom items)
   - No valid order found

OUTPUT FORMAT: Always return valid JSON with all required fields.

TONE: Empathetic, professional, solution-oriented in customer messages.
```

**Tools Needed (Step 4):**
- Shopify API client (get order details)
- Customer database query (refund history)
- Email API (send confirmation)

**Architecture (Layers):**
- Layer 4 (Tooling): Shopify API, customer DB
- Layer 5 (Reasoning): Rule-based logic with edge case handling
- Layer 7 (Application): API endpoint accepting JSON requests
- Layer 8 (Ops): Log all decisions, track approval rates

**Result:**
- 70% of requests auto-processed
- Average processing time: 30 seconds (vs. 5-10 minutes manual)
- 95% accuracy rate (5% escalated appropriately)

---

## Example 2: Sales Qualification Multi-Agent

### Problem Statement
Sales team spends hours researching leads before outreach. Need to automatically qualify leads, research company background, and draft personalized outreach.

### Agent Design

**Scope (Step 1):**
"A multi-agent system that takes a lead name/company, researches company background and pain points, scores lead quality based on ICP criteria, and drafts personalized outreach email with relevant case studies"

**Multi-Agent Architecture (Step 5):**

**Agent 1: Research Agent**
- Tools: Web search, LinkedIn API, company website crawler
- Output: Company info, employee count, tech stack, recent news
- Time: 2-3 minutes

**Agent 2: Qualification Agent**
- Input: Research data + ICP criteria
- Logic: Score against ideal customer profile
- Output: Lead score (0-100), qualification reasoning
- Time: 30 seconds

**Agent 3: Content Agent**
- Input: Qualification data + case study database
- Tools: Internal CRM, case study repository
- Output: Relevant case studies, pain point mapping
- Time: 1 minute

**Agent 4: Writing Agent**
- Input: All above data
- Output: Personalized email draft
- Quality check: Tone, length, personalization level
- Time: 1 minute

**Orchestration:**
Research → Qualification → (if qualified) → Content + Writing (parallel) → Output

**System Instructions Example (Agent 2 - Qualification):**
```
You are a B2B SaaS sales qualification specialist.

IDEAL CUSTOMER PROFILE:
- Company size: 50-500 employees
- Industry: SaaS, FinTech, E-commerce
- Tech stack: React, Node.js, PostgreSQL
- Pain points: Scaling issues, data management, API complexity

SCORING RUBRIC:
- Company size match: 30 points
- Industry match: 25 points
- Tech stack overlap: 25 points
- Identified pain points: 20 points

QUALIFICATION TIERS:
- 80-100: Hot lead (immediate outreach)
- 60-79: Warm lead (nurture sequence)
- 40-59: Cold lead (newsletter only)
- <40: Not qualified (skip)

OUTPUT: Return JSON with score, tier, reasoning for each criterion.
```

**Architecture (Layers):**
- Layer 2 (Agent Internet): Custom orchestration layer
- Layer 4 (Tooling): Web search, LinkedIn API, CRM integration
- Layer 5 (Cognition): Each agent has specialized reasoning
- Layer 6 (Memory): Store research to avoid re-processing same lead
- Layer 7 (Application): Slack bot interface for sales team
- Layer 8 (Ops): Track qualification accuracy, cost per lead

**Result:**
- Lead research time: 5-10 minutes (vs. 2 hours manual)
- Qualification accuracy: 85%
- Email personalization quality: 90% of drafts used with minor edits
- Sales team productivity: 3x increase in qualified outreach volume

---

## Example 3: Code Review Agent (Specialized Single Agent)

### Problem Statement
Engineering team needs consistent code review feedback. Junior developers wait hours for senior review. Goal: Provide instant first-pass review focusing on common issues.

### Agent Design

**Scope (Step 1):**
"An agent that reviews pull requests, checks for code quality issues, security vulnerabilities, and style violations, then provides structured feedback with severity levels and suggested fixes"

**Input/Output Structure (Step 2):**
```json
Input: {
  "pr_url": "string",
  "files_changed": ["string"],
  "programming_language": "string"
}

Output: {
  "overall_score": "number (0-100)",
  "issues": [
    {
      "severity": "critical | high | medium | low",
      "category": "security | performance | style | logic",
      "file": "string",
      "line": "number",
      "description": "string",
      "suggested_fix": "string"
    }
  ],
  "approval_recommendation": "approve | request_changes | needs_senior_review",
  "summary": "string"
}
```

**System Instructions (Step 3):**
```
You are a senior software engineer performing code reviews.

REVIEW CRITERIA:
1. Security: SQL injection, XSS, authentication issues, exposed secrets
2. Performance: N+1 queries, unnecessary loops, memory leaks
3. Code Quality: Complexity, duplication, naming conventions
4. Style: Follows team guidelines, consistent formatting
5. Logic: Edge cases, error handling, validation

SEVERITY LEVELS:
- Critical: Security vulnerabilities, breaking bugs (block merge)
- High: Performance issues, major logic flaws (request changes)
- Medium: Code quality, minor issues (suggest improvements)
- Low: Style preferences, nitpicks (optional)

REVIEW PROCESS:
1. Analyze each changed file
2. Identify issues with severity and category
3. Provide specific, actionable feedback
4. Suggest fixes with code examples when possible
5. Recommend approval status

TONE: Constructive, educational, specific. Praise good patterns.
```

**Tools Needed (Step 4):**
- GitHub API (fetch PR details, file diffs)
- Static analysis tools (ESLint, Pylint, SonarQube)
- Security scanner (Snyk, npm audit)
- Custom linting rules

**Architecture (Layers):**
- Layer 4 (Tooling): GitHub API, static analysis tools
- Layer 5 (Reasoning): Pattern recognition, security analysis
- Layer 7 (Application): GitHub bot commenting on PRs
- Layer 8 (Ops): Track false positive rate, developer satisfaction

**Memory Strategy (Step 6):**
- Store team coding patterns and preferences
- Remember past issues per developer (personalize feedback)
- Learn from senior engineer overrides (improve accuracy)

**Result:**
- Initial review time: 2-3 minutes (vs. 2-4 hours wait)
- Critical issue detection: 95%
- False positive rate: 10%
- Senior engineer review time saved: 60%
- Junior developer satisfaction: High (instant feedback accelerates learning)

---

## Example 4: Content Marketing Multi-Agent System

### Problem Statement
Content team needs to research topics, create outlines, write drafts, and optimize for SEO. Current process takes 8-10 hours per article. Goal: Accelerate high-quality content production.

### Agent Design

**Scope (Step 1):**
"A multi-agent system that researches trending topics and keywords, creates detailed article outlines, generates long-form content drafts, and optimizes for SEO while maintaining brand voice"

**Multi-Agent Architecture (Step 5):**

**Agent 1: Topic Research Agent**
- Tools: Google Trends API, competitor blog crawler, keyword research tools
- Input: Topic theme or industry
- Output: Trending topics, search volumes, competition analysis
- Reasoning: Identify content gaps and opportunities

**Agent 2: Outline Agent**
- Input: Selected topic + research data
- Tools: Internal content database (avoid duplication)
- Output: Detailed outline with section headers, key points, target word count
- Reasoning: Structure for maximum engagement and completeness

**Agent 3: Writing Agent**
- Input: Outline + brand guidelines + previous articles
- Output: Full article draft (2000-3000 words)
- Style: Matches brand voice using examples from past articles
- Quality: Fact-checking, coherence, flow

**Agent 4: SEO Optimization Agent**
- Input: Article draft + keyword research
- Tools: SEO analysis tools (keyword density, readability)
- Output: Optimized version with meta description, headings, internal links
- Reasoning: Balance SEO requirements with readability

**Agent 5: QA Agent**
- Input: Final draft
- Checks: Factual accuracy, grammar, plagiarism, brand voice consistency
- Output: Approval or revision requests with specific issues
- Reasoning: Quality gating before publication

**Orchestration:**
Topic Research → Outline → Writing → SEO Optimization → QA
(If QA fails: Writing revises based on feedback)

**System Instructions Example (Agent 3 - Writing):**
```
You are a content writer specializing in B2B SaaS marketing.

BRAND VOICE:
- Tone: Professional but conversational
- Perspective: Second person ("you") for engagement
- Style: Data-driven, actionable, example-rich
- Avoid: Jargon, clichés, fluff

CONTENT STRUCTURE:
1. Hook: Compelling opening with stat or question
2. Problem: Clearly articulate reader's pain point
3. Solution: In-depth explanation with examples
4. Implementation: Step-by-step actionable guidance
5. Results: Expected outcomes and success metrics
6. CTA: Relevant next step (demo, download, read more)

QUALITY STANDARDS:
- Use subheadings every 200-300 words
- Include 2-3 data points per section
- Provide concrete examples (not hypothetical)
- Link to authoritative sources
- Vary sentence length for readability
- End sections with transition to next topic

TARGET: 2500 words, grade 8-10 reading level.
```

**Architecture (Layers):**
- Layer 2 (Agent Internet): Complex orchestration with feedback loops
- Layer 4 (Tooling): Google Trends, SEO tools, CMS integration
- Layer 5 (Cognition): Each agent specialized reasoning
- Layer 6 (Memory): Brand voice examples, past article performance
- Layer 7 (Application): Web dashboard for content team
- Layer 8 (Ops): Track content quality scores, publish rate, SEO performance

**Result:**
- Article creation time: 2-3 hours (vs. 8-10 hours)
- Content quality: 85% publish-ready with minor edits
- SEO score: 90+ average (Yoast/similar tools)
- Publishing frequency: 3x increase
- Content team satisfaction: High (focus on strategy vs. grinding)

---

## Decision Framework Examples

### When Single Agent is Sufficient

**Scenario: Password Reset Agent**
- Linear workflow: Verify identity → Generate token → Send email
- No sub-task specialization needed
- Decision-making is straightforward
- Context maintained throughout
**Recommendation:** Single agent with 3-4 tools

**Scenario: Invoice Processing**
- Extract data from PDF → Validate against PO → Route for approval
- Sequential steps with clear handoffs
- Unified context improves accuracy
**Recommendation:** Single agent with document processing tools

### When Multi-Agent is Beneficial

**Scenario: Competitive Intelligence System**
- Research (web scraping multiple sources)
- Analysis (compare features, pricing, positioning)
- Reporting (create executive summary)
- Monitoring (track changes over time)
Each sub-task needs specialized expertise
**Recommendation:** 4-agent system with orchestrator

**Scenario: Customer Onboarding Flow**
- Welcome agent (personalized greetings, account setup)
- Education agent (product tours, documentation links)
- Support agent (answer questions, troubleshoot)
- Success agent (track progress, identify blockers)
Parallel processes improve user experience
**Recommendation:** 4-agent system with shared memory

---

## Common Tool Integration Patterns

### Pattern 1: CRM Integration (Salesforce Example)

**Use Case:** Sales qualification agent needs customer data

**Tools Required:**
- Salesforce REST API
- Authentication handler (OAuth 2.0)
- Rate limiter (API call limits)

**Implementation:**
```python
# System instructions snippet
You have access to Salesforce via the get_customer_data tool.

INPUT: {"customer_email": "string"}
OUTPUT: {"account": {...}, "opportunities": [...], "cases": [...]}

When analyzing customer fit:
1. Call get_customer_data with customer email
2. Review account details (industry, size, ARR)
3. Check open opportunities (deal stage, amount)
4. Review case history (support issues, satisfaction)
5. Synthesize into qualification score
```

### Pattern 2: Document Processing

**Use Case:** Contract review agent

**Tools Required:**
- PDF extraction (pdfplumber)
- OCR for scanned docs (Tesseract)
- NLP for clause identification
- Document comparison

**Workflow:**
1. Extract text from PDF
2. Identify key sections (payment terms, liability, termination)
3. Flag non-standard clauses
4. Compare against template
5. Generate review summary

### Pattern 3: Real-Time Data Integration

**Use Case:** Trading recommendation agent

**Tools Required:**
- Market data API (real-time prices)
- News aggregation API
- Portfolio database
- Risk calculator

**Considerations:**
- Latency: Sub-second response required
- Caching: Avoid redundant API calls
- Fallback: Handle API failures gracefully
- Cost: Monitor API usage costs

---

## Error Handling Patterns

### Pattern 1: Graceful Degradation

```
If primary tool fails:
1. Log error details
2. Try fallback tool/method
3. If all fail: Return partial result with disclaimer
4. Never leave user hanging with "error occurred"

Example: Web search fails
→ Use cached data if available
→ Provide general guidance
→ Explain limitation to user
```

### Pattern 2: Human-in-the-Loop for Critical Decisions

```
For high-stakes decisions:
1. Agent provides recommendation + confidence score
2. If confidence < 85%: Flag for human review
3. Include reasoning and alternative options
4. Log human decision to improve future accuracy

Example: $10K+ refund request
→ Agent analyzes and recommends
→ Requires manager approval
→ Manager sees full context and reasoning
```

### Pattern 3: Retry with Clarification

```
If input is ambiguous or incomplete:
1. Identify missing information
2. Request specific clarification from user
3. Provide examples of valid input
4. Never guess or make assumptions

Example: Vague customer complaint
→ Ask: "What product/service does this concern?"
→ Ask: "What is the desired outcome?"
→ Proceed only with sufficient information
```

---

## Cost Optimization Strategies

### Strategy 1: Prompt Caching

For repeated context (system instructions, knowledge base):
- Cache stable content (reduces tokens by 90%)
- Update cache only when content changes
- Massive savings for high-volume agents

### Strategy 2: Tool Call Optimization

- Batch API calls when possible
- Cache frequent queries
- Use webhooks vs. polling
- Implement circuit breakers for flaky APIs

### Strategy 3: Model Tiering

- Use cheaper model (GPT-3.5) for simple tasks
- Route to powerful model (GPT-4) only when needed
- Classify complexity before routing

**Example:**
```
Query: "What's our return policy?"
→ Use GPT-3.5 (simple lookup)

Query: "Analyze this customer situation and recommend solution"
→ Use GPT-4 (complex reasoning)
```

### Strategy 4: Output Length Control

- Specify max tokens in system prompt
- Use structured outputs (JSON) to avoid verbosity
- Trim unnecessary context from conversation history

**Result:** 40-60% cost reduction without quality loss
