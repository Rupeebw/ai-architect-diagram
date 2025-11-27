# AWS Diagram Generation - Setup Guide for New Team Members

## Prerequisites

- macOS (Intel or Apple Silicon)
- Admin access to install software
- Terminal access
- Internet connection

---

## Step-by-Step Setup Instructions

### Step 1: Install Homebrew (if not already installed)

```bash
# Check if Homebrew is installed
which brew

# If not installed, run:
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Follow the "Next steps" instructions to add Homebrew to PATH
```

### Step 2: Install Claude Code

```bash
# Install Claude Code CLI
brew install --cask claude

# Verify installation
claude --version

# Login to Claude Code (requires Anthropic account)
claude auth login
# Follow the browser authentication flow
```

**Important**: You'll need an Anthropic account with Claude Code access. Sign up at https://claude.ai/

### Step 3: Clone the Project Repository

```bash
# Navigate to your projects directory
cd ~/Documents/Project/

# Clone the repository (replace with actual repo URL)
git clone <repository-url> schild

# Navigate to project directory
cd schild
```

### Step 4: Install AWS Diagram Tools

```bash
# Install awsdac (AWS Diagram-as-Code)
brew install awsdac

# Graphviz will be auto-installed as a dependency
# Verify installation
awsdac --version    # Should show: awsdac version 0.22.3
dot -V              # Should show: dot - graphviz version X.X.X
```

### Step 5: Verify Claude Code Agents

The project includes custom AI agents for diagram generation:

```bash
# Check if agents directory exists
ls -la .claude/agents/

# You should see these agents:
# - aws-diagram-orchestrator.md
# - aws-core-architecture-agent.md (aws-diagram-generator.md)
# - aws-storage-layer-agent.md
# - aws-observability-layer-agent.md
# - aws-security-services-agent.md

# Check slash commands
ls -la .claude/commands/

# You should see:
# - draw-aws-diagram.md
```

**If these files are missing**, you need to either:
1. Pull them from the repository, OR
2. Request them from your team lead

### Step 6: Verify Output Directory

```bash
# Check if diagrams directory exists
ls -la architecture/diagrams/

# If it doesn't exist, create it:
mkdir -p architecture/diagrams
```

### Step 7: Optional - Install Draw.io Desktop

For offline diagram editing:

```bash
# Install Draw.io desktop application
brew install --cask drawio

# Verify installation
open -a draw.io
```

---

## Quick Test - Generate Your First Diagram

### Test 1: Using Claude Code Multi-Agent System

```bash
# Open Claude Code in the project directory
cd ~/Documents/PProject/schild
claude

# In Claude Code, run:
/draw-aws-diagram "Simple 3-tier web app with VPC, EC2, and RDS"

# Expected output:
# - Diagram file created in architecture/diagrams/
# - File format: aws-{name}-{timestamp}.drawio
```

### Test 2: Using awsdac (Optional)

Create a simple test file:

```bash
# Create a test YAML file
cat > test-diagram.yaml << 'EOF'
Diagram:
  Resources:
    - Type: VPC
      Properties:
        Name: TestVPC
        CIDR: 10.0.0.0/16
    - Type: EC2
      Properties:
        Name: WebServer
EOF

# Generate diagram
awsdac test-diagram.yaml -o test-output.png

# Check if PNG was created
ls -lh test-output.png
```

---

## Troubleshooting Common Issues

### Issue 1: "command not found: claude"

**Solution**:
```bash
# Add Homebrew to PATH (for Apple Silicon Macs)
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
source ~/.zprofile

# For Intel Macs
echo 'eval "$(/usr/local/bin/brew shellenv)"' >> ~/.zprofile
source ~/.zprofile
```

### Issue 2: "awsdac: command not found"

**Solution**:
```bash
# Check if awsdac is installed
brew list | grep awsdac

# If not found, install it
brew install awsdac

# Check installation location
which awsdac
```

### Issue 3: Claude Code agents not working

**Solution**:
```bash
# Ensure you're in the project root directory
pwd  # Should show: /Users/<your-username>/Documents/PProject/schild

# Verify .claude directory exists
ls -la .claude/

# If missing, you need to pull from git or request from team
```

### Issue 4: Authentication errors with Claude Code

**Solution**:
```bash
# Re-authenticate
claude auth logout
claude auth login

# Follow the browser authentication flow again
```

### Issue 5: "Permission denied" errors

**Solution**:
```bash
# Fix directory permissions
chmod -R 755 architecture/diagrams/

# Or create directory if it doesn't exist
mkdir -p architecture/diagrams
```

---

## Verification Checklist

Before starting work, verify all components are ready:

```bash
# Run these commands and check for successful output:

✅ Homebrew installed:
   brew --version

✅ Claude Code installed:
   claude --version

✅ Claude Code authenticated:
   claude auth status

✅ awsdac installed:
   awsdac --version

✅ Graphviz installed:
   dot -V

✅ Project cloned:
   ls -la ~/Documents/PProject/schild/.claude/

✅ Agents available:
   ls -la .claude/agents/ | grep aws-

✅ Output directory exists:
   ls -la architecture/diagrams/

✅ Optional - Draw.io installed:
   open -a draw.io
```

---

## Repository Structure (What You Need)

```
root-directory/
├── .claude/
│   ├── agents/                          # AI agents (5 files)
│   │   ├── aws-diagram-orchestrator.md
│   │   ├── aws-diagram-generator.md     # Core architecture agent
│   │   ├── aws-storage-layer-agent.md
│   │   ├── aws-observability-layer-agent.md
│   │   └── aws-security-services-agent.md
│   └── commands/                        # Slash commands
│       └── draw-aws-diagram.md
├── architecture/
│   ├── diagrams/                        # Generated diagrams (output)
│   ├── demo/                            # Example architecture plans
│   └── Planning/                        # Documentation (this file)
└── [other project files]
```

---

## Next Steps After Setup

1. **Read the tech stack document**:
   ```
   cat architecture/Planning/Diagram-Generation-Tech-Stack.txt
   ```

2. **Try example diagrams**:
   ```bash
   # Generate from demo files
   /draw-aws-diagram architecture/demo/1-simple-3tier.txt
   ```

3. **Learn the workflow**:
   - Review existing diagrams in `architecture/diagrams/`
   - Check example architecture plans in `architecture/demo/`
   - Practice with simple architectures first

4. **Join team communication**:
   - Ask team lead for repository URL if not provided
   - Get access to project documentation
   - Request onboarding session if needed

---

## Required Accounts & Access

### 1. Anthropic Account (Required)
- **URL**: https://claude.ai/
- **Purpose**: Claude Code authentication
- **Cost**: Check current pricing at https://www.anthropic.com/pricing
- **Setup**: Sign up → Verify email → Login via `claude auth login`

### 2. GitHub/GitLab Account (Required)
- **Purpose**: Clone project repository
- **Setup**: Request repository access from team lead

### 3. AWS Account (Optional)
- **Purpose**: If using awsdac with actual CloudFormation templates
- **Setup**: Not required for diagram generation

---

## Estimated Setup Time

- **Minimal Setup** (awsdac only): 10 minutes
- **Full Setup** (Claude Code + awsdac): 20-30 minutes
- **Including testing**: 30-45 minutes

---

## Support & Resources

### Documentation
- **Tech Stack**: `architecture/Planning/Diagram-Generation-Tech-Stack.txt`
- **This Guide**: `architecture/Planning/Setup-Guide-For-New-Team-Members.txt`

### External Resources
- Claude Code Docs: https://docs.claude.com/claude-code
- awsdac GitHub: https://github.com/awslabs/diagram-as-code
- Draw.io: https://app.diagrams.net/

### Team Support
- Contact your team lead for:
  - Repository access
  - Claude Code subscription/access
  - Agent files (if missing from repo)
  - Onboarding session

---

## Summary: What You'll Have After Setup

✅ **Claude Code** - AI-powered diagram generation
✅ **awsdac** - YAML-based diagram tool
✅ **Graphviz** - Rendering engine
✅ **5 AI Agents** - Specialized AWS service agents
✅ **Project Repository** - All configuration files
✅ **Output Directory** - Ready for diagram generation
✅ **Draw.io** (optional) - Diagram editing tool

**You'll be able to**:
- Generate AWS architecture diagrams from natural language descriptions
- Create diagrams from YAML configurations
- Edit and customize diagrams in draw.io
- Version control diagrams (XML format)
- Export diagrams to PNG, PDF, SVG

---

**Welcome to the team! Happy diagramming! 🎨📊**
