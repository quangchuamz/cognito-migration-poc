# Cognito Cross-Account Migration Design

## Architecture Overview

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
│ ┌─────────────┐ │                          │        │        │
│ │ Cross-      │ │                          │        ▼        │
│ │ Account     │ │                          │ ┌─────────────┐ │
│ │ IAM Role    │ │                          │ │ Migration   │ │
│ └─────────────┘ │                          │ │ Lambda      │ │
└─────────────────┘                          │ │ Function    │ │
                                             │ └─────────────┘ │
                                             └─────────────────┘
```

## Component Design

### 1. Migration Lambda Function (Account B)
- **Runtime**: Node.js 18.x or Python 3.11
- **Trigger**: Cognito User Migration trigger
- **Purpose**: Authenticate users against Account A and create users in Account B
- **Key Functions**:
  - Cross-account authentication
  - User attribute extraction and mapping
  - Error handling and logging
  - Security compliance

### 2. Cross-Account IAM Role (Account A)
- **Purpose**: Allow Account B Lambda to access Account A Cognito
- **Permissions**:
  - `cognito-idp:AdminInitiateAuth`
  - `cognito-idp:AdminGetUser`
  - `cognito-idp:ListUsers`
- **Trust Policy**: Account B Lambda execution role

### 3. Target User Pool Configuration (Account B)
- **Migration Trigger**: Configured to invoke Lambda function
- **Authentication Flow**: `USER_PASSWORD_AUTH` enabled during migration
- **Post-Migration**: Switch to `USER_SRP_AUTH` for security

### 4. Monitoring and Logging
- **CloudWatch Logs**: Detailed migration event logging
- **CloudWatch Metrics**: Success/failure rates, latency
- **Alarms**: Failed migration attempts, error rates

## Security Design

### Authentication Flow Security
1. **TLS Encryption**: All communications use TLS 1.2+
2. **IAM Role Assumption**: Temporary credentials for cross-account access
3. **Password Handling**: Never log or expose passwords in plain text
4. **Network Security**: VPC endpoints for internal communication

### Data Protection
- **In-Transit**: TLS encryption for all API calls
- **At-Rest**: Cognito native encryption
- **Access Control**: Least privilege IAM policies
- **Audit Trail**: Complete CloudWatch logging

## Migration Flow

### Step-by-Step Process
1. User attempts sign-in to Account B user pool
2. User doesn't exist → Cognito triggers Lambda function
3. Lambda receives username/password from Cognito
4. Lambda assumes cross-account role in Account A
5. Lambda authenticates user against Account A user pool
6. If successful, Lambda extracts user attributes
7. Lambda creates user in Account B with same password
8. Lambda sets finalUserStatus to CONFIRMED
9. Cognito completes authentication and returns tokens
10. Future logins go directly to Account B

### Error Handling Flow
1. Authentication fails against Account A
2. Lambda logs error details (without password)
3. Lambda returns error to Cognito
4. Cognito returns authentication failure to client
5. No user created in Account B

## Performance Considerations

### Latency Optimization
- Connection pooling for AWS SDK clients
- Caching of IAM role credentials
- Optimized Lambda memory allocation
- Regional proximity for cross-account calls

### Scalability
- Lambda concurrent execution limits
- Cognito API rate limits
- Cross-account API throttling
- Auto-scaling considerations

## Monitoring Strategy

### Key Metrics
- Migration success rate
- Migration latency (p50, p95, p99)
- Error rates by type
- Cross-account authentication latency

### Alerting
- Failed migration rate > 1%
- Migration latency > 5 seconds
- Lambda function errors
- Cross-account authentication failures

### Dashboards
- Real-time migration status
- Historical success rates
- Performance trends
- Error analysis