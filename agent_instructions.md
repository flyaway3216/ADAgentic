# Agent Assistant Setup Instructions

This file instructs AI coding assistants on the documentation files they should automatically generate for this secure AI coder agent framework project.

## Required Documentation Files to Generate

The agent assistant should create the following documentation structure with minimal human input before proceeding to PRP generation and coding:

### Core Project Documentation
- **CLAUDE.md** - Global rules and project-specific guidelines for AI assistants
- **TESTING.md** - Test protocols, patterns, coverage requirements, and validation frameworks
- **CODE_STYLE.md** - Coding standards, formatting rules, and language conventions
- **ARCHITECTURE.md** - Code structure, organization rules, and system design principles
- **ROADMAP.md** - Project milestones, feature priorities, and development timeline

### Advanced Documentation Framework

#### Error Management
- **ERROR_PATTERNS.md** - Common error scenarios, handling patterns, and recovery strategies
- **VALIDATION_FRAMEWORK.md** - Input validation rules, security checks, and data integrity protocols

#### Architecture & Design
- **ARCHITECTURE_DECISIONS.md** (ADRs) - Record of significant architectural decisions and rationale
- **COMPONENT_INTERACTIONS.md** - Maps showing how system components interact and communicate
- **INTEGRATION_PATTERNS.md** - External service integration patterns and best practices

#### Development Workflow
- **INCREMENTAL_DEVELOPMENT.md** - Step-by-step development workflow and iteration patterns
- **SUCCESS_CRITERIA.md** - Templates for defining and measuring feature completion
- **CONTEXT_VALIDATION.md** - Commands and checks to validate AI assistant context understanding

#### Code Examples Structure
- **examples/README.md** - Comprehensive guide to all code examples and their purposes
- **examples/PROGRESSIVE_COMPLEXITY.md** - Examples ordered from simple to complex implementations
- **examples/security/README.md** - Security-focused implementation examples
- **examples/agents/README.md** - AI agent architecture and interaction examples
- **examples/integration/README.md** - External service integration examples

#### Domain-Specific Documentation
- **SECURITY_VOCABULARY.md** - Project-specific security terms, concepts, and definitions
- **AI_AGENT_VOCABULARY.md** - Domain-specific terminology for AI agent development
- **API_PATTERNS.md** - Standard API design patterns and conventions for this project

### File Generation Priority

**Phase 1 - Foundation (Generate First):**
1. CLAUDE.md
2. ARCHITECTURE.md
3. SECURITY_VOCABULARY.md
4. AI_AGENT_VOCABULARY.md

**Phase 2 - Development Framework:**
5. CODE_STYLE.md
6. TESTING.md
7. VALIDATION_FRAMEWORK.md
8. ERROR_PATTERNS.md

**Phase 3 - Advanced Structure:**
9. INTEGRATION_PATTERNS.md
10. COMPONENT_INTERACTIONS.md
11. INCREMENTAL_DEVELOPMENT.md
12. SUCCESS_CRITERIA.md

**Phase 4 - Examples and Validation:**
13. All examples/README.md files
14. PROGRESSIVE_COMPLEXITY.md
15. CONTEXT_VALIDATION.md
16. ARCHITECTURE_DECISIONS.md

## Content Generation Guidelines

### For Each File, Include:
- **Purpose**: Clear explanation of what this document covers
- **Scope**: Specific boundaries and limitations
- **Examples**: Concrete examples relevant to secure AI agent development
- **References**: Links to related documentation
- **Validation**: How to verify the guidelines are being followed

### Security-First Approach:
All generated documentation must prioritize security considerations:
- Security implications of architectural decisions
- Secure coding patterns and anti-patterns
- Threat modeling considerations
- Input validation and sanitization requirements
- Authentication and authorization patterns

### AI Agent Context:
Documentation should be optimized for AI agent development:
- Clear interaction patterns between agents
- State management in multi-agent systems
- Error propagation in agent networks
- Performance considerations for agent operations
- Scalability patterns for agent frameworks

## Validation Commands

The agent should create context validation commands in **CONTEXT_VALIDATION.md** that include:
- Commands to verify understanding of project architecture
- Security requirement comprehension checks  
- Code style compliance verification
- Integration pattern understanding tests
- Success criteria evaluation methods

## Success Criteria for Documentation Generation

Each generated file must:
- [ ] Be immediately usable without human editing
- [ ] Include practical, project-specific examples
- [ ] Reference other relevant documentation files
- [ ] Include validation methods or checklists
- [ ] Align with security-first development principles
- [ ] Support incremental development workflow
- [ ] Enable context-rich AI assistant interactions

## Post-Generation Workflow

After generating all documentation:
1. Run context validation commands to verify AI understanding
2. Generate initial PRP using the comprehensive documentation context  
3. Execute development workflow following incremental patterns
4. Update Architecture Decision Records for significant choices
5. Validate all implementations against success criteria templates

---

**Note for AI Assistants**: This file structure is designed to provide comprehensive context for secure AI agent framework development. Generate all files with rich, actionable content that enables autonomous development while maintaining security and quality standards.