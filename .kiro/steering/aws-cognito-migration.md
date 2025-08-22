---
inclusion: always
---

# AWS Cognito Migration Development Guidelines

## Security First Approach
- Never log passwords or sensitive user data
- Use least privilege IAM policies
- Implement comprehensive error handling
- Validate all inputs and outputs

## AWS SDK Best Practices
- Use AWS SDK v3 for Node.js or Boto3 for Python
- Implement proper retry logic with exponential backoff
- Use connection pooling for performance
- Handle AWS service limits and throttling

## Lambda Function Standards
- Use environment variables for configuration
- Implement structured logging with correlation IDs
- Set appropriate timeout and memory settings
- Use Lambda layers for shared dependencies

## Testing Requirements
- Unit tests for all business logic
- Integration tests for AWS service interactions
- Security tests for authentication flows
- Performance tests for migration latency

## Monitoring Standards
- CloudWatch metrics for all operations
- Detailed logging for debugging
- Alarms for critical failures
- Dashboard for operational visibility

## Code Organization
- Separate authentication logic from user creation
- Use dependency injection for AWS clients
- Implement proper error handling hierarchies
- Follow single responsibility principle

## Documentation Standards
- Document all environment variables
- Include deployment instructions
- Provide troubleshooting guides
- Maintain API documentation