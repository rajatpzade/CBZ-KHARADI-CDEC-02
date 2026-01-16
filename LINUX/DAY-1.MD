# Day-1

---

## Introduction to DevOps

### What is DevOps?

DevOps (Development + Operations) is a modern software development approach that emphasizes collaboration, automation, and integration between software developers and IT operations teams. The primary goal is to shorten the development lifecycle and enable continuous delivery of high-quality software.

![Alt Text](img/e404c522-8c6c-429a-b226-f8c98b9c3948.gif)

### Historical Context

**Before DevOps:**
- Development and Operations teams worked in silos
- Release cycles took months or years
- Manual processes led to frequent errors
- Communication was poor between teams
- Blame culture existed when things went wrong

**After DevOps:**
- Teams work collaboratively from the start
- Releases happen multiple times per day
- Automation reduces human errors
- Shared responsibility and accountability
- Focus on continuous improvement

### Core Principles of DevOps

**1. Collaboration**
- Developers, testers, and operations work together
- Shared goals and metrics
- Open communication channels
- Joint planning and decision-making

**2. Automation**
- Automate repetitive manual tasks
- Reduce human errors
- Speed up processes (build, test, deploy)
- Enable faster feedback loops

**3. Continuous Integration (CI)**
- Developers integrate code multiple times per day
- Automated tests run on every code change
- Issues detected early
- Example: Jenkins automatically builds code when pushed to repository

**4. Continuous Deployment (CD)**
- Automated deployment to production environments
- Fast and reliable releases
- Rollback capabilities if issues occur
- Example: Code automatically deployed after passing all tests

**5. Infrastructure as Code (IaC)**
- Infrastructure defined in code (not manual setup)
- Version control for infrastructure
- Reproducible and scalable environments
- Tools: Terraform, Ansible, CloudFormation

**6. Monitoring and Logging**
- Real-time visibility into application performance
- Quick detection of issues
- Data-driven decision making
- Tools: Prometheus, Grafana, ELK Stack

**7. Feedback Culture**
- Regular feedback loops
- Learning from failures
- Continuous improvement mindset
- Retrospectives and reviews

### Benefits of DevOps

| Benefit | Explanation |
|---------|-------------|
| **Faster Time-to-Market** | Reduce time between development and production (from months to days/hours) |
| **Higher Quality** | Automated testing catches issues early |
| **Reduced Risk** | Better monitoring and quick rollback capabilities |
| **Cost Efficiency** | Automation reduces manual work; better resource utilization |
| **Employee Satisfaction** | Reduced toil; focus on meaningful work |
| **Scalability** | Infrastructure as code enables easy scaling |

---

## How IT Company Works

### Organizational Structure

```
┌─────────────────────────────────────────┐
│         IT Company Management            │
├─────────────────────────────────────────┤
│                                         │
│  ┌─────────────┐  ┌──────────────┐    │
│  │Development  │  │   Testing    │    │
│  │   Team      │  │    Team      │    │
│  └─────────────┘  └──────────────┘    │
│                                         │
│  ┌─────────────┐  ┌──────────────┐    │
│  │ Operations  │  │   Project    │    │
│  │   Team      │  │  Management  │    │
│  └─────────────┘  └──────────────┘    │
│                                         │
└─────────────────────────────────────────┘
```

### Department Responsibilities

#### 1. Development Team
**What they do:**
- Analyze client requirements
- Design software architecture
- Write code for features and functionality
- Participate in code reviews
- Fix bugs identified by testers
- Create technical documentation

**Skills Needed:**
- Programming languages (Java, Python, JavaScript, Go, etc.)
- Database design (SQL, NoSQL)
- System design principles
- Version control (Git)
- API development

**Example:** If a client needs an e-commerce website, developers write the code for product catalog, shopping cart, payment integration, etc.

---

#### 2. Testing/QA Team
**What they do:**
- Create test cases based on requirements
- Execute manual and automated tests
- Identify and document bugs
- Verify bug fixes
- Perform performance testing
- Ensure compliance with requirements

**Skills Needed:**
- Test automation (Selenium, TestNG,Postman,sonarqube)
- Manual testing techniques
- SQL for database testing
- API testing (Postman)
- Performance testing tools

**Example:** For the e-commerce website, testers verify that products display correctly, shopping cart calculations are accurate, payment processing works, etc.

---

#### 3. Operations Team
**What they do:**
- Manage servers and infrastructure
- Handle deployment processes
- Monitor application performance
- Manage databases
- Handle backups and disaster recovery
- Ensure system uptime and reliability
- Apply security patches

**Skills Needed:**
- Linux/Unix administration
- Server management
- Network management
- Database administration
- Cloud platforms (AWS, Azure)
- Automations tools (Gir,Docker,K8s,terrform,etc.)

**Example:** Operations team ensures the e-commerce website stays online 24/7, manages database backups, handles traffic spikes during sales, etc.

---

#### 4. Project Management
**What they do:**
- Gather requirements from clients
- Plan project timeline and resources
- Assign tasks to team members
- Track progress
- Manage communication with clients
- Handle risks and issues
- Ensure project stays within budget

**Skills Needed:**
- Agile/Scrum methodologies
- Communication skills
- Leadership
- Risk management
- Budget management

---

### Software Development Lifecycle (SDLC)

A typical IT company follows this process for every project:

**Phase 1: Requirements Gathering**
- Meet with clients to understand needs
- Document functional and non-functional requirements
- Create specifications document
- **Timeline:** 1-2 weeks

**Phase 2: Design**
- Architects design the solution
- Create system architecture diagrams
- Database schema design
- Create technical specifications
- **Timeline:** 1-2 weeks

**Phase 3: Development**
- Developers write code based on design
- Code committed to version control multiple times daily
- Code reviews by senior developers
- **Timeline:** 2-4 weeks (depends on complexity)

**Phase 4: Testing**
- Testers execute test cases
- Report bugs to developers
- Developers fix bugs
- Regression testing (retesting after fixes)
- **Timeline:** 1-2 weeks

**Phase 5: Deployment**
- Prepare production environment
- Deploy application to production
- Smoke testing in production
- **Timeline:** 1 day

**Phase 6: Maintenance & Support**
- Monitor application performance
- Fix issues reported by users
- Release patches and updates
- **Timeline:** Ongoing

### Common Challenges in IT Companies

**1. Slow Release Cycles**
- Testing takes weeks
- Manual deployment processes
- Approval workflows cause delays
- **Solution:** DevOps automation

**2. Poor Communication**
- Silos between teams
- Miscommunication about requirements
- Blame culture when issues occur
- **Solution:** Collaborative tools, shared goals

**3. Manual and Error-Prone Processes**
- Manual testing misses bugs
- Manual deployments cause errors
- Infrastructure setup is repetitive
- **Solution:** Automation and IaC

**4. Scalability Issues**
- Adding servers is time-consuming
- Cannot handle traffic spikes
- **Solution:** Cloud infrastructure, containerization

---

## What is an Application?

### Definition

An **application** (or app) is a software program or set of programs designed to perform specific functions or tasks for end-users, businesses, or organizations.

### Characteristics of Applications

- **Purpose-driven:** Designed to solve specific problems
- **User-centric:** Built with end-users in mind
- **Functional:** Performs specific operations
- **Maintainable:** Can be updated and improved
- **Scalable:** Can handle growth in users/data

### Types of Applications

#### 1. Web Applications
**Definition:** Applications accessed through web browsers using HTTP/HTTPS protocols

**Examples:**
- Gmail (email service)
- Google Docs (document editing)
- Facebook (social media)
- Netflix (video streaming)

**Architecture:**
```
User's Browser → Web Server → Application Server → Database
     (Client)       (Server)        (Business Logic)   (Data)
```

**Advantages:**
- No installation required
- Works on any device with a browser
- Easy to update
- Accessible from anywhere

---

#### 2. Desktop Applications
**Definition:** Applications installed directly on computers (Windows, Mac, Linux)

**Examples:**
- Microsoft Office (Word, Excel, PowerPoint)
- Adobe Photoshop (image editing)
- Visual Studio Code (code editor)
- Slack (communication)

**Advantages:**
- Better performance (local processing)
- Works offline
- Full access to system resources

**Disadvantages:**
- Requires installation on each machine
- Updates need manual installation
- Platform-specific

---

#### 3. Mobile Applications
**Definition:** Applications installed on smartphones and tablets

**Examples:**
- Instagram (social media)
- Uber (ride-sharing)
- WhatsApp (messaging)
- Pokemon Go (gaming)

**Types:**
- **Native Apps:** Built for specific OS (iOS using Swift, Android using Java/Kotlin)
- **Hybrid Apps:** Use web technologies (React Native, Flutter)

**Advantages:**
- Optimized for mobile devices
- Access to device features (camera, GPS, contacts)
- Works offline

---

#### 4. Enterprise Applications
**Definition:** Large-scale applications used by organizations for business operations

**Examples:**
- SAP (enterprise resource planning)
- Salesforce (customer relationship management)
- Oracle (database management)
- Jira (project management)

**Characteristics:**
- Serve thousands of users
- Handle massive amounts of data
- Mission-critical for businesses
- Complex and feature-rich

---

### Application Architecture

#### Monolithic Architecture
**Structure:** Entire application in one large codebase
```
┌────────────────────────────────────────┐
│      Monolithic Application             │
├────────────────────────────────────────┤
│  ┌──────────────────────────────────┐  │
│  │  User Interface (UI)             │  │
│  │  Business Logic                  │  │
│  │  Data Access Layer               │  │
│  │  Database                        │  │
│  └──────────────────────────────────┘  │
└────────────────────────────────────────┘
```

**Pros:** Simple to develop, easy to deploy
**Cons:** Hard to scale, difficult to maintain, one bug affects everything

#### Microservices Architecture
**Structure:** Application broken into small, independent services
```
┌──────────┐  ┌──────────┐  ┌──────────┐
│  User    │  │ Product  │  │ Payment  │
│ Service  │  │ Service  │  │ Service  │
└──────────┘  └──────────┘  └──────────┘
     ↓             ↓              ↓
   DB 1          DB 2           DB 3
```

**Pros:** Scalable, independent deployment, easy to maintain
**Cons:** More complex, requires DevOps expertise

---

### Application Development Lifecycle

**1. Planning**
- Understand client needs
- Define scope and features
- Estimate timeline and resources
- **Duration:** 1-2 weeks

**2. Design**
- UI/UX design (mockups, wireframes)
- System architecture design
- Database design
- API design
- **Duration:** 1-2 weeks

**3. Development**
- Write code for frontend (UI)
- Write code for backend (business logic)
- Integrate different components
- **Duration:** 2-8 weeks (depends on complexity)

**4. Testing**
- Unit testing (individual components)
- Integration testing (components together)
- System testing (entire application)
- UAT (User Acceptance Testing)
- **Duration:** 1-4 weeks

**5. Deployment**
- Prepare production environment
- Deploy application
- Monitor performance
- **Duration:** 1-2 days

**6. Maintenance**
- Fix bugs reported by users
- Add new features
- Improve performance
- **Duration:** Ongoing

---

## Developers vs Testers vs DevOps Engineers

### 1. Developers (Software Engineers)

#### Who are they?
Developers are professionals who write code to build software applications. They transform requirements into functional software.

#### Key Responsibilities
- **Code Development:** Write clean, efficient, maintainable code
- **Feature Implementation:** Build features based on requirements
- **Bug Fixing:** Fix issues reported by testers
- **Code Reviews:** Review peers' code and provide feedback
- **Documentation:** Create technical documentation
- **Optimization:** Improve code performance
- **Collaboration:** Work with testers and operations

#### Skills Required
**Programming Languages:**
- Backend: Java, Python, C++, Go, Node.js
- Frontend: JavaScript, HTML, CSS, React, Angular
- Mobile: Swift, Kotlin, Flutter, React Native

**Other Skills:**
- Database design (SQL, NoSQL)
- API development (REST, GraphQL)
- Design patterns (MVC, Singleton, Factory)
- Version control (Git/GitHub)
- Problem-solving and algorithms

#### Tools & Technologies Used
```
IDEs/Editors:
├── Visual Studio Code
├── IntelliJ IDEA
├── Eclipse
└── Sublime Text

Version Control:
├── Git
├── GitHub
├── GitLab
└── Bitbucket

Databases:
├── MySQL
├── PostgreSQL
├── MongoDB
└── Redis

Frameworks:
├── Spring Boot (Java)
├── Django (Python)
├── React (JavaScript)
└── Laravel (PHP)
```

#### Daily Tasks Example
```
9:00 AM  - Daily standup (15 min)
9:15 AM  - Code new feature for login page
10:30 AM - Code review from senior developer
11:00 AM - Fix comments from code review
12:00 PM - Lunch break
1:00 PM  - Unit testing of login feature
2:00 PM  - Commit code to GitHub
3:00 PM  - Fix bug reported by testers
4:00 PM  - Documentation
5:00 PM  - End of day
```

---

### 2. Testers (QA Engineers)

#### Who are they?
Testers are professionals who verify that software works as intended. They find bugs before users encounter them.

#### Key Responsibilities
- **Test Planning:** Plan testing strategy based on requirements
- **Test Case Design:** Create test cases covering all scenarios
- **Manual Testing:** Execute tests step-by-step
- **Automated Testing:** Write automation scripts
- **Bug Reporting:** Document bugs with detailed information
- **Regression Testing:** Retest after bug fixes
- **Performance Testing:** Test application under load
- **Documentation:** Create test reports and metrics

#### Skills Required
**Testing Knowledge:**
- Black-box testing (test without seeing code)
- White-box testing (test knowing code structure)
- API testing
- Performance/Load testing
- Security testing
- Mobile testing

**Tools & Technologies:**
- Test automation frameworks (Selenium, TestNG)
- Test management tools (TestRail, Zephyr)
- Bug tracking (Jira)
- Performance tools (JMeter, LoadRunner)
- API testing (Postman, REST Assured)

#### Example Test Case
```
Test Case: Login with Valid Credentials
────────────────────────────────────────
Precondition: User is on login page
Steps:
1. Enter valid email in email field
2. Enter valid password in password field
3. Click "Login" button
Expected Result: User logged in, redirected to dashboard
Actual Result: [To be filled during execution]
Status: PASS/FAIL
```

#### Daily Tasks Example
```
9:00 AM  - Daily standup
9:15 AM  - Review new features and requirements
10:00 AM - Create test cases for new login feature
11:00 AM - Execute test cases manually
12:00 PM - Report bugs in Jira
1:00 PM  - Lunch break
2:00 PM  - Retest fixed bugs
3:00 PM  - Execute automation tests
4:00 PM  - Performance testing
5:00 PM  - Test report generation
```

---

### 3. DevOps Engineers

#### Who are they?
DevOps engineers are professionals who bridge the gap between development and operations. They automate and optimize the entire software delivery process.

#### Key Responsibilities
- **CI/CD Pipeline:** Build and maintain automated build/test/deploy pipelines
- **Infrastructure Management:** Manage servers, networks, and cloud resources
- **Containerization:** Deploy applications using Docker/Kubernetes
- **Infrastructure as Code:** Define infrastructure in code
- **Monitoring & Logging:** Monitor application and infrastructure health
- **Security:** Implement security best practices
- **Disaster Recovery:** Ensure backup and recovery procedures
- **Performance Optimization:** Optimize infrastructure and applications
- **Cost Management:** Optimize cloud costs

#### Skills Required
**Core Skills:**
- Linux/Unix administration
- Networking and firewalls
- Cloud platforms (AWS, Azure, GCP)
- Containerization (Docker, Kubernetes)
- CI/CD tools (Jenkins, GitLab CI, GitHub Actions)
- Infrastructure as Code (Terraform, Ansible)
- Scripting (Bash, Python, Go)
- Monitoring tools (Prometheus, Grafana)
- Logging tools (ELK Stack, Splunk)

#### DevOps Tool Stack
```
Planning & Version Control:
├── Git/GitHub/GitLab
├── Jira
└── Confluence

CI/CD:
├── Jenkins
├── GitLab CI/CD
├── GitHub Actions
└── CircleCI

Containerization:
├── Docker
├── Kubernetes
└── Docker Compose

Infrastructure as Code:
├── Terraform
├── Ansible
├── CloudFormation
└── Puppet

Monitoring:
├── Prometheus
├── Grafana
├── ELK Stack
└── Datadog

Cloud Platforms:
├── AWS
├── Google Cloud
└── Microsoft Azure
```

#### DevOps Workflow Example
```
Developer pushes code → GitHub
         ↓
Webhook triggers Jenkins
         ↓
Jenkins pulls code from GitHub
         ↓
Automated Build (compile code)
         ↓
Automated Tests (unit, integration)
         ↓
Code Quality Check (SonarQube)
         ↓
Build Docker Image
         ↓
Push to Docker Registry
         ↓
Deploy to Staging (Kubernetes)
         ↓
Automated Integration Tests
         ↓
Deploy to Production
         ↓
Monitor with Prometheus/Grafana
```

#### Daily Tasks Example
```
9:00 AM  - Daily standup
9:15 AM  - Monitor production dashboards
9:30 AM  - Fix pipeline failure (Jenkins job)
10:30 AM - Write Terraform code for new AWS infrastructure
12:00 PM - Code review for infrastructure changes
1:00 PM  - Lunch break
2:00 PM  - Deploy new version to staging
3:00 PM  - Investigate production issue
4:00 PM  - Optimize Docker image
5:00 PM  - Documentation and knowledge sharing
```

---

### Detailed Comparison

#### 1. Focus & Goals

| Aspect | Developer | Tester | DevOps |
|--------|-----------|--------|--------|
| **Main Focus** | Writing code/features | Finding bugs/quality | Automation/deployment |
| **Goal** | Implement functionality | Ensure quality | Fast & reliable delivery |
| **Mindset** | Build new features | Break features | Optimize processes |
| **Success Metric** | Features delivered | Bugs found | Deployment frequency, speed |

---

#### 2. Timeline & Work Phases

| Phase | Developer | Tester | DevOps |
|-------|-----------|--------|--------|
| **Planning** | Requirements gathering | Test case design | Infrastructure planning |
| **Development** | Code new features | Design tests | Build pipelines |
| **Execution** | Implementation | Test execution | Deploy & monitor |
| **Continuous** | Ongoing coding | Ongoing testing | Always monitoring |

---

#### 3. Interaction with Other Roles

**Developer:**
```
Developers ←→ Testers (report bugs)
   ↓
Testers report bugs → Developers fix
   ↓
DevOps (deployment)
```

**Tester:**
```
Testers ← Requirements (Product Managers)
   ↓
Test Cases ↓
   ↓
Developers (code) → Testers (test)
   ↓
Testers → Developers (bug reports)
   ↓
DevOps (production validation)
```

**DevOps:**
```
Developers (code) → DevOps (automated build/test/deploy)
Testers (testing requirements) ← DevOps (test environments)
Operations (infrastructure) ← DevOps (Infrastructure as Code)
   ↓
Monitors & Alerts
```

---

#### 4. Technologies & Tools

**Developer Tools:**
- IDEs: VS Code, IntelliJ
- Languages: Java, Python, JavaScript
- Databases: MySQL, MongoDB
- Frameworks: Spring, React, Django
- Version Control: Git

**Tester Tools:**
- Automation: Selenium, TestNG, Cypress
- API Testing: Postman, REST Assured
- Performance: JMeter, LoadRunner
- Bug Tracking: Jira
- Test Management: TestRail

**DevOps Tools:**
- CI/CD: Jenkins, GitLab CI
- Containerization: Docker, Kubernetes
- IaC: Terraform, Ansible
- Monitoring: Prometheus, Grafana
- Cloud: AWS, Azure, GCP

---

#### 5. Problem-Solving Approaches

**Developer** - "How do I implement this feature?"
- Analyzes requirements
- Designs solution
- Writes code
- Tests locally
- Commits to version control

**Tester** - "How can I break this feature?"
- Analyzes requirements
- Designs test scenarios
- Creates test cases
- Executes tests
- Reports issues

**DevOps** - "How do I automate this process?"
- Analyzes deployment needs
- Designs pipeline
- Writes automation scripts
- Implements monitoring
- Optimizes performance

---

#### 6. Career Growth Paths

**Developer:**
```
Junior Developer → Senior Developer → Tech Lead → Architect
                                           ↓
                                     Engineering Manager
```

**Tester:**
```
QA Engineer → Senior QA → QA Lead → Test Architect
                               ↓
                         QA Manager
```

**DevOps:**
```
DevOps Engineer → Senior DevOps → DevOps Lead → Infrastructure Architect
                                       ↓
                               DevOps Manager/Engineering Manager
```

---

## Day-2:

## Top Features of Linux
- Open source: source code available and modifiable.
- Stability and reliability: long uptimes for servers.
- Security: strong permission model, SELinux/AppArmor support.
- Performance: efficient resource usage, suitable for servers and embedded systems.
- Package management: apt, yum, pacman for easy software install/updates.
- Variety of distributions: Ubuntu, CentOS, Fedora, Arch, etc.
- Strong networking and server tools: ssh, cron, systemd, iptables/nftables.
- Customizability: kernels, desktop environments, shells.
- Community support and documentation.

---

## Linux Everywhere
- Servers: web, database, mail, and cloud infrastructure.
- Desktops: developer and power-user environments.
- Embedded systems: routers, IoT devices, smart TVs.
- Mobile: Android uses the Linux kernel.
- Containers & orchestration: Docker, Kubernetes run on Linux.
- Supercomputers and scientific computing.

---

## Unlocking Linux Careers
- Roles: System Administrator, DevOps Engineer, Site Reliability Engineer (SRE), Cloud Engineer.
- Typical tasks: server setup, automation, monitoring, troubleshooting, security hardening.
- Entry path: learn CLI, shell scripting, networking, system internals.
- Progression: certification, specialization (containers, cloud, security).

---

## Why AWS Stands Out in the Cloud Market
- Broad service portfolio: compute, storage, database, ML, analytics, serverless.
- Global footprint: many regions and availability zones.
- Mature ecosystem: rich partner network, integrations, marketplace.
- Enterprise features: compliance, security controls, managed services.
- Scale and reliability: proven at large scale for many customers.

---

## Overview of AWS
- Core services:
  - Compute: EC2, Lambda
  - Storage: S3, EBS, EFS
  - Databases: RDS, DynamoDB
  - Networking: VPC, Route 53, CloudFront
  - Management & Monitoring: CloudWatch, CloudTrail
- Billing: pay-as-you-go, reserved and spot instances for cost savings.
- Security: IAM for identity and access control, encryption, compliance.

---

## Customer Success Stories (short examples)
- Netflix: streaming infrastructure on AWS for global scale.
- Airbnb: uses AWS for scalable backend services.
- Spotify: data processing and analytics on AWS services.
- Small startups: rapid prototyping and global rollout without heavy infra investment.

---

## Scalability and Flexibility of Business with AWS
- Auto-scaling: scale compute automatically with demand.
- Managed services: reduce operational overhead (RDS, EKS).
- Global reach: deploy applications close to users.
- Cost controls: budgeting tools, right-sizing, reserved capacity.

---

## Comparing AWS with Competitors
- AWS vs Azure vs GCP:
  - AWS: broadest service set and market maturity.
  - Azure: strong enterprise integrations, Microsoft ecosystem.
  - GCP: strong data/ML offerings and competitive pricing.
- Choice depends on requirements: services, integrations, price, existing vendor relationships.

---

## Why DevOps is a Growing Career Field
- Faster software delivery expectations from businesses.
- Need for automation, reliability, and continuous delivery.
- Cross-functional skillset valuable across industries.
- DevOps practices reduce time-to-market and operational risk.

---

## High Demand for DevOps Professionals
- Employers seek skills in CI/CD, cloud, containers, IaC, monitoring.
- Roles exist in startups to large enterprises and cloud-native companies.
- Remote and hybrid opportunities widely available.

---

## Salary Expectations and Career Growth
- Entry-level: system admin / junior DevOps — varies by region.
- Mid-level: DevOps Engineer / Cloud Engineer — significant salary increase.
- Senior-level: SRE, DevOps Lead, Cloud Architect — higher compensation and leadership roles.
- Salaries depend on region, experience, certifications, and tech stack.

---

## Skills and Expertise in DevOps
- Linux administration and scripting (Bash, Python).
- CI/CD tools: Jenkins, GitHub Actions, GitLab CI.
- Containers & orchestration: Docker, Kubernetes.
- Infrastructure as Code: Terraform, CloudFormation, Ansible.
- Cloud platforms: AWS, Azure, GCP.
- Monitoring & logging: Prometheus, Grafana, ELK.
- Networking, security best practices, and automation.

---

## Certifications and Learning Resources
- AWS: AWS Certified Cloud Practitioner, AWS Solutions Architect.
- DevOps: Certified Kubernetes Administrator (CKA), HashiCorp Terraform Associate.
- Linux: Linux Foundation Certified, CompTIA Linux+.
- Learning resources: official docs, free courses, hands-on labs (cloud free tiers), community tutorials.

---

## The Future of DevOps Careers
- Growing emphasis on SRE practices and platform engineering.
- More automation, AI-assisted operations, and GitOps adoption.
- Need for multi-cloud and security-focused DevOps skills.

---

## Goal to Achieve in CDEC
- Build foundational skills: Linux CLI, shell scripting, basic networking.
- Learn cloud basics (AWS) and core services.
- Practice CI/CD pipelines and container workflows.
- Earn at least one relevant certification (Linux / AWS / Kubernetes).
- Complete hands-on projects and labs to demonstrate practical skills.

---

## Getting Started with Operating Systems

### What is an Operating System (OS)?
- Software that manages computer hardware and provides services to applications and users.
- Acts as an intermediary between user programs and physical hardware.

### Main Responsibilities
- Process management (create, schedule, terminate processes)
- Memory management (allocate/free RAM)
- File system management (read/write, permissions)
- Device management (drivers for hardware)
- Security and access control
- User interface (CLI/GUI)

---

## Different Types of Operating Systems
- Batch OS — Executes jobs in batches (old mainframes).
- Time-Sharing / Multiuser — Many users share CPU time (e.g., Unix).
- Real-Time OS — Deterministic response for embedded systems.
- Distributed OS — Manages distributed resources across networked machines.
- Network OS — Provides network services (file/print sharing).
- Mobile OS — Optimized for phones/tablets (Android, iOS).
- Embedded OS — For appliances and IoT devices (RTOS, Embedded Linux).

---

## How Operating Systems Impact Your Daily Life
- Enable running apps (browsers, email, messaging).
- Manage smartphone operations (calls, notifications, apps).
- Provide security (user accounts, permissions, updates).
- Control home devices (routers, smart TVs) via embedded OS.
- Power cloud servers and web services people use daily.

---

## Windows vs Unix vs Linux

### Ownership and Origin
- Windows: Developed by Microsoft; proprietary.
- Unix: Originated at AT&T Bell Labs (1970s); many commercial variants (AIX, HP-UX).
- Linux: Kernel by Linus Torvalds (1991); open-source, many distributions (Ubuntu, CentOS).

### Cost and Licensing
- Windows: Commercial license; paid for many editions.
- Unix: Commercial licensing for most proprietary flavors.
- Linux: Mostly free/open-source (GPL); some enterprise distributions offer paid support.

### Security and Privacy
- Windows: Larger target for malware; frequent security updates; telemetry in some editions.
- Unix: Historically used in servers; strong POSIX security model.
- Linux: Strong permission model; active patching and community audits; customizable privacy.

### User Interface
- Windows: Graphical, user-friendly GUI; consistent UX.
- Unix: Historically CLI-first; GUIs available (X11, Wayland).
- Linux: Flexible — CLI (bash, zsh) and multiple desktop environments (GNOME, KDE).

---

## What is a Server?
- A server is a computer or program that provides services to other computers (clients) over a network.
- Examples: web server (Apache, Nginx), database server (MySQL, PostgreSQL), file server (Samba).

---

## Desktop OS vs Server OS

Desktop OS
- Optimized for interactive user experience (GUI, multimedia, peripherals).
- Examples: Windows Desktop, macOS, Ubuntu Desktop.
- Focus: user applications, responsiveness.

Server OS
- Optimized for reliability, performance, remote access and headless operation.
- Examples: Windows Server, Ubuntu Server, CentOS, RHEL.
- Focus: network services, concurrency, uptime, security.

Key differences
- GUI presence (server often headless), default services, update cadence, tuning for workloads.

---

## Introduction to Linux
- Linux refers to the kernel; common distributions bundle the kernel with GNU tools and packages.
- Popular distros: Ubuntu, Debian, Fedora, CentOS, Arch.
- Strengths: open-source, flexible, strong server adoption, container & cloud friendly.

Quick commands for students:
- Check kernel and OS:
  - uname -a
  - lsb_release -a  (may require lsb-release package)
- List processes:
  - ps aux | head
  - top or htop
- Disk and filesystems:
  - lsblk
  - df -h

---

## Architecture of Linux — Layered Notes

- Hardware
  - Physical components: CPU, RAM, disk, network cards, peripherals.
  - Provides raw resources that the kernel manages.

- Kernel
  - Core of the OS: device drivers, process scheduler, memory manager, filesystem (VFS), network stack.
  - Exposes system calls as the interface for user-space programs.
  - Runs in kernel space with full hardware access.

- Shell
  - Command-line interface that interprets user commands and scripts (examples: bash, zsh).
  - Acts as a bridge between the user and kernel (invokes system calls, launches processes).
  - Can be used interactively or for automation via scripts.

- Application
  - User-space programs (browsers, editors, daemons, services).
  - Run with limited privileges and use system calls to request kernel services.
  - Isolated from kernel space to protect system stability and security.

- User (User Layer)
  - Humans and user accounts interacting with the system via shell or GUI.
  - Owns and runs applications; subject to permission and access control enforced by kernel.
  - Includes desktop environments and user sessions.

Diagram (simple)
- Hardware ←→ Kernel (drivers, scheduler, memory) ←→ System Calls ←→ User Space (shells, services, apps)

![Alt Text](img/Linux_arch.png)

---

## Simple Learning Exercises
1. Identify your OS:
   - uname -a
   - lsb_release -a
2. Create a file and check permissions:
   - touch ~/testfile && ls -l ~/testfile
3. View running services:
   - systemctl list-units --type=service | head
4. Explore processes:
   - ps aux --sort=-%cpu | head

---

## Quick Summary for Students
- OS manages hardware and provides a platform for apps.
- Types of OS vary by purpose (desktop, server, real-time, embedded).
- Linux is open-source, widely used on servers and in cloud environments.
- Understanding kernel, system calls, filesystem, and user space is key to Linux mastery.