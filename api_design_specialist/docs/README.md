# API Design Specialist - Documentation

## Overview

This directory contains resources and documentation for the API Design Specialist consultant role. The API Design Specialist provides expert guidance on designing, implementing, and maintaining REST and GraphQL APIs according to industry best practices and organizational standards.

## Directory Structure

```
api_design_specialist/
├── IDENTITY.md                 # Role definition and responsibilities
├── docs/
│   ├── README.md              # This file
│   ├── rest-api-patterns.md   # REST API design patterns and examples
│   ├── graphql-patterns.md    # GraphQL schema design patterns
│   ├── authentication.md      # Authentication and authorization guides
│   ├── versioning.md          # API versioning strategies
│   ├── testing.md             # API testing approaches
│   └── examples/              # Code examples and templates
│       ├── rest/              # REST API examples
│       ├── graphql/           # GraphQL examples
│       └── openapi/           # OpenAPI specifications
└── templates/                  # Reusable templates
    ├── openapi-template.yaml   # OpenAPI spec template
    ├── graphql-schema.graphql  # GraphQL schema template
    └── api-design-doc.md       # API design document template
```

## Core Competencies

### 1. REST API Design
The API Design Specialist helps with:
- Resource modeling and URL structure design
- HTTP method and status code selection
- Request/response format design
- Pagination, filtering, and sorting implementation
- HATEOAS and hypermedia design
- JSON:API compliance

**Key Documents:**
- API Design Standards SOP (ENG-SOP-008) - Section 3
- REST API Design Patterns Guide
- HTTP Status Code Reference

### 2. GraphQL API Design
Expertise in:
- Schema design and type system
- Query and mutation design
- Pagination with connections
- Custom scalars and directives
- Performance optimization (DataLoader, batching)
- Schema evolution and deprecation

**Key Documents:**
- API Design Standards SOP (ENG-SOP-008) - Section 4
- GraphQL Schema Design Guide
- GraphQL Performance Optimization

### 3. API Security
Implements:
- OAuth 2.0 and OpenID Connect
- JWT authentication
- API key management
- Role-based and attribute-based access control
- Rate limiting strategies
- OWASP API Security Top 10 compliance

**Key Documents:**
- API Design Standards SOP (ENG-SOP-008) - Section 6
- Authentication Implementation Guide
- API Security Checklist

### 4. API Versioning
Strategies for:
- URL path versioning
- Header-based versioning
- GraphQL schema evolution
- Deprecation processes
- Migration planning
- Backward compatibility

**Key Documents:**
- API Design Standards SOP (ENG-SOP-008) - Section 5
- Versioning Strategy Guide
- Deprecation Policy

### 5. API Documentation
Creates:
- OpenAPI/Swagger specifications
- GraphQL schema documentation
- Getting started guides
- Code examples and tutorials
- Migration guides
- Interactive API documentation

**Key Documents:**
- API Design Standards SOP (ENG-SOP-008) - Section 9
- OpenAPI Documentation Guide
- Documentation Best Practices

### 6. API Testing
Develops:
- Contract tests
- Integration tests
- Performance tests
- Security tests
- End-to-end tests
- OpenAPI validation

**Key Documents:**
- API Design Standards SOP (ENG-SOP-008) - Section 10
- API Testing Strategy Guide
- Test Automation Patterns

## Common Use Cases

### Scenario 1: Designing a New REST API
**Situation:** Need to create a new REST API for a microservice

**Approach:**
1. Identify resources and business entities
2. Design URL structure and endpoints
3. Define request/response formats
4. Choose authentication method
5. Implement error handling
6. Create OpenAPI specification
7. Design testing strategy

**Deliverables:**
- API design document
- OpenAPI specification
- Implementation guide
- Test cases

### Scenario 2: Creating a GraphQL Schema
**Situation:** Building a GraphQL API for a mobile application

**Approach:**
1. Model domain types and relationships
2. Design queries for data fetching
3. Design mutations for data modification
4. Implement pagination with connections
5. Add custom scalars and directives
6. Optimize with DataLoader
7. Document schema

**Deliverables:**
- GraphQL schema definition
- Resolver implementation guide
- Query examples
- Performance optimization plan

### Scenario 3: Implementing API Authentication
**Situation:** Need to add OAuth 2.0 to existing API

**Approach:**
1. Choose appropriate OAuth flow
2. Design token structure and claims
3. Implement token validation
4. Add authorization checks
5. Configure rate limiting
6. Update API documentation
7. Create migration guide

**Deliverables:**
- Authentication flow diagram
- Implementation code
- Updated OpenAPI spec
- Developer guide

### Scenario 4: Versioning an Existing API
**Situation:** Need to make breaking changes to production API

**Approach:**
1. Assess impact of changes
2. Choose versioning strategy
3. Design new version
4. Create migration path
5. Implement deprecation warnings
6. Update documentation
7. Plan sunset timeline

**Deliverables:**
- Version comparison document
- Migration guide
- Deprecation timeline
- Communication plan

### Scenario 5: Improving API Performance
**Situation:** API response times are too slow

**Approach:**
1. Profile current performance
2. Identify bottlenecks
3. Implement pagination
4. Add caching headers
5. Optimize database queries
6. Add field selection
7. Monitor improvements

**Deliverables:**
- Performance analysis
- Optimization recommendations
- Implementation code
- Monitoring dashboard

## Quick Reference Guides

### REST API Checklist
- [ ] Resources use plural nouns
- [ ] URLs are lowercase with hyphens
- [ ] HTTP methods used correctly
- [ ] Appropriate status codes returned
- [ ] Pagination implemented
- [ ] Filtering and sorting supported
- [ ] Authentication required
- [ ] Authorization checked
- [ ] Rate limiting configured
- [ ] Error responses standardized
- [ ] Versioning strategy defined
- [ ] OpenAPI spec created
- [ ] Documentation published
- [ ] Tests implemented

### GraphQL Schema Checklist
- [ ] Types follow naming conventions
- [ ] Fields are properly documented
- [ ] Nullability carefully considered
- [ ] Pagination uses connections
- [ ] Mutations return payloads
- [ ] Errors handled gracefully
- [ ] Custom scalars defined
- [ ] Directives documented
- [ ] Schema evolution planned
- [ ] DataLoader implemented
- [ ] Query complexity limited
- [ ] Tests cover all resolvers

### API Security Checklist
- [ ] HTTPS enforced
- [ ] Authentication required
- [ ] Authorization implemented
- [ ] Input validation in place
- [ ] Output encoding applied
- [ ] SQL injection prevented
- [ ] XSS prevention implemented
- [ ] CSRF protection added
- [ ] Rate limiting configured
- [ ] Security headers set
- [ ] Secrets not exposed
- [ ] Audit logging enabled

## Best Practices Summary

### REST API Best Practices
1. **Design for the consumer first** - Make APIs intuitive and easy to use
2. **Use standard HTTP methods** - GET, POST, PUT, PATCH, DELETE appropriately
3. **Return proper status codes** - 2xx for success, 4xx for client errors, 5xx for server errors
4. **Implement pagination** - Never return unbounded result sets
5. **Support filtering and sorting** - Use query parameters
6. **Version your API** - Plan for change from the start
7. **Document everything** - Use OpenAPI specification
8. **Handle errors gracefully** - Provide clear, actionable error messages
9. **Implement rate limiting** - Protect your API from abuse
10. **Monitor and measure** - Track performance and usage

### GraphQL Best Practices
1. **Design schema around domain** - Model business entities and relationships
2. **Use descriptive names** - Make schema self-documenting
3. **Document all types and fields** - Use description strings
4. **Implement connections for lists** - Standard pagination pattern
5. **Use non-null judiciously** - Consider backward compatibility
6. **Deprecate, don't remove** - Mark old fields as deprecated
7. **Optimize with DataLoader** - Prevent N+1 query problems
8. **Limit query complexity** - Prevent expensive queries
9. **Return detailed errors** - Use error extensions
10. **Version through evolution** - Add fields, deprecate old ones

### Security Best Practices
1. **Authenticate everything** - No unauthenticated endpoints
2. **Apply least privilege** - Grant minimum necessary permissions
3. **Validate all inputs** - Never trust client data
4. **Sanitize outputs** - Prevent injection attacks
5. **Use HTTPS only** - Encrypt all traffic
6. **Implement rate limiting** - Prevent abuse and DoS
7. **Log security events** - Enable audit trails
8. **Keep dependencies updated** - Patch vulnerabilities
9. **Don't expose sensitive data** - Be careful with error messages
10. **Test security regularly** - Automated and manual testing

## Common Patterns and Solutions

### Pagination Patterns

**Offset-based (Simple):**
```
GET /v1/users?page=2&per_page=20
```

**Cursor-based (Scalable):**
```
GET /v1/users?cursor=eyJpZCI6MTIzfQ&limit=20
```

**GraphQL Connection:**
```graphql
query {
  users(first: 20, after: "cursor") {
    edges {
      node { id, name }
      cursor
    }
    pageInfo {
      hasNextPage
      endCursor
    }
  }
}
```

### Error Handling Pattern
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Request validation failed",
    "details": [
      {
        "field": "email",
        "message": "Invalid email format",
        "code": "INVALID_FORMAT"
      }
    ],
    "request_id": "req_abc123"
  }
}
```

### Authentication Pattern (JWT)
```http
Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...

Token Payload:
{
  "sub": "user123",
  "iss": "https://api.example.com",
  "aud": "https://api.example.com",
  "exp": 1742294400,
  "scope": "read:users write:users"
}
```

### Rate Limiting Pattern
```http
Response Headers:
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 987
X-RateLimit-Reset: 1742294400

Error Response (429):
{
  "error": {
    "code": "RATE_LIMIT_EXCEEDED",
    "message": "Rate limit exceeded",
    "retry_after": 60
  }
}
```

## Tools and Resources

### API Development Tools
- **OpenAPI Tools:** Swagger Editor, Stoplight Studio, OpenAPI Generator
- **GraphQL Tools:** Apollo Studio, GraphQL Playground, Altair
- **Testing Tools:** Postman, Insomnia, Newman, k6
- **Documentation:** Swagger UI, ReDoc, Docusaurus, GraphQL Voyager

### Code Generators
- **OpenAPI Generator:** Client and server code generation
- **GraphQL Code Generator:** TypeScript types and resolvers
- **Swagger Codegen:** API client libraries
- **Apollo Codegen:** GraphQL client code

### Validation Tools
- **Spectral:** OpenAPI linting
- **OpenAPI Validator:** Spec validation
- **GraphQL Inspector:** Schema validation and comparison
- **ESLint plugins:** API code linting

### Monitoring and Analytics
- **Prometheus + Grafana:** Metrics and dashboards
- **Datadog:** APM and monitoring
- **New Relic:** Performance monitoring
- **Custom analytics:** API usage tracking

## Learning Resources

### Official Specifications
- [OpenAPI Specification 3.1](https://spec.openapis.org/oas/v3.1.0)
- [GraphQL Specification](https://spec.graphql.org/)
- [JSON:API Specification](https://jsonapi.org/)
- [OAuth 2.0 (RFC 6749)](https://tools.ietf.org/html/rfc6749)
- [JWT (RFC 7519)](https://tools.ietf.org/html/rfc7519)

### API Design Guides
- [Microsoft REST API Guidelines](https://github.com/microsoft/api-guidelines)
- [Google API Design Guide](https://cloud.google.com/apis/design)
- [Stripe API Design](https://stripe.com/docs/api)
- [GitHub API](https://docs.github.com/en/rest)
- [GraphQL Best Practices](https://graphql.org/learn/best-practices/)

### Books
- "RESTful Web APIs" by Leonard Richardson
- "Designing Web APIs" by Brenda Jin, Saurabh Sahni, Amir Shevat
- "GraphQL in Action" by Samer Buna
- "API Security in Action" by Neil Madden

### Online Courses
- RESTful API Design courses on Udemy, Pluralsight
- GraphQL tutorials on Apollo documentation
- API security courses on OWASP
- Cloud provider API training (AWS, Azure, GCP)

## Getting Help

### When to Engage the API Design Specialist

**Design Phase:**
- Creating new API designs
- Reviewing API proposals
- Establishing API standards
- Making architectural decisions

**Implementation Phase:**
- Implementing authentication/authorization
- Creating OpenAPI specifications
- Writing GraphQL schemas
- Developing test strategies

**Maintenance Phase:**
- Versioning existing APIs
- Deprecating old features
- Improving performance
- Enhancing security

**Documentation Phase:**
- Writing API documentation
- Creating migration guides
- Developing tutorials
- Building interactive docs

### How to Request Support

1. **Provide Context:**
   - What are you trying to achieve?
   - What constraints do you have?
   - Who are the API consumers?

2. **Share Relevant Information:**
   - Current API design or code
   - Requirements and use cases
   - Performance or security concerns
   - Timeline and priorities

3. **Be Specific:**
   - What specific guidance do you need?
   - What have you already tried?
   - What are the open questions?

## Contributing

To improve this documentation:
1. Review existing content for accuracy
2. Add new patterns and examples
3. Update references to latest standards
4. Share lessons learned from implementations
5. Contribute code examples and templates

---

**Last Updated:** 2026-03-14
**Maintained By:** API Design Specialist
**Version:** 1.0
