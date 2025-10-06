# Secure Coding Guidelines
This md file outlines secure coding practices across nine critical areas: Input Validation &
  Sanitization, Authentication &Authorization, Data Protection, Error Handling & Logging, Database  Security, API Security, Working with AI Assistants securely, Code Quality
  & Dependencies, Infrastructure Security, and Development Practices.

## Input Validation & Sanitization
- Identify all data sources and classify them into trusted and untrusted
- Validate all data from untrusted sources (databases, file streams, etc)
- Use a centralized input validation routine for the whole application
- Encode input to a common character set before validating
- Validate all input at application boundaries (user input, APIs, file uploads)
- Use allow-lists rather than deny-lists for input validation
- Sanitize data based on context (HTML encoding for web, SQL parameterization for databases)
- Implement proper length limits and data type validation
- Never trust client-side validation alone
- All validation failures should result in input rejection

## Authentication & Authorization
- Require authentication for all pages and resources, except those specifically intended to be public
- All authentication controls must be enforced on a trusted system
- Establish and utilize standard, tested, authentication services whenever possible
- Use a centralized implementation for all authentication controls, including libraries that call external authentication services
- Implement multi-factor authentication for sensitive operations
- Use strong password policies and secure password storage (bcrypt, Argon2)
- Implement proper session management with secure session tokens
- Follow principle of least privilege for access control
- Validate authorization on every request, not just at login
- If your application manages a credential store, use cryptographically strong one-way salted hashes
- Password entry should be obscured on the user's screen
- If using third party code for authentication, inspect the code carefully to ensure it is not affected by any malicious code

## Data Protection
- Encrypt sensitive data at rest and in transit (TLS 1.2+)
- Never store passwords in plain text or reversible encryption
- Use environment variables or secure vaults for secrets management
- Implement proper key rotation and management
- Sanitize logs to prevent sensitive data exposure
- Implement least privilege, restrict users to only the functionality, data and system information that is required to perform their tasks
- Do not store passwords, connection strings or other sensitive information in clear text or in any non-cryptographically secure manner on the client side
- Remove comments in user accessible production code that may reveal backend system or other sensitive information
- Do not include sensitive information in HTTP GET request parameters
- Disable client side caching on pages containing sensitive information

## Error Handling & Logging
- Implement centralized error handling
- Log security events (failed logins, privilege escalations, data access)
- Never expose internal system details in error messages
- Implement proper audit trails for sensitive operations
- Monitor and alert on suspicious patterns
- Implement generic error messages and use custom error pages
- All logging controls should be implemented on a trusted system
- Logging controls should support both success and failure of specified security events
- Do not store sensitive information in logs, including unnecessary system details, session identifiers or passwords
- Use a cryptographic hash function to validate log entry integrity
 
## Database Security
- Use parameterized queries to prevent SQL injection
- Implement database connection pooling and proper connection management
- Apply principle of least privilege to database accounts
- Encrypt database connections and sensitive columns
- Regular database security updates and patches
- Close the connection as soon as possible
- Remove or change all default database administrative passwords
- Disable any default accounts that are not required to support business requirements
- The application should connect to the database with different credentials for every trust distinction (for example user, read-only user, guest, administrators)


## API Security
- Implement rate limiting and throttling
- Use proper HTTP security headers (HSTS, CSP, X-Frame-Options)
- Validate content types and enforce proper CORS policies
- Implement API versioning and deprecation strategies
- Use OAuth 2.0 or similar standards for API authentication

## Working with AI Assistants securely
- Never include sensitive data, passwords, apikey in prompts, azure blob urls, DB credentials etc to AI agents for producing code
- Validate code produced by AI agents by running through SAST or DAST
- Ask AI to review and improve it's work and review this.
- Generate AI to generate an SBOM so you are aware of all your dependencies
- Sanitize code snippets before sharing - remove proprietary business logic and algorithms
- Do not rely solely on AI for security-critical code - always conduct manual security reviews
- Treat AI assistants as untrusted sources - apply the same scrutiny as third-party code
- Implement proper access controls when AI tools are integrated into development workflows
- Log and monitor AI assistant usage in development environments for compliance
- Educate development teams on secure practices when working with AI coding assistants
- Verify AI-generated security implementations against established security libraries
- Establish clear policies for AI tool usage in enterprise development environments
- Review AI-generated database queries for potential injection vulnerabilities
- Test AI-generated authentication and authorization code thoroughly before deployment

## Code Quality & Dependencies
- Keep dependencies updated and scan for known vulnerabilities
- Implement secure code review processes
- If on github do not allow merge to main with a pull request review
- Use static analysis security testing (SAST) tools
- Follow secure coding standards for your language/framework
- Implement proper exception handling without information leakage

## Infrastructure Security
- Use HTTPS everywhere with proper certificate validation
- Implement proper firewall rules and network segmentation
- Regular security patching of operating systems and services
- Use containerization with minimal base images
- Implement proper backup and disaster recovery procedures

## Development Practices
- Conduct threat modeling for new features and systems
- Never commit secrets, keys, or credentials to version control
- Use separate environments for development, testing, and production
- Implement security testing in CI/CD pipelines such SAST, SCA, DAST
- Regular security training for development team
