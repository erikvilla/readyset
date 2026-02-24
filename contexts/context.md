Coppel | SSO to on-prem
	Actors
		Auth0
			Main dashboard for authenticated users
		Cerby
			Web extension
				Responsible for
					receiving SSO login events to disconnected systems
					Fetching automation workflows
					Running web automations
		Coppel 
			Customer
				Wants to run SSO flows triggered from Auth0 to on-prem disconnected systems in stores
					Coppel has a disconnected on-prem windows application they use in stores. In ~4k stores ~50k users access such application using usernames and passwords. They want to enable SSO-like experience via Cerby. Users would go to Auth0, click a tile (which points to Cerby) to login to the on-prem app and the ideal experience is that Cerby can initiate the access account workflow against the on-prem app
	Current state
		Coppel
			The aproximately 50,000 users have their own username and password for accessing physical store systems
				No policies or secure vaulting mechanisms are in place to protect these accounts
				Password rotations rely on manual human effort
				Disconnected applications are not part of the existing IAM and Security Governance frameworks
		Cerby
			Cerby allows SSO-like experience to web-based disconnected systems only
			On-prem automation capabilities supported are related to a single node configured per system to run joiner, mover, leaver and data reconciliation routines
				The current ask here is to setup a node per machine, not per system to allow users authetnitcate SSO-like to on-prem systems
	Future state
		User accounts are securely stored
		Automatic Password rotation policies execute periodically
		Users do not need to know their username and password, access is automated and granted by a trusted source (Cerby)
			End user experience to login to disconnected on-prem applications is SSO-like for disconnected systems without SAML support
	Phased proposal
		Phase 1
			EPM (Enterprise Password Manager) + Password rotation policies
				Cerby onboards the 50,000 user accounts to the Enterprise Password Manager product
				Cerby adds password rotation support for the target disconnected system
				Establish periodic password rotation policies
				Cerby and Coppel collaborate to configure an on-prem orchestrator capable of receiving desktop automation requests to run password rotations automatically
			Value
				User credentials are securely stored and passwords get periodically rotated to reduce attack windows (AI rephrase this)
		Phase 2
			SSO to on-prem capabilities
				Cerby develops capabilties for secure local client communication from the web extension to the Cerby Windows service running in the host machine
				Cerby develops capabilities for local desktop automation orchestration extending the web extension capabilities 
			Value
				Transparent SSO-like experience for end users accessing on-prem systems
				Users don't need to know their credentials for accessing disconnected (Non-SAML compliant) systems
	Cerby definitions
		# Cerby Platform Descriptions
			## Level 1: General Audience (Non-Technical)
				Cerby is a digital security platform that helps businesses manage access to all their online accounts and services in one place. Think of it as a master key system for your company's digital tools.
				**What can Cerby do?**
					- **Centralized Account Management**: Instead of employees managing passwords for dozens of different apps (like Salesforce, GitHub, Facebook Business Manager, etc.), Cerby stores and manages all these accounts securely in one place.
					- **Automated Access Control**: When someone joins your company, Cerby can automatically give them access to all the accounts they need. When they leave, it automatically removes their access—no manual work required.
					- **Secure Password Storage**: Cerby keeps all your company's passwords and secrets in an encrypted digital vault, so employees don't need to remember or write down passwords.
					- **Multi-Factor Authentication (MFA) Support**: Cerby can handle the security codes and verification steps that many apps require, making it easier for employees to access their accounts securely.
					- **Works with Hundreds of Apps**: Whether your company uses popular tools like Slack and Microsoft 365, specialized platforms like SAP, or custom internal systems, Cerby can connect to and manage access to them.
					**In simple terms**: Cerby is like having a smart assistant that remembers all your passwords, gives new employees access to everything they need automatically, and makes sure former employees can't access company accounts anymore—all while keeping everything secure.
			## Level 2: Business/Product Level
				**What is Cerby?**
					Cerby is an Identity and Access Management (IAM) platform designed to solve the challenge of managing user access across hundreds of heterogeneous business systems. It provides automated provisioning, deprovisioning, and ongoing access management for enterprise applications, SaaS platforms, and legacy systems.
				**What can Cerby do?**
					1. **Unified Account Management**
						   - Centralized repository for all organizational accounts across different platforms
						   - Support for social media business hubs (Facebook Business Manager, LinkedIn Campaign Manager)
						   - Integration with SaaS products (Salesforce, HubSpot, GitHub, Slack)
						   - Enterprise application support (SAP, Oracle, Microsoft 365)
						   - Legacy system integration through RPA (Robotic Process Automation)
					2. **Automated Lifecycle Management**
						   - **Provisioning**: Automatically grant access to new users across all required systems
						   - **Access Updates**: Modify permissions and roles as employees change positions
						   - **Deprovisioning**: Automatically revoke access when users leave
						   - **SCIM Protocol Support**: Standardized user provisioning via SCIM v2
					3. **Robotic Process Automation (RPA)**
						   - Handles systems without APIs by automating browser interactions
						   - Manages complex authentication flows including MFA challenges
						   - Supports various MFA types: TOTP, SMS, push notifications, email verification
						   - Handles identity verification challenges (email swaps, phone verification)
					4. **Security & Compliance**
						   - Secure vault for storing credentials and secrets
						   - Role-Based Access Control (RBAC) for fine-grained permissions
						   - Audit trails and activity logging
						   - Session management and secure device onboarding
						   - Support for secure sharing of credentials with proper access controls
					5. **Data Reconciliation**
						   - Synchronizes user data across heterogeneous systems
						   - Handles different data schemas and field mappings
						   - Maintains consistency across platforms with varying data models
					6. **Collections & Organization**
						   - Organize accounts into collections for better management
						   - Support for hierarchical collections (parent/child relationships)
						   - Team-based access management
						   - Workspace governance and policy enforcement
				**Business Value:**
					- Reduces IT overhead for access management
					- Improves security posture through automated deprovisioning
					- Ensures compliance with access policies
					- Scales to support hundreds of integrated systems
					- Reduces time-to-productivity for new employees
			## Level 3: Technical/Developer Level
				**What is Cerby?**
					Cerby is a comprehensive Identity and Access Management (IAM) platform built on domain-driven design principles, providing abstractions for managing accounts, users, tenants, and access across heterogeneous external systems. The platform uses a combination of API integrations and Robotic Process Automation (RPA) to handle identity lifecycle management at scale.
				**What can Cerby do?**
					1. **Multi-Tenant Workspace Model**
						   - Workspace-based isolation with multi-tenancy support
						   - SCIM token management for external identity providers
						   - API token generation and management
						   - Workspace governance with assignment rules and policies
					2. **Account Abstraction Layer**
						   - Unified account model supporting multiple providers (Google, Microsoft, custom OAuth, SAML)
						   - Provider-agnostic account management with provider-specific adapters
						   - Account relations and tenant relationships
						   - Account capabilities and feature flag management
					3. **Automation Job System**
						   - Asynchronous job execution using Celery workers
						   - Workflow-based automation supporting multiple execution platforms
						   - Job triggers with execution groups for audit and tracking
						   - Support for various automation types:
						     - `PROVIDE_ACCESS` / `SHARE`: Grant access to accounts
						     - `REVOKE_ACCESS`: Remove access from accounts
						     - `UPDATE_ACCESS`: Modify existing access
						     - `SETUP_MFA`: Configure multi-factor authentication
						     - `EMAIL_SWAP_IN`, `PHONE_SWAP_IN`: Handle identity verification
					4. **RPA Bot Session Management**
						   - Bot session lifecycle (start, stop, retry, next task)
						   - Task queue management for browser automation
						   - Screenshot capture for error debugging
						   - Notification handling for automation events
					5. **Authentication & Authorization**
						   - OIDC authentication flow with PKCE support
						   - Session management with JWT tokens
						   - Role-Based Access Control (RBAC) with granular permissions
						   - API key authentication for public/external APIs with scope-based access
					6. **Data Models & Abstractions**
						   - **Accounts**: Provider-agnostic representation of external system accounts
						   - **Users**: Identity management with support for guests and external identities
						   - **Teams**: Group-based access management
						   - **Collections**: Hierarchical organization of accounts and secrets
						   - **Secure Secrets**: Encrypted storage for credentials and sensitive data
						   - **Vaults**: Container for organizing secrets
						   - **Tenants**: Integration/tenant relationships for external systems
					7. **Integration Patterns**
						   - REST API endpoints (128 internal, 9 public, 2 external)
						   - SCIM v2 protocol implementation (Users, Groups, Schemas, ResourceTypes)
						   - Webhook support (Twilio, PhoneBlur)
						   - Public API with API key authentication
						   - External API for tenant management operations
					8. **Message Bus Architecture**
						   - Event-driven architecture using message bus
						   - Async event processing for domain events
						   - Decoupled service communication
					9. **Database & Persistence**
						   - MySQL for primary data storage
						   - Redis for caching and session management
						   - DynamoDB for certain domain entities
						   - Alembic for database migrations
					10. **Security Features**
						    - Secure device onboarding with activation codes
						    - MFA device management (TOTP, SMS, push)
						    - OTP code generation and validation
						    - Secure secret sharing with expiration
						    - Encryption utilities for sensitive data
					**Technical Stack:**
						- Backend: Python 3.11, Flask, Flask-RESTful
						- Task Queue: Celery with Redis broker
						- Database: MySQL, Redis, DynamoDB
						- Infrastructure: Docker, Nginx, LocalStack (for local dev)
						- Stream Processing: Apache Flink (Java)