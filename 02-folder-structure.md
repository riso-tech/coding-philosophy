# Folder Organization and Module Structure

## Folder Architecture Philosophy

### 1. Feature-Centric Organization
**Principle**: Each module/feature is a **self-contained unit** with standardized and predictable structure.

**Why**: Predictable structure enables fast navigation, easy maintenance, clear ownership boundaries.

**General Structure**:
```
feature-or-module/
├── metadata/config file      # Declare dependencies, settings
├── main implementation       # Core logic
├── documentation            # Complete usage guide
├── configurations/          # Pre-configured files
└── supporting-scripts/      # Lifecycle/utility scripts
```

### 2. Lifecycle-Based Separation
**Principle**: Separate logic by lifecycle/responsibility instead of monolithic implementations.

**Approaches**:
- **Initialization**: System-level setup, dependencies
- **Configuration**: User-space setup, customization
- **Runtime**: Active operation logic
- **Cleanup**: Resource cleanup, state reset

**Benefits**:
- Clear responsibility boundaries
- Easier debugging and maintenance
- Better error isolation
- Modular testing possible

### 3. Conditional Structure Respect
**Principle**: Respect existing project structure rather than forcing templates.

**Learned from Session**: "không cần template, mỗi dự án mỗi khác"
- Check for existing files before creating new ones
- Enhance existing structure rather than replace it
- Provide options without mandating specific layouts

**Implementation**:
```bash
# Check before creating
[ ! -f "README.md" ] && create_readme
[ ! -d ".github" ] && setup_github_workflows
[ ! -f "package.json" ] && [ "$ENABLE_NODE" = "true" ] && init_node_project
```

**Why Better**:
- Works with diverse project needs
- Non-intrusive enhancement
- Preserves user's established patterns

### 4. Configuration Management Strategy
**Principle**: Separate configuration data from implementation logic.

**Patterns**:
- Pre-configured defaults for immediate productivity
- Template-based configuration generation
- Environment-specific overrides
- Validation mechanisms for configuration integrity

## Module Organization Patterns

### 1. Utility-First Approach
**Principle**: Extract common functionality into reusable utilities

**Benefits**:
- DRY principle adherence
- Consistent behavior across modules
- Easier testing and maintenance
- Clear API boundaries

**Organization**:
- Group utilities by domain/responsibility
- Consistent naming conventions
- Well-documented interfaces
- Version compatibility considerations

### 2. Step-Based Execution Flow
**Principle**: Organize complex operations into sequential, trackable steps

**Structure**:
- Clear step boundaries with progress indicators
- Error handling at each step
- Rollback capabilities when possible
- Summary reporting for completed operations

### 3. State Management Patterns
**Principle**: Explicit state tracking and validation

**Approaches**:
- State variables for progress tracking
- Validation checkpoints throughout execution
- Idempotency markers to avoid duplicate work
- State persistence for recovery scenarios

## Directory Standards

### 1. Naming Conventions
**Principles**:
- **Descriptive over abbreviated**: `authentication` instead of `auth`
- **Consistent casing**: Stick to one convention (kebab-case, camelCase, etc.)
- **Hierarchical organization**: Group related functionality
- **Future-proof naming**: Avoid overly specific names

### 2. Logical Grouping
**Source Code**:
- Group by feature/domain rather than technical layer
- Co-locate related functionality
- Minimize cross-dependencies

**Configuration**:
- Environment-specific configurations
- Template files separated from instances
- Validation schemas alongside configs

**Documentation**:
- Co-located with relevant code
- Hierarchical structure matching code organization
- Cross-references for related concepts

### 3. Dependency Management
**Principles**:
- Clear dependency declarations
- Minimal coupling between modules
- Explicit interface definitions
- Version pinning strategies

## Testing Organization

### 1. Test Structure Philosophy
**Principle**: Test organization should mirror and validate production structure

**Approaches**:
- Test files co-located with code they test
- Integration tests separated from unit tests
- Performance tests in dedicated areas
- Test utilities shared across test suites

### 2. Test Categorization
**Levels**:
- **Unit**: Individual function/module testing
- **Integration**: Cross-module interaction testing
- **System**: End-to-end workflow testing
- **Performance**: Resource usage and timing validation

### 3. Test Documentation
**Requirements**:
- Clear test purpose and scope
- Setup and teardown procedures
- Expected outcomes and success criteria
- Troubleshooting guides for failures

## Build and Automation Organization

### 1. Build Tool Philosophy
**Principle**: Build processes should be self-documenting and consistent

**Structure**:
- Clear section separation in build files
- Helper functions with descriptive names
- Consistent variable naming conventions
- Color-coded output for usability

### 2. Automation Principles
**Goals**:
- Make everything scriptable
- Self-documenting processes
- Built-in validation and error checking
- Cleanup automation

### 3. Documentation Integration
**Approaches**:
- Inline help systems
- Auto-generated documentation from code
- Examples embedded in build files
- Troubleshooting guides integrated

## Scalability Considerations

### 1. Growth Patterns
**Prepare for**:
- Module proliferation
- Cross-module dependencies
- Team collaboration needs
- Legacy compatibility requirements

### 2. Refactoring Strategies
**Approaches**:
- Gradual migration paths
- Backward compatibility layers
- Clear deprecation policies
- Migration tooling when needed

[TO BE SUPPLEMENTED LATER]: Guidelines for large-scale project organization, monorepo vs polyrepo strategies
