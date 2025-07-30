# Programming Philosophy and Principles

## Core Philosophy

### 1. Zero-Configuration Philosophy
**Principle**: Prioritize creating solutions that **"work immediately"** without requiring complex configuration from users.

**Why**: Focus on user experience - they want immediate productivity, not time spent on setup.

**Implementation**:
- Create sensible defaults for all configurations
- Apply 80/20 rule - optimize for 80% of common use cases
- Provide customization options for advanced users
- Progressive disclosure - show basics first, advanced features later

### 2. Dependency Orchestration
**Principle**: Manage dependencies elegantly through composition patterns instead of tightly coupled implementations.

**Why**: Avoid conflicts, leverage existing ecosystem, clear separation of concerns.

**Implementation**:
- Declare dependencies explicitly rather than assume
- Implement waiting/polling patterns for async dependencies
- Provide graceful fallbacks for optional dependencies
- Use composition over inheritance when possible

### 3. Constraint-Driven Development
**Principle**: Embrace constraints as creative catalysts rather than limitations.

**Learned from Session**: "không cần template, mỗi dự án mỗi khác" led to better conditional approach
- Real-world constraints often reveal better solutions than theoretical perfection
- User limitations drive more practical, maintainable implementations
- Performance constraints force architectural clarity

**Implementation**:
- Start with user constraints and work backwards to solution
- Use limitations to eliminate over-engineering
- Validate assumptions against real usage patterns

### 4. Idempotent Operations
**Principle**: All operations must be safe to run multiple times without causing side effects.

**Why**: Ensure reliability, easier debugging, safe when re-running.

**Implementation**:
- Check-before-modify patterns
- Backup mechanisms before changing critical files
- State tracking to avoid duplicate work
- Use atomic operations when possible

### 4. Progressive Enhancement
**Principle**: Build upon existing foundations, enhance rather than replace.

**Why**: Leverage ecosystem, avoid reinventing the wheel, higher maintainability.

**Implementation**:
- Build on proven, stable foundations
- Add value layers without breaking base functionality
- Maintain backward compatibility
- Provide clear migration paths

## Design Principles

### 1. User-Centric Design
**Principle**: Always prioritize user experience in every decision

**Implementation**:
- Rich feedback with progress indicators
- Clear error messages with actionable advice
- Comprehensive integrated documentation
- Visual formatting for readability

### 2. Fail-Safe Defaults
**Principle**: Systems must be resilient and recover gracefully from failures

**Implementation**:
- Warnings instead of hard errors when possible
- Multiple fallback strategies
- Continue execution on non-critical failures
- Clear escalation paths for serious errors

### 3. Observability First
**Principle**: Visibility into system behavior is a prerequisite for reliability

**Implementation**:
- Structured logging with consistent format
- Timestamped events for debugging
- Progress tracking and summary reports
- Persistent logs for post-mortem analysis

### 4. Maintainability Over Cleverness
**Principle**: Clear, understandable code is more important than "clever" code

**Implementation**:
- Explicit over implicit behavior
- Function composition over monolithic scripts
- Descriptive naming for variables and functions
- Clear separation of concerns

## Core Values Framework

### 1. Reliability
- Operations must be predictable and repeatable
- Comprehensive error handling for edge cases
- Recovery mechanisms for failure scenarios
- Testing coverage for critical paths

### 2. Usability
- Minimize cognitive load for users
- Provide immediate value with minimal setup
- Clear documentation and examples
- Progressive disclosure of complexity

### 3. Extensibility
- Design for future needs without over-engineering
- Clear extension points and interfaces
- Configuration hooks for customization
- Backward compatibility considerations

### 4. Performance
- Optimize for common use cases
- Resource efficiency in implementations
- Caching strategies for expensive operations
- Cleanup automation to avoid bloat

## Decision Framework

When making architectural decisions, prioritize in this order:

1. **User Experience** - Does it improve user's workflow?
2. **Reliability** - Does it ensure consistent behavior?
3. **Maintainability** - Is it sustainable in the long term?
4. **Performance** - Does it provide efficient resource utilization?

**Trade-off Philosophy**:
- User convenience vs System security → Lean toward convenience with safety nets
- Performance vs Readability → Optimize for readability first, performance second
- Features vs Simplicity → Prefer simple solutions that solve 80% of problems
- Speed vs Quality → Never compromise quality for short-term speed gains
