Dealer Evaluation Microservices System

A cloud-native application built using a Microservices Architecture. This project demonstrates the deployment of multiple independent services (Python, Node.js, and HTML/JS) into a unified ecosystem using IBM Cloud Code Engine.

This system consists of three distinct microservices that communicate via REST APIs:
graph TD
    User((User/Browser)) -->|Port 5001| FE[Frontend Microservice]
    FE -->|API Call| BE1[Product Details API]
    FE -->|API Call| BE2[Dealer Pricing API]
    
    subgraph "IBM Cloud Code Engine Cluster"
        FE[Frontend - HTML/JS]
        BE1[Product Details - Python/Flask]
        BE2[Dealer Pricing - Node.js/Express]
    end

    BE1 ---|Endpoint: /products| BE1_Info((Product Info))
    BE2 ---|Endpoint: /price| BE2_Price((Pricing Data))

🛠 Tech Stack:
Frontend: HTML5, CSS3, JavaScript (Axios for API orchestration).
Backend A: Python (Flask) – Handles product catalog and dealer mapping.
Backend B: Node.js (Express) – Handles pricing logic and dealer data.
DevOps/Cloud: IBM Cloud Code Engine, Docker (Source-to-Image), IBM Container Registry (ICR).

🚀 Deployment Instructions:
This project is containerized and deployed using IBM Cloud Code Engine CLI.

1. Deploy Product Details (Backend)
ibmcloud ce application create --name prodlist \
  --image us.icr.io/${SN_ICR_NAMESPACE}/prodlist \
  --registry-secret icr-secret --port 5000 \
  --build-context-dir products_list \
  --build-source https://github.com/ibm-developer-skills-network/dealer_evaluation_backend.git

2. Deploy Dealer Pricing (Backend)
ibmcloud ce application create --name dealerdetails \
  --image us.icr.io/${SN_ICR_NAMESPACE}/dealerdetails \
  --registry-secret icr-secret --port 8080 \
  --build-context-dir dealer_details \
  --build-source https://github.com/ibm-developer-skills-network/dealer_evaluation_backend.git

3. Deploy Frontend Interface
ibmcloud ce application create --name frontend-final \
  --image us.icr.io/${SN_ICR_NAMESPACE}/frontend \
  --registry-secret icr-secret --port 5001 \
  --build-source .

For a professional, portfolio-ready README.md, you want to combine the technical "how-to" with a high-level explanation of the architecture. Since you're showcasing this to potential employers, focusing on the DevOps and Microservices aspects is key.Here is the complete content for your file, organized into one cohesive document:Dealer Evaluation Microservices SystemA cloud-native application built using a Microservices Architecture. This project demonstrates the deployment of multiple independent services (Python, Node.js, and HTML/JS) into a unified ecosystem using IBM Cloud Code Engine.🏗 Architecture OverviewThis system consists of three distinct microservices that communicate via REST APIs.Code snippetgraph TD
    User((User/Browser)) -->|Port 5001| FE[Frontend Microservice]
    FE -->|API Call| BE1[Product Details API]
    FE -->|API Call| BE2[Dealer Pricing API]
    
    subgraph "IBM Cloud Code Engine Cluster"
        FE[Frontend - HTML/JS]
        BE1[Product Details - Python/Flask]
        BE2[Dealer Pricing - Node.js/Express]
    end

    BE1 ---|Endpoint: /products| BE1_Info((Product Info))
    BE2 ---|Endpoint: /price| BE2_Price((Pricing Data))
🛠 Tech StackFrontend: HTML5, CSS3, JavaScript (Axios for API orchestration).Backend A: Python (Flask) – Handles product catalog and dealer mapping.Backend B: Node.js (Express) – Handles pricing logic and dealer data.DevOps/Cloud: IBM Cloud Code Engine, Docker (Source-to-Image), IBM Container Registry (ICR).🚀 Deployment InstructionsThis project is containerized and deployed using IBM Cloud Code Engine CLI.1. Deploy Product Details (Backend)Bashibmcloud ce application create --name prodlist \
  --image us.icr.io/${SN_ICR_NAMESPACE}/prodlist \
  --registry-secret icr-secret --port 5000 \
  --build-context-dir products_list \
  --build-source https://github.com/ibm-developer-skills-network/dealer_evaluation_backend.git
2. Deploy Dealer Pricing (Backend)Bashibmcloud ce application create --name dealerdetails \
  --image us.icr.io/${SN_ICR_NAMESPACE}/dealerdetails \
  --registry-secret icr-secret --port 8080 \
  --build-context-dir dealer_details \
  --build-source https://github.com/ibm-developer-skills-network/dealer_evaluation_backend.git
3. Deploy Frontend InterfaceBashibmcloud ce application create --name frontend-final \
  --image us.icr.io/${SN_ICR_NAMESPACE}/frontend \
  --registry-secret icr-secret --port 5001 \
  --build-source .

💡 Key Learning Objectives
Polyglot Programming: Successfully integrated services written in different languages (Python & Node.js) into a single functional UI.

Containerization: Automated the creation of Docker images directly from GitHub source code using Source-to-Image (S2I) builds.

Cloud Orchestration: Configured registry secrets and environment variables to allow secure communication between isolated containers.

Asynchronous UX: Implemented dynamic dropdown menus that fetch and render data without reloading the page using the Axios library.🔧 

Troubleshooting & Lessons Learned
Build Contexts: Managed monorepo complexities by correctly setting the --build-context-dir for specific sub-projects.

Deployment Resilience: Resolved deployment timeouts by utilizing ce application update and implementing unique application naming conventions.

State Management: Optimized frontend logic to ensure DOM elements (like the Dealer dropdown) clear and rebuild correctly based on user input.

📄 LicenseThis project is licensed under the Apache License 2.0.