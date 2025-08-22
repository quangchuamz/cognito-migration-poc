# Cognito Cross-Account & Cross-Region Migration POC

A Proof of Concept (POC) for implementing Amazon Cognito user pool migration across AWS accounts and regions using User Migration Lambda triggers. This project demonstrates seamless user migration while preserving passwords and authentication capabilities.

## 🎯 Project Overview

This project implements a solution to migrate users from:
- **Source**: Account A, Region A (Cognito User Pool)
- **Target**: Account B, Region B (Cognito User Pool)

### Key Features
- ✅ **Password Preservation**: Users keep their existing passwords
- ✅ **Seamless Migration**: Users migrate on first sign-in attempt
- ✅ **Cross-Account Security**: Secure IAM role-based authentication
- ✅ **Comprehensive Logging**: Full audit trail and monitoring
- ✅ **Error Handling**: Robust error handling and recovery

## 🏗️ Architecture

```
┌─────────────────┐    Migration Request    ┌─────────────────┐
│   Account A     │◄─────────────────────────│   Account B     │
│   Region A      │                          │   Region B      │
│                 │                          │                 │
│ ┌─────────────┐ │                          │ ┌─────────────┐ │
│ │ Cognito     │ │                          │ │ Cognito     │ │
│ │ User Pool   │ │                          │ │ User Pool   │ │
│ │ (Source)    │ │                          │ │ (Target)    │ │
│ └─────────────┘ │                          │ └─────────────┘ │
│                 │                          │        │        │
│ ┌─────────────┐ │                          │        ▼        │
│ │ Cross-      │ │                          │ ┌─────────────┐ │
│ │ Account     │ │                          │ │ Migration   │ │
│ │ IAM Role    │ │                          │ │ Lambda      │ │
│ └─────────────┘ │                          │ │ Function    │ │
└─────────────────┘                          │ └─────────────┘ │
                                             └─────────────────┘
```

## 🚀 Getting Started with Kiro.dev

This project is designed to work with [Kiro.dev](https://kiro.dev), an AI-powered development environment that uses spec-driven development.

### Prerequisites
- [Kiro.dev](https://kiro.dev) installed
- AWS CLI configured with appropriate permissions
- Node.js 18+ or Python 3.11+
- Git

### Opening in Kiro

1. **Clone the repository**:
   ```bash
   git clone https://github.com/quangchuamz/cognito-migration-poc.git
   cd cognito-migration-poc
   ```

2. **Open with Kiro**:
   ```bash
   kiro .
   ```

3. **Kiro will automatically**:
   - Load the project specifications from `.kiro/specs/`
   - Apply steering files from `.kiro/steering/`
   - Configure MCP servers from `.kiro/settings/mcp.json`

### Kiro.dev Spec-Driven Development

This project follows Kiro.dev's spec-driven methodology:

#### 📋 **Specifications** (`.kiro/specs/cognito-migration/`)
- **`requirements.md`**: Requirements using EARS notation
- **`design.md`**: Technical architecture and design
- **`tasks.md`**: Implementation tasks organized by phases

#### 🎯 **Steering Files** (`.kiro/steering/`)
- **`aws-cognito-migration.md`**: AWS development guidelines
- **`cross-account-security.md`**: Security best practices

#### 🔧 **MCP Configuration** (`.kiro/settings/mcp.json`)
- AWS Documentation server for real-time AWS docs access
- GitHub server for code examples and repository management

### Working with Kiro

1. **Start a Spec Session**:
   - Click the "Spec" button in Kiro chat
   - Or navigate to the Specs section in the Kiro panel

2. **Execute Tasks**:
   - Open `.kiro/specs/cognito-migration/tasks.md`
   - Click on individual tasks to execute them
   - Track progress as tasks move from "Todo" to "Done"

3. **Use MCP Tools**:
   - `#aws-docs search Cognito user migration` - Search AWS documentation
   - `#github search code Lambda migration` - Find code examples

## 📁 Project Structure

```
cognito-migration-poc/
├── .kiro/
│   ├── specs/
│   │   └── cognito-migration/
│   │       ├── requirements.md    # EARS notation requirements
│   │       ├── design.md          # Technical architecture
│   │       └── tasks.md           # Implementation tasks
│   ├── steering/
│   │   ├── aws-cognito-migration.md    # AWS guidelines
│   │   └── cross-account-security.md   # Security practices
│   └── settings/
│       └── mcp.json               # MCP server configuration
├── src/                           # Source code (to be implemented)
├── infrastructure/                # CloudFormation/CDK templates
├── tests/                         # Test files
└── docs/                          # Additional documentation
```

## 🛠️ Implementation Phases

### Phase 1: Infrastructure Setup (1 week)
- Create cross-account IAM roles
- Setup target user pool
- Create Lambda function skeleton
- Configure development environment

### Phase 2: Migration Logic (2 weeks)
- Implement authentication logic
- User creation and attribute mapping
- Error handling and security measures

### Phase 3: Testing & Validation (1.5 weeks)
- Unit and integration testing
- Security testing
- Performance optimization

### Phase 4: Monitoring & Documentation (1 week)
- CloudWatch dashboards and alarms
- Comprehensive documentation
- Deployment procedures

### Phase 5: Deployment (0.5 weeks)
- Staging and production deployment
- Post-deployment validation

## 🔒 Security Considerations

- **Password Security**: Passwords are never logged or exposed
- **Cross-Account Access**: Uses temporary credentials with least privilege
- **Data Encryption**: All communications use TLS 1.2+
- **Audit Trail**: Complete CloudWatch logging for all operations

## 📊 Success Criteria

- ✅ Migration latency < 3 seconds per user
- ✅ 99.9% migration success rate
- ✅ Zero password exposure in logs
- ✅ Complete audit trail for all operations
- ✅ Scalable to handle concurrent migrations

## 🤝 Contributing

This project uses Kiro.dev's spec-driven development approach:

1. **Requirements**: Use EARS notation for new requirements
2. **Design**: Update technical design documents
3. **Tasks**: Break down work into discrete, executable tasks
4. **Implementation**: Use Kiro's AI assistance for coding
5. **Testing**: Comprehensive testing at each phase

## 📚 Resources

### AWS Documentation
- [User Migration Lambda Trigger](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-pools-import-using-lambda.html)
- [Cross-Account IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_cross-account-with-roles.html)

### Kiro.dev Resources
- [Spec-Driven Development](https://kiro.dev/docs/specs/concepts)
- [EARS Notation](https://kiro.dev/docs/specs/concepts)
- [MCP Servers](https://kiro.dev/docs/mcp/servers)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🏷️ Tags

`aws` `cognito` `migration` `lambda` `cross-account` `kiro-dev` `spec-driven` `poc`