# Plugin Integration Microservice Platform

## Purpose
This microservice platform enables businesses to seamlessly integrate and manage plugins. It serves as a marketplace between platforms accepting plugins and developers building them.

## Key Features

1. **Plugin Management**: 
   - Manage a list of plugins per business, track their status (Test, Published, Unapproved).
   
2. **Access Control**: 
   - Integrate with SSO for OAuth-based access management, allowing each plugin to receive appropriate tokens for user data access and task execution.
   
3. **Plugin Installation & Activation**: 
   - Handle plugin installation and activation based on user requests, ensuring smooth deployment into user environments.

4. **Request Handling**:
   - Send requests to installed plugins and process responses, ensuring effective communication between the platform and plugins.

5. **Feedback & Ratings**: 
   - Allow users to comment, rate, and review plugins, enhancing the evaluation process.

## Architecture

The platform is built using a microservices architecture with distinct services for core functions:

- **Core Service**: Handles the main business logic of managing plugins, users, and businesses.
- **Policy Service**: Manages access scopes and communicates with the SSO service to control what each plugin can access.
- **SSO Integration**: Centralizes user authentication and authorization, allowing plugins to use OAuth for secure access.

## Challenge Resolved
The management of access scopes, initially a point of uncertainty, is handled by the SSO service. This ensures scalability and flexibility when adjusting access levels. A dedicated microservice was introduced to bridge the plugin and platform, ensuring each component communicates seamlessly.

## Getting Started

To set up the project:
1. Clone the repository.
2. Set up environment variables for SSO and OAuth integration.
3. Deploy each service as independent containers using Docker.
4. Connect the services via API gateways for secure communication.

### Installation

```bash
git clone <repository-url>
cd project-directory
docker-compose up
```

## Contribution

We welcome contributions! To get started, check out our issues list or submit a pull request.

## License

This project is licensed under the MIT License.
