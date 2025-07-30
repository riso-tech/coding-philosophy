# Code Style and Coding Standards

## Naming Philosophy

### 1. Descriptive Over Concise
**Principle**: Names must be self-documenting, prefer clarity over brevity

**Guidelines**:
- Use full words instead of abbreviations: `configuration` instead of `config`
- Function names should describe what they do: `validateUserInput()` instead of `validate()`
- Variable names should describe what they contain: `userEmail` instead of `email`
- Boolean variables should be questions: `isValid`, `hasPermission`, `canExecute`

### 2. Consistent Naming Patterns
**Variables and Functions**:
- Use consistent casing convention throughout project
- Prefix/suffix patterns for related functionality
- Namespace-like naming for utilities: `log_info()`, `log_error()`

**Files and Directories**:
- Consistent case convention (kebab-case, camelCase, snake_case)
- Descriptive names that indicate purpose
- Group related files with common prefixes

### 3. Context-Aware Naming
**Principles**:
- Names should make sense in their context
- Avoid redundant prefixes when context is clear
- Use domain-specific terminology consistently
- Abbreviations only for well-known industry standards

### 4. Abstraction-First Naming for Multiple Cases
**Principle**: When supporting multiple variants/cases, use abstract interface names with switch-case implementation rather than variant-specific function names.

**Pattern from Session**: Multi-OS support analysis revealed this scalable approach
- Use consistent function names across all variants: `install_packages()` not `apt_install()` vs `apk_install()`
- Abstract variant-specific details behind common interfaces
- File naming that indicates multi-case intent: `install-common.sh`, `detect-environment.sh`

**Universal Application**:
- **Multi-OS Support**: `install_packages()`, `detect_os()`, `configure_shell()`
- **Multi-Language Projects**: `setup_linter()`, `run_tests()`, `build_project()`
- **Multi-Environment**: `deploy_app()`, `configure_database()`, `setup_monitoring()`
- **Multi-User Context**: `setup_permissions()`, `configure_workspace()`, `install_tools()`

**Implementation Pattern**:
```bash
# Good - Abstract interface with switch-case optimization
install_packages() {
    case "$OS_TYPE" in
        "alpine") apk add --no-cache "$@" ;;
        "debian"|"ubuntu") apt-get update && apt-get install -y "$@" ;;
        "fedora"|"centos") yum install -y "$@" ;;
        *) log_error "Unsupported OS: $OS_TYPE"; exit 1 ;;
    esac
}

setup_linter() {
    case "$PROJECT_TYPE" in
        "javascript"|"typescript") npm install -D eslint prettier ;;
        "python") pip install flake8 black ;;
        "go") go install golang.org/x/tools/cmd/goimports@latest ;;
        *) log_warning "No linter configuration for: $PROJECT_TYPE" ;;
    esac
}

# Avoid - Variant-specific naming (creates code duplication)
apt_install_packages() { ... }
yum_install_packages() { ... }
javascript_setup_linter() { ... }
python_setup_linter() { ... }
```

**Benefits**:
- **Scalability**: Easy to add new variants without changing interface
- **Maintainability**: Single function to maintain instead of multiple variants
- **Consistency**: Same interface regardless of underlying implementation
- **Testability**: One interface to test with different contexts

## Code Structure Patterns

### 1. Function Design Philosophy
**Single Responsibility**:
- Each function should do one thing well
- Function length should be readable in single screen
- Clear input/output contracts
- Minimal side effects

**Error Handling**:
- Functions should handle their own errors when possible
- Return error indicators rather than silent failures
- Provide meaningful error messages
- Document error conditions

### 2. Variable Management
**Scope Management**:
- Declare variables close to where they're used
- Use const/readonly when values don't change
- Minimize global state
- Clear variable lifetime management

**State Tracking**:
- Use explicit state variables for complex operations
- Boolean flags for status tracking
- Arrays/collections for accumulating results
- Clear state initialization and cleanup

### 3. Control Flow Patterns
**Early Returns**:
- Use early returns to reduce nesting
- Guard clauses for validation
- Clear success path through code
- Minimal cognitive complexity

**Loop and Iteration**:
- Clear loop termination conditions
- Avoid complex nested loops
- Extract loop bodies into functions when complex
- Iterator patterns for collection processing

## Documentation Standards

### 1. Code Comments Philosophy
**When to Comment**:
- **Why** decisions were made, not **what** code does
- Complex algorithms that aren't immediately obvious
- Business logic requirements
- Workarounds and their reasons

**Comment Quality**:
- Keep comments up-to-date with code changes
- Use consistent comment formatting
- Avoid obvious comments
- Focus on maintainer's perspective

### 2. Function Documentation
**Required Elements**:
- Purpose and behavior description
- Parameter descriptions and types
- Return value specifications
- Error conditions and handling
- Usage examples for complex functions

### 3. File and Module Documentation
**Header Comments**:
- File purpose and responsibility
- Dependencies and requirements
- Author and maintenance info
- Usage guidelines

## Formatting Standards

### 1. Consistency Principles
**Visual Structure**:
- Consistent indentation throughout project
- Clear section separations
- Aligned assignments when beneficial
- Consistent spacing around operators

**Line Management**:
- Reasonable line length limits
- Logical line breaks for readability
- Consistent continuation patterns
- Clear statement termination

### 2. Code Organization Within Files
**Section Organization**:
- Logical grouping of related functions
- Clear separation between sections
- Consistent ordering patterns
- Related code co-located

**Import/Dependency Management**:
- Clear dependency declarations
- Logical grouping of imports
- Minimize circular dependencies
- Version-specific requirements documented

## Error Handling Style

### 1. Error Communication
**User-Facing Errors**:
- Clear, actionable error messages
- Contextual information for debugging
- Consistent error formatting
- Escalation paths for complex issues

**Developer-Facing Errors**:
- Detailed error context
- Stack traces when helpful
- Error categorization
- Recovery suggestions

### 2. Error Recovery Patterns
**Graceful Degradation**:
- Fallback strategies for non-critical failures
- Partial success reporting
- Continue-on-error options
- Clear failure boundaries

## Performance Considerations

### 1. Efficiency Patterns
**Resource Management**:
- Explicit resource cleanup
- Avoid unnecessary computations
- Cache expensive operations
- Memory usage awareness

**Algorithm Choice**:
- Appropriate data structures for use case
- Consider time/space complexity
- Profile before optimizing
- Readability vs performance trade-offs

### 2. Scalability Patterns
**Design for Growth**:
- Algorithms that scale with data size
- Configurable resource limits
- Modular designs for horizontal scaling
- Performance monitoring hooks

## Security Considerations

### 1. Input Validation
**Validation Patterns**:
- Validate all external inputs
- Sanitize data before processing
- Use allowlists rather than blocklists
- Fail securely on validation errors

### 2. Output Security
**Data Exposure**:
- Minimize information leakage in errors
- Secure logging practices
- Sanitize output data
- Protect sensitive information

## Shell Script Standards

### 1. Script Structure and Safety
**Essential Script Headers**:
```bash
#!/bin/bash
set -e  # Exit on any error
```

**Error Handling Philosophy**:
- Use `set -e` for immediate error termination
- Validate prerequisites before main execution
- Provide clear error messages with context
- Exit with appropriate error codes

### 2. Logging and Output Standards
**Structured Logging Functions**:
```bash
# Color constants for consistent output
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
BLUE='\033[0;34m'
CYAN='\033[0;36m'
PURPLE='\033[0;35m'
NC='\033[0m' # No Color

# Standardized logging functions
log_info() {
    echo -e "${BLUE}[$(date '+%Y-%m-%d %H:%M:%S')]${NC} ${CYAN}[INFO]${NC} $1"
}

log_success() {
    echo -e "${BLUE}[$(date '+%Y-%m-%d %H:%M:%S')]${NC} ${GREEN}[SUCCESS]${NC} $1"
}

log_warning() {
    echo -e "${BLUE}[$(date '+%Y-%m-%d %H:%M:%S')]${NC} ${YELLOW}[WARNING]${NC} $1"
}

log_error() {
    echo -e "${BLUE}[$(date '+%Y-%m-%d %H:%M:%S')]${NC} ${RED}[ERROR]${NC} $1"
}
```

**Output Formatting Principles**:
- Timestamp all log messages for debugging
- Use color coding for different log levels
- Consistent message formatting across scripts
- Clear visual separators for script sections

### 3. Script Organization Patterns
**Step-Based Execution**:
```bash
# ========================================
# STEP 1: DESCRIPTIVE STEP NAME
# ========================================
echo ""
log_info "Step 1/3: Clear description of what this step does..."
```

**Visual Section Separators**:
- Use consistent comment headers with equal signs
- Clear step numbering (Step X/Y format)
- Empty lines for visual breathing space
- Descriptive section titles

### 4. Variable and State Management
**Progress Tracking**:
```bash
# Progress tracking variables
COMPONENT_INSTALLED=false
INSTALLED_ITEMS=()
MAX_WAIT=30
WAIT_COUNT=0
```

**Environment Handling**:
- Get current user context: `CURRENT_USER=$(whoami)`
- Set environment variables with defaults: `${VAR:-default_value}`
- Validate environment before proceeding
- Clear variable initialization

### 5. Command Execution Patterns
**Safe Command Execution**:
```bash
# Check command availability
if ! command -v required_tool &> /dev/null; then
    log_error "Required tool not found"
    exit 1
fi

# Conditional command execution with logging
if some_command 2>/dev/null; then
    log_success "✓ Command succeeded"
else
    log_warning "⚠ Command failed (continuing anyway)"
fi
```

**Wait and Retry Patterns**:
```bash
# Wait for conditions with timeout
while [ ! -d "$TARGET_DIR" ] && [ $WAIT_COUNT -lt $MAX_WAIT ]; do
    log_info "Waiting for condition..."
    sleep 1
    WAIT_COUNT=$((WAIT_COUNT + 1))
done
```

### 6. User Experience Guidelines
**Visual Appeal**:
- Use Unicode symbols for status (✓, ⚠, 🚀, 🎉)
- Color-coded borders for script sections
- Progressive disclosure of information
- Clear success/failure indicators

**Informative Messages**:
- Always explain what the script is doing
- Provide context for wait operations
- Show progress for multi-step operations
- Include helpful tips and next steps

### 7. Directory and File Operations
**Safe File Operations**:
```bash
# Create directories with error handling
mkdir -p /target/directory || {
    log_error "Failed to create directory"
    exit 1
}

# Copy with verification
if [ -d ./source ]; then
    find ./source -mindepth 1 -exec cp -r {} /target/ \;
    log_success "✓ Files copied successfully"
else
    log_warning "⚠ Source directory not found"
fi
```

**Path Management**:
- Always use absolute paths when possible
- Validate paths before operations
- Handle missing directories gracefully
- Clear ownership and permission handling

### 8. Script Portability Considerations
**Cross-Platform Compatibility**:
- Test command availability before use
- Handle different package managers
- Account for different tool versions
- Provide fallback options

**Environment Assumptions**:
- Document required tools and versions
- Validate runtime environment
- Clear dependency management
- Graceful degradation when possible

[TO BE SUPPLEMENTED LATER]: Language-specific style guides, linting tool configurations

**Line Management**:
- Reasonable line length limits
- Logical line breaks for readability
- Consistent continuation patterns
- Clear statement termination

### 2. Code Organization Within Files
**Section Organization**:
- Logical grouping of related functions
- Clear separation between sections
- Consistent ordering patterns
- Related code co-located

**Import/Dependency Management**:
- Clear dependency declarations
- Logical grouping of imports
- Minimize circular dependencies
- Version-specific requirements documented

## Error Handling Style

### 1. Error Communication
**User-Facing Errors**:
- Clear, actionable error messages
- Contextual information for debugging
- Consistent error formatting
- Escalation paths for complex issues

**Developer-Facing Errors**:
- Detailed error context
- Stack traces when helpful
- Error categorization
- Recovery suggestions

### 2. Error Recovery Patterns
**Graceful Degradation**:
- Fallback strategies for non-critical failures
- Partial success reporting
- Continue-on-error options
- Clear failure boundaries

## Performance Considerations

### 1. Efficiency Patterns
**Resource Management**:
- Explicit resource cleanup
- Avoid unnecessary computations
- Cache expensive operations
- Memory usage awareness

**Algorithm Choice**:
- Appropriate data structures for use case
- Consider time/space complexity
- Profile before optimizing
- Readability vs performance trade-offs

### 2. Scalability Patterns
**Design for Growth**:
- Algorithms that scale with data size
- Configurable resource limits
- Modular designs for horizontal scaling
- Performance monitoring hooks

## Security Considerations

### 1. Input Validation
**Validation Patterns**:
- Validate all external inputs
- Sanitize data before processing
- Use allowlists rather than blocklists
- Fail securely on validation errors

### 2. Output Security
**Data Exposure**:
- Minimize information leakage in errors
- Secure logging practices
- Sanitize output data
- Protect sensitive information
