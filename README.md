# ufaas-docs
In this file you can find the documentation principales in UFaaS, Product and indevidual service document structure.

## 1. Documentation Structure and Storage
   We use GitHub for storing and managing our documentation.

   ### 1.1. Repository Organization
   - Main Documentation Repo: We have a separate GitHub repository solely for documentation. This keeps it distinct from our codebase and allows for easier management and contributions.
     https://github.com/ufaasio/ufaas-docs
   - Individual Service Repos: Each microservice have its own documentation within its GitHub repository, stored under a /docs directory. This helps to keep the documentation close to the code.
     Example: /ufaas-core/docs
   
   ### 1.2. Documentation Types and Structure
   Within the main documentation repo and each microservice repo, we organize the documents in a way that aligns with how users will engage with them:

  - README.md:
    - Purpose: Provide an overview of the service or the main project.
    - Content: Brief description, purpose, and links to further documentation.

  - /docs directory:
    - App Description (Functional):
      - app-description.md - High-level overview of the app’s functionality, use cases, and user stories.
    - App Architecture (Technical):
      - architecture-overview.md - Technical details of the system architecture, including diagrams.
      - microservices-overview.md - Detailed information on each microservice’s role, communication, and deployment.
    - UML Diagrams:
      - /uml/ - Store UML diagrams here. Use tools like PlantUML, Lucidchart, or draw.io, and include both source files and exported images (e.g., .png).[it is better to choose a tool to use in commen]
    - Test Documents:
      - test-strategy.md - Overall testing strategy, including unit tests, integration tests, and end-to-end tests.
      - test-cases.md - Detailed test cases for each service.
    - API Documentation:
      - api-overview.md - High-level API design principles, versioning strategy.
      - /api/v1/ - Detailed API reference (endpoints, parameters, responses). We use Swagger/OpenAPI in commen to help us automate this. See the link to API doc here for detail and also test them.

## 2. Principles and Best Practices (Continued)
### 2.1. Consistency

- **Language and Terminology:** Define a style guide for terminology and tone (e.g., formal vs. informal). Ensure everyone on the team uses the same terms for features, services, and actions.
- **Formatting:** Use Markdown for all textual documentation to keep formatting consistent and simple. Markdown is widely supported and works well with GitHub’s native rendering.
- **Structure:** Ensure that each type of document (e.g., functional descriptions, technical architecture) follows a similar structure. This helps users know what to expect and where to find information.

### 2.2. Modularity

- **Decouple Documentation:** Separate documentation for each microservice and have a centralized documentation that links to individual microservice docs. This allows for easier updates and maintenance as microservices evolve independently.
- **Linking:** Use relative links within your documentation to connect related sections or documents. This keeps navigation smooth and logical, especially when users are exploring your GitHub repository.

### 2.3. Version Control

- **Versioning Documentation:** As your application evolves, so should your documentation. Use branches or tags in GitHub to maintain different versions of your documentation. For example, you can have v1.0, v2.0 branches for major releases.
- **Changelog:** Maintain a CHANGELOG.md file in the main documentation repository that tracks significant changes to the documentation itself, especially API changes, new features, or deprecated functionality.

### 2.4. Accessibility

- **Readability:** Write in clear, simple language. Avoid jargon unless absolutely necessary, and always explain terms or concepts that might be unfamiliar to your audience.
- **Searchability:** Use clear headings and subheadings, and consider adding a Table of Contents at the beginning of longer documents. You can also leverage GitHub’s Wiki feature to make documentation more navigable.
- **Images and Diagrams:** Use visuals like UML diagrams, flowcharts, and API schemas where possible. Ensure that these visuals are well-labeled and described in the accompanying text.


ChatGPT suggestion on "Design documentation principales, structure and procedures" for UFaaS:
https://chatgpt.com/share/66e68b6c-47cc-8011-869b-f667aac85557
