---
description: Generate professional AWS architecture diagrams with intelligent multi-layer orchestration
---

# AWS Architecture Diagram Generator

**Intelligent orchestrator-based diagram generation with automatic layer detection and specialized agent coordination.**

## Capabilities

- **Smart Layer Detection**: Automatically detects required layers (storage, observability, security, CI/CD)
- **Multi-Agent Coordination**: Orchestrates specialized agents for comprehensive diagrams
- **Security-First Design**: Enforces 3-tier subnet separation (Public → App → DB)
- **Professional Standards**: Follows AWS Well-Architected Framework visualization guidelines
- **Enhancement Mode**: Add layers to existing diagrams
- **Quality Validation**: Self-validates and corrects before delivery

## Usage

### Basic Usage
```bash
/draw-aws-diagram <path-to-plan-file>
/draw-aws-diagram <architecture-description>
```

### Advanced Usage
```bash
# Explicit layer specification
/draw-aws-diagram <plan-file> --layers=core,storage,observability,security,cicd

# Enhancement mode (add layers to existing diagram)
/draw-aws-diagram --enhance <existing-diagram.drawio> --add=observability,cicd

# Minimal mode (core infrastructure only)
/draw-aws-diagram <plan-file> --minimal
```

## Examples

```bash
# From plan file (auto-detects layers)
/draw-aws-diagram /Users/rupeshpanwar/Documents/PProject/schild/architecture/1-Simple-3-tier-arch-Plan.txt

# Direct description
/draw-aws-diagram "3-tier web app with RDS, S3 storage, CloudWatch monitoring, and CI/CD pipeline"

# Serverless architecture
/draw-aws-diagram "Serverless API with Lambda, API Gateway, DynamoDB, and X-Ray tracing"

# Container-based
/draw-aws-diagram "ECS Fargate cluster with ALB, RDS, and CloudWatch Container Insights"

# Add observability to existing diagram
/draw-aws-diagram --enhance aws-3tier-app.drawio --add=observability
```

---

## Orchestrator Workflow

This slash command invokes the **AWS Diagram Orchestrator Agent**, which intelligently coordinates specialized agents based on your requirements.

**IMPORTANT: Output Directory Configuration**
- All diagrams MUST be saved to: `/Users/rupeshpanwar/Documents/PProject/schild/architecture/diagrams/`
- Use naming convention: `aws-{architecture-name}-{timestamp}.drawio`
- The directory already exists and is ready for use

### Step 1: Invoke Orchestrator Agent

Use the Task tool to launch the orchestrator agent:

```
Launch aws-diagram-orchestrator agent with user input
```

The orchestrator agent will:
1. Analyze your architecture requirements
2. Detect what services and layers are needed
3. Select appropriate specialized agents
4. Coordinate diagram generation
5. Ensure professional quality output

### Step 2: Orchestrator Analyzes Requirements

The orchestrator performs:

**Input Parsing**:
- Read architecture plan file (if provided)
- Parse architecture description
- Extract user preferences (--layers, --minimal, etc.)

**Layer Detection** (Keyword Matching):
```
Detected Keywords → Agents Invoked

"S3", "storage", "bucket" → aws-storage-layer-agent
"CloudWatch", "monitoring", "logging" → aws-observability-layer-agent
"KMS", "Secrets Manager", "encryption" → aws-security-services-agent
"CI/CD", "pipeline", "CodePipeline" → aws-cicd-pipeline-agent
"CloudFront", "CDN", "WAF" → aws-cdn-edge-agent
"ECS", "EKS", "containers" → aws-container-orchestration-agent
"Lambda", "serverless" → aws-serverless-architecture-agent
"Redshift", "Kinesis", "data pipeline" → aws-data-analytics-agent
```

**Architecture Type Detection**:
- **Serverless**: Contains Lambda, API Gateway → Use serverless agent
- **Containers**: Contains ECS, EKS, Kubernetes → Use container agent
- **Traditional**: Default → Use core architecture agent

### Step 3: Agent Execution (Coordinated by Orchestrator)

The orchestrator executes agents in priority order:

**Priority 1: Primary Architecture**
- `aws-core-architecture-agent` (VPC, EC2, RDS, ALB)
- OR `aws-serverless-architecture-agent` (Lambda, API Gateway)
- OR `aws-container-orchestration-agent` (ECS/EKS)

**Priority 2: Infrastructure Layers**
- `aws-storage-layer-agent` (S3, EFS)
- `aws-cdn-edge-agent` (CloudFront, WAF)

**Priority 3: Cross-Cutting Concerns**
- `aws-security-services-agent` (KMS, Secrets Manager - always included)
- `aws-observability-layer-agent` (CloudWatch, CloudTrail, X-Ray)

**Priority 4: Specialized Workflows**
- `aws-cicd-pipeline-agent` (CodePipeline, CodeBuild)
- `aws-data-analytics-agent` (Redshift, Kinesis)
- `aws-backup-recovery-agent` (AWS Backup, DR)

### Step 4: Diagram Assembly

The orchestrator coordinates positioning across zones:

```
┌─────────────────────────────────────────────────────────────┐
│  EDGE LAYER (CloudFront, WAF)                Top: y=50      │
│  ┌────────────────────────────────────────────────────┐     │
│  │ CORE ARCHITECTURE (VPC, EC2, RDS)                 │ OBS │
│  │                                                     │ SRV │
│  │  ┌──────────┐  ┌──────────┐                       │ BLT │
│  │  │   AZ1    │  │   AZ2    │                       │ Y   │
│  │  └──────────┘  └──────────┘                       │     │
│  └────────────────────────────────────────────────────┘ SEC │
│                                                              │
│  CI/CD PIPELINE         |  STORAGE (S3, EFS)    Bottom     │
└─────────────────────────────────────────────────────────────┘

Layout Zones:
- Core: 40,200 → 1560,1140 (main architecture)
- Right Panel: 1600,200 → 1960,1140 (monitoring, security)
- Bottom Panel: 40,1200 → 1560,1560 (CI/CD, storage)
- Edge Layer: 40,50 → 1560,170 (CDN, WAF)
```

### Step 5: Quality Validation

The orchestrator validates:
- [ ] No overlapping components
- [ ] Proper zone allocation
- [ ] AWS color scheme consistency
- [ ] Security architecture (3-tier separation)
- [ ] Valid XML structure
- [ ] Professional spacing and alignment

### Step 6: Output Generation

**Deliverables**:
1. **Diagram file**: `architecture/aws-{name}-{timestamp}.drawio`
2. **Generation report** with:
   - Layers included
   - Components added
   - Diagram dimensions
   - File path
   - Next steps (if applicable)

---

## Available Layers

### Core Infrastructure (Always Included)
- VPC, Subnets (Public, Private App, Private DB)
- Internet Gateway, NAT Gateways
- Route Tables
- EC2 instances, Auto Scaling Groups
- RDS databases (Multi-AZ)
- Application Load Balancer
- Route 53

### Storage Layer (Auto-Detected)
- S3 buckets
- EFS file systems
- EBS volumes
- FSx managed file systems

### Observability Layer (Auto-Detected)
- CloudWatch (metrics, logs, alarms)
- CloudTrail (audit logs)
- X-Ray (distributed tracing)
- EventBridge (event bus)
- SNS (alert notifications)

### Security Services (Always Included)
- KMS (encryption key management)
- Secrets Manager (credentials)
- AWS Certificate Manager (SSL/TLS)
- Security Groups (implied by subnet placement)

### CI/CD Pipeline (Auto-Detected)
- CodePipeline / GitLab CI / GitHub Actions
- CodeBuild (build environments)
- CodeDeploy (deployment)
- ECR (container registry)
- Artifact storage (S3)

### CDN & Edge (Auto-Detected)
- CloudFront (CDN)
- WAF (Web Application Firewall)
- Shield (DDoS protection)
- Global Accelerator

### Container Orchestration (Auto-Detected)
- ECS clusters
- EKS (Kubernetes)
- Fargate
- App Mesh (service mesh)
- Container insights

### Serverless (Auto-Detected)
- Lambda functions
- API Gateway
- Step Functions
- DynamoDB
- SQS/SNS

### Data & Analytics (Auto-Detected)
- Redshift (data warehouse)
- Kinesis (streaming)
- Glue (ETL)
- Athena (query)
- EMR (big data processing)

---

## Orchestrator Agent Registry

### ✅ Currently Available Agents

1. **aws-core-architecture-agent**
   - File: `.claude/agents/aws-diagram-generator.md`
   - Services: VPC, Subnets, IGW, NAT, ALB, EC2, RDS, Route53
   - Status: ✅ Ready

2. **aws-diagram-orchestrator**
   - File: `.claude/agents/aws-diagram-orchestrator.md`
   - Role: Intelligent coordinator
   - Status: ✅ Ready

### ⏳ Agents To Be Created (Priority Order)

**P1: Essential Services (Week 1)**
3. `aws-storage-layer-agent` - S3, EFS, EBS
4. `aws-observability-layer-agent` - CloudWatch, CloudTrail, X-Ray
5. `aws-security-services-agent` - KMS, Secrets Manager, Security Hub

**P2: DevOps & Edge (Week 2)**
6. `aws-cicd-pipeline-agent` - CI/CD workflows
7. `aws-cdn-edge-agent` - CloudFront, WAF, Shield

**P3: Advanced Architectures (Week 3)**
8. `aws-container-orchestration-agent` - ECS, EKS
9. `aws-serverless-architecture-agent` - Lambda-based patterns

**P4: Specialized (Week 4)**
10. `aws-data-analytics-agent` - Data pipelines
11. `aws-backup-recovery-agent` - DR planning
12. `aws-network-security-agent` - Detailed security views

### Fallback Behavior

When an agent is not yet available:
- Orchestrator logs: "Agent {name} not yet implemented"
- Uses core agent to add basic service icons
- Adds TODO annotation in diagram
- Reports to user what was included vs. skipped
- Continues with available agents

---

## Security-First Design Principles

**All diagrams enforce these security best practices:**

### 1. 3-Tier Subnet Separation (CRITICAL)

**❌ NEVER place compute and database in same subnet**

```
Tier 1: Public Subnets (DMZ)
├── Application Load Balancer
└── NAT Gateways

Tier 2: Private Application Subnets
├── EC2 instances
├── ECS/EKS containers
└── Can route outbound via NAT

Tier 3: Private Database Subnets
├── RDS databases
├── ElastiCache
└── NO internet access (isolated)
```

### 2. Defense in Depth
- Network isolation via subnet separation
- Security Groups (implied by placement)
- Encryption at rest (KMS)
- Secrets management (Secrets Manager)
- Monitoring (CloudWatch, CloudTrail)

### 3. Least Privilege Access
- No direct internet access to databases
- ALB as single internet-facing entry point
- NAT Gateways for outbound only
- Private subnets for all application/data layers

---

## How It Works Behind the Scenes

1. **You run**: `/draw-aws-diagram "3-tier app with S3 and monitoring"`

2. **Slash command invokes**: Task tool → aws-diagram-orchestrator agent

3. **Orchestrator analyzes**:
   - Architecture type: Traditional (EC2-based)
   - Detected keywords: "3-tier", "S3", "monitoring"
   - Required agents: core, storage, observability, security

4. **Orchestrator coordinates**:
   ```
   Priority 1: aws-core-architecture-agent
     → Generates VPC, EC2, RDS, ALB
     → Returns: base diagram XML + positioning metadata

   Priority 2: aws-storage-layer-agent
     → Adds S3 buckets to bottom panel
     → Returns: updated XML

   Priority 3: aws-security-services-agent
     → Adds KMS, Secrets Manager to right panel
     → Returns: updated XML

   Priority 3: aws-observability-layer-agent
     → Adds CloudWatch, CloudTrail to right panel
     → Returns: final XML
   ```

5. **Orchestrator assembles**:
   - Merges all XML outputs
   - Validates no overlaps
   - Checks quality standards
   - Saves final diagram

6. **You receive**:
   ```
   ✅ AWS Architecture Diagram Generated

   📊 Layers Included:
   - Core Infrastructure (VPC, EC2, RDS)
   - Storage Services (S3)
   - Observability (CloudWatch)
   - Security Services (KMS, Secrets Manager)

   📁 File: architecture/aws-3tier-app-20251116.drawio
   🔗 Open: https://app.diagrams.net/
   ```

---

## Progressive Enhancement

As new specialized agents are created:
- ✅ **Orchestrator automatically uses them** (no updates needed)
- ✅ **Diagrams become more comprehensive**
- ✅ **New capabilities unlocked**
- ✅ **Backward compatible** (existing commands still work)

### Current Capabilities
- ✅ Core infrastructure (VPC, EC2, RDS, ALB)
- ✅ Basic security (3-tier subnet separation)
- ✅ Intelligent orchestration

### Soon Available (as agents are created)
- ⏳ Storage layer (S3, EFS)
- ⏳ Full observability (CloudWatch, X-Ray, CloudTrail)
- ⏳ Security services (KMS, Secrets Manager)
- ⏳ CI/CD pipelines
- ⏳ Container orchestration
- ⏳ Serverless patterns
- ⏳ Data analytics flows

---

## Troubleshooting

### "Agent not yet implemented" warning
- **Meaning**: Requested service requires agent that's not created yet
- **Action**: Orchestrator uses core agent to add basic icon
- **Workaround**: Manually enhance diagram in draw.io
- **Future**: Agent will be added in upcoming updates

### Diagram too crowded
- **Solution 1**: Orchestrator expands page size (2000x1600)
- **Solution 2**: Creates multi-page diagram (tabs)
- **Solution 3**: Use `--minimal` to show core only

### Services not detected
- **Solution**: Use explicit `--layers` parameter
- **Example**: `--layers=storage,observability,cicd`

---

## Best Practices

1. **Start simple**: Let orchestrator auto-detect layers
2. **Be specific**: Mention services explicitly in plan ("S3", "CloudWatch")
3. **Use enhancement mode**: Add layers incrementally
4. **Review output**: Check generation report for what was included
5. **Iterate**: Add layers progressively as needed

---

## Next Steps After Generation

1. **Open diagram**: https://app.diagrams.net/
2. **Review layers**: Check all components are present
3. **Customize**: Drag, resize, modify as needed
4. **Add annotations**: Include CIDR blocks, SG rules, notes
5. **Export**: PNG/PDF for presentations, SVG for docs

---

## Output Format

All diagrams are generated as:
- **Format**: draw.io XML (.drawio extension)
- **Output Directory**: `/Users/rupeshpanwar/Documents/PProject/schild/architecture/diagrams/`
- **Naming Convention**: `aws-{architecture-name}-{timestamp}.drawio`
- **Fully editable**: Open in https://app.diagrams.net/
- **Standards-compliant**: AWS Well-Architected Framework
- **Professional**: Presentation-ready
- **Version control friendly**: Text-based XML

---

**Ready to generate your AWS architecture diagram? Let the orchestrator handle the complexity!**
