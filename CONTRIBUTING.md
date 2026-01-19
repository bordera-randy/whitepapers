*# Contributing to Azure Whitepapers Repository

Thank you for your interest in contributing to the Azure Whitepapers repository! We welcome contributions from Azure experts, architects, engineers, and the broader cloud community.

## 📋 Table of Contents

- [Getting Started](#getting-started)
- [Contribution Guidelines](#contribution-guidelines)
- [Whitepaper Standards](#whitepaper-standards)
- [Technical Requirements](#technical-requirements)
- [Submission Process](#submission-process)
- [Review Process](#review-process)
- [Style Guide](#style-guide)
- [Resources](#resources)

## Getting Started

### Prerequisites

Before contributing, ensure you have:
- **Azure Expertise**: Deep knowledge of Azure services and implementation patterns
- **Technical Writing Skills**: Ability to explain complex concepts clearly
- **IaC Experience**: Proficiency with Terraform and Azure CLI
- **Markdown Proficiency**: Comfortable with Markdown formatting and GitHub workflows
- **Development Environment**: Git, VS Code (or preferred editor), Azure subscription for testing

### Before You Start

1. **Review Existing Content**: Browse [available whitepapers](README.md#available-whitepapers) to avoid duplication
2. **Check Open Issues**: Look for [requested topics](../../issues?q=is%3Aissue+is%3Aopen+label%3Awhitepaper-request) or propose a new one
3. **Study the Template**: Review the [whitepaper template](templates/) structure and requirements
4. **Identify Category**: Determine which category your whitepaper belongs to:
   - `architecture/` - Design patterns, frameworks, Well-Architected guidance
   - `compute/` - VMs, AKS, AVD, serverless, container services
   - `storage/` - Blob, Files, NetApp, Disk, Data Lake, databases
   - `networking/` - VNets, NSGs, Virtual WAN, load balancing, security
   - `security/` - Identity, compliance, encryption, Key Vault, Defender
   - `devops/` - CI/CD, monitoring, automation, observability

## Contribution Guidelines

### What We Accept ✅

- **Enterprise-Grade Technical Documentation**: In-depth coverage of Azure services with production implementation guidance
- **Architecture Patterns**: Solutions architecture designs with decision trees and trade-off analysis
- **Implementation Guides**: Step-by-step deployment instructions with working IaC code
- **Best Practices**: Proven patterns validated in production environments
- **Security & Compliance**: Hardening guides, compliance frameworks, zero-trust implementations
- **Migration Strategies**: On-premises to Azure migration methodologies with tooling guidance
- **Performance Optimization**: Tuning guides with benchmarking and monitoring strategies
- **Cost Optimization**: TCO analysis, resource sizing, and cost management patterns

### What We Don't Accept ❌

- **Marketing Content**: Sales pitches, feature announcements, promotional material
- **Third-Party Product Promotion**: Content primarily promoting non-Microsoft products
- **Duplicate Content**: Topics already thoroughly covered in existing whitepapers
- **Outdated Information**: Content based on deprecated services or old API versions
- **Incomplete Submissions**: Missing required sections, untested code, or broken links
- **Non-Azure Cloud Content**: AWS, GCP, or other cloud providers (unless for migration context)
- **Surface-Level Overviews**: Content that merely summarizes Microsoft documentation without adding value

### Content Scope and Quality Standards

#### Target Audience
- **Primary**: Cloud architects, DevOps engineers, security professionals, platform engineers
- **Secondary**: Technical decision-makers, IT leadership evaluating Azure solutions
- **Depth Level**: Intermediate to advanced technical content with implementation focus

#### Cloud Environment
- **Focus**: Azure Commercial cloud only
- **Exclusions**: Azure Government, Azure China, Azure Stack (unless explicitly scoped)

#### Value Proposition
Your whitepaper should provide:
- **Actionable Guidance**: Readers can implement solutions based on your documentation
- **Production-Ready Code**: All IaC and scripts tested in real environments
- **Decision Frameworks**: Help readers make informed architectural choices
- **Real-World Context**: Address practical challenges and limitations
- **Implementation Patterns**: Repeatable solutions for common scenarios

## Whitepaper Standards

### Technical Requirements

- **Accuracy:** All information must be technically accurate and up-to-date
- **Completeness:** Cover the topic comprehensively within the defined scope
- **Clarity:** Use clear, concise language appropriate for the target audience
- **Practical Value:** Include actionable guidance and real-world examples

### Format Requirements

- Use the provided [whitepaper template](templates/whitepaper-template.md)
- Include code examples where appropriate
- Provide architecture diagrams (ASCII art, images, or links to diagrams)
- Include references to official Microsoft documentation
- Follow consistent formatting and style

### Content Guidelines

1. **Executive Summary:** 2-3 paragraphs summarizing the content and value
## Whitepaper Standards

### Document Structure (Required)

All whitepapers must follow this standardized structure:

#### 1. Metadata Header
## Technical Requirements

### Mandatory Components

#### 1. Terraform Infrastructure as Code
```hcl
# Example structure - all whitepapers must include working Terraform
terraform {
  required_version = ">= 1.5.0"
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~> 3.0"
    }
  }
  backend "azurerm" {} # State management configuration
}

provider "azurerm" {
  features {}
}

# Resource definitions with variables, outputs, and comments
```

**Requirements:**
- Complete, deployable configurations
- Variables for parameterization
- Outputs for important resource IDs and endpoints
- Comments explaining key decisions
- Backend configuration for state management
- Follows Azure naming conventions

#### 2. Mermaid Diagrams
```mermaid  
## Review Process

### Review Stages

#### Stage 1: Automated Checks (Immediate)
- Markdown linting and formatting validation
- Link checker for broken references
- File structure and naming conventions
- Spell check and basic grammar

#### Stage 2: Initial Maintainer Review (3-5 business days)
Maintainers verify:
- ✅ Follows whitepaper template structure
- ✅ All required sections present
- ✅ Appropriate category placement
- ✅ No duplicate content
- ✅ Metadata header complete
- ✅ Table of contents functional

**Outcome**: Approved for technical review, or returned with feedback

#### Stage 3: Technical Subject Matter Expert Review (5-10 business days)
Azure experts evaluate:
- ✅ Technical accuracy of all content
- ✅ Terraform code quality and best practices
- ✅ Azure CLI commands tested and current
- ✅ Security practices aligned with Microsoft recommendations
- ✅ Architecture patterns follow Well-Architected Framework
- ✅ KQL queries syntactically correct and useful
- ✅ Real-world applicability and practical value

**Outcome**: Approved for final review, or technical corrections requested

## Style Guide

### Writing Style Standards

#### Tone and Voice
- **Professional**: Authoritative technical content without marketing language
- **Active Voice**: "Deploy the solution" not "The solution should be deployed"
- **Present Tense**: "Azure provides" not "Azure will provide"
- **Direct Address**: "You can configure" when providing instructions
- **Technical Depth**: Assume intermediate Azure knowledge; explain advanced concepts

#### Language Guidelines
```markdown
✅ GOOD: "Configure private endpoints to secure storage account access"
❌ AVOID: "You should probably think about maybe using private endpoints"

✅ GOOD: "Azure Files supports SMB 3.0 and NFS 4.1 protocols"
❌ AVOID: "Azure Files is the best file sharing solution available"

✅ GOOD: "This architecture provides 99.99% SLA for production workloads"
❌ AVOID: "This amazing architecture delivers incredible uptime"
```

### Markdown Formatting Standards

#### Document Structure
```markdown
# Whitepaper Title (H1 - Only once at top)

## Major Section (H2 - Main sections)

### Subsection (H3 - Detailed topics)

#### Minor Point (H4 - Specific details)

##### Rarely Used (H5 - Only when deeper hierarchy needed)
```

#### Code Blocks with Language Identifiers
```terraform
# Terraform examples
resource "azurerm_resource_group" "example" {
  name     = "rg-production-eastus2"
  location = "eastus2"
}
```

```bash
# Azure CLI commands
az group create --name rg-production-eastus2 --location eastus2
```
## Resources

### Official Microsoft Documentation

#### Core Azure Resources
- **[Azure Documentation](https://learn.microsoft.com/azure/)** - Primary Azure documentation
- **[Azure Architecture Center](https://learn.microsoft.com/azure/architecture/)** - Architecture patterns and best practices
- **[Well-Architected Framework](https://learn.microsoft.com/azure/well-architected/)** - Design principles and pillars
- **[Cloud Adoption Framework](https://learn.microsoft.com/azure/cloud-adoption-framework/)** - Enterprise cloud adoption guidance
- **[Microsoft Learn](https://learn.microsoft.com/training/)** - Interactive learning paths and modules

#### Infrastructure as Code
- **[Terraform Azure Provider](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)** - Terraform AzureRM provider documentation
- **[Azure CLI Reference](https://learn.microsoft.com/cli/azure/)** - Complete CLI command reference
- **[Azure PowerShell](https://learn.microsoft.com/powershell/azure/)** - PowerShell Az module documentation
- **[Bicep Documentation](https://learn.microsoft.com/azure/azure-resource-manager/bicep/)** - Azure Bicep language reference

#### Monitoring and Operations
- **[Azure Monitor](https://learn.microsoft.com/azure/azure-monitor/)** - Monitoring and observability platform
- **[KQL Language Reference](https://learn.microsoft.com/azure/data-explorer/kusto/query/)** - Kusto Query Language documentation
- **[Log Analytics](https://learn.microsoft.com/azure/azure-monitor/logs/log-analytics-overview)** - Log query and analysis

### Development Tools

#### Required Tools
- **[Git](https://git-scm.com/)** - Version control system
- **[Visual Studio Code](https://code.visualstudio.com/)** - Recommended editor with Azure extensions
- **[Azure CLI](https://learn.microsoft.com/cli/azure/install-azure-cli)** - Command-line interface for Azure
- **[Terraform](https://www.terraform.io/downloads)** - Infrastructure as Code tool

#### Recommended VS Code Extensions
- **Azure Account** - Azure subscription management
- **Azure Terraform** - Terraform language support
- **Markdown All in One** - Markdown editing and preview
- **Mermaid Markdown Syntax** - Mermaid diagram support
- **markdownlint** - Markdown linting and style checking
- **Azure CLI Tools** - Azure CLI IntelliSense

### Diagram and Visualization Tools

- **[Mermaid Live Editor](https://mermaid.live/)** - Create and preview Mermaid diagrams
- **[Mermaid Documentation](https://mermaid.js.org/)** - Complete Mermaid syntax reference
- **[Excalidraw](https://excalidraw.com/)** - Hand-drawn style diagrams (export to include in docs)
- **[Draw.io / diagrams.net](https://app.diagrams.io/)** - Professional diagram creation

### Style and Writing References

- **[Microsoft Writing Style Guide](https://learn.microsoft.com/style-guide/)** - Official Microsoft writing standards
- **[Azure Naming Conventions](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming)** - Resource naming standards
- **[Azure Tagging Strategy](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/resource-tagging)** - Resource tagging best practices
- **[Markdown Guide](https://www.markdownguide.org/)** - Comprehensive Markdown reference
- **[GitHub Flavored Markdown](https://github.github.com/gfm/)** - GitHub Markdown specification

### Testing and Validation

- **[Terraform Validate](https://www.terraform.io/cli/commands/validate)** - Validate Terraform configuration
- **[terraform-docs](https://terraform-docs.io/)** - Generate documentation from Terraform
- **[TFLint](https://github.com/terraform-linters/tflint)** - Terraform linter
- **[Azure Resource Graph Explorer](https://portal.azure.com/#blade/HubsExtension/ArgQueryBlade)** - Query Azure resources with KQL
- **[ARM Template Test Toolkit](https://learn.microsoft.com/azure/azure-resource-manager/templates/test-toolkit)** - Validate ARM templates

### Community and Support

#### Getting Help
- **[GitHub Issues](../../issues)** - Report bugs, request features, ask questions
- **[GitHub Discussions](../../discussions)** - Community discussions and collaboration
- **[Microsoft Q&A](https://learn.microsoft.com/answers/topics/azure.html)** - Official Azure Q&A forum

#### Contributing Tips
- Browse existing whitepapers to understand style and depth
- Start with smaller contributions before tackling large topics
- Ask questions early if uncertain about approach or scope
- Collaborate with reviewers; feedback improves quality
- Test all code examples in real Azure subscriptions
- Keep content updated as Azure services evolve

## Questions or Help Needed?

### Before Asking
1. **Search existing issues** for similar questions or topics
2. **Review this guide** thoroughly for answers to common questions
3. **Check existing whitepapers** for examples of quality and style

### How to Get Help

#### For Questions About Contributing
Create a [GitHub Discussion](../../discussions) with:
- Clear description of your question
- What you've already tried or researched
- Specific areas where you need guidance

#### For Technical Review Assistance
Create a [GitHub Issue](../../issues/new) with:
- **Label**: `help wanted` or `question`
- **Topic**: Specific service or technology area
- **Context**: What you're trying to accomplish
- **Specific Questions**: Concrete questions about implementation

#### For Whitepaper Proposals
Create a [GitHub Issue](../../issues/new) with:
- **Label**: `whitepaper-request`
- **Title**: Proposed whitepaper topic
- **Description**: Scope, audience, key sections
- **Value Proposition**: Why this whitepaper is needed

---

## Thank You!

Thank you for contributing to the Azure Whitepapers repository and helping build a comprehensive knowledge base for the Azure community. Your expertise and effort help engineers and architects worldwide implement better Azure solutions.

**Questions?** Open an issue or discussion - we're here to help!

*Last Updated: January 19, 2026* for docs

✅ GOOD: For more details, see the [Well-Architected Framework](link)
❌ AVOID: More info can be found here: https://long-url-pasted-directly
```

#### Lists and Bullets
```markdown
**Unordered lists:**
- Use for non-sequential items
- Maintain consistent indentation
- Keep items parallel in structure

**Ordered lists:**
1. Use for sequential steps
2. Number sequentially
3. Use for procedures and processes

**Nested lists:**
- Parent item
  - Child item (2 spaces indent)
    - Nested child (4 spaces indent)
```

### Technical Content Standards

#### Terraform Code Style
```hcl
# Follow HashiCorp style guide
resource "azurerm_storage_account" "example" {
  name                     = "stprodeastus2001"
  resource_group_name      = azurerm_resource_group.example.name
  location                 = azurerm_resource_group.example.location
  account_tier             = "Standard"
  account_replication_type = "GRS"
  
  # Enable security features
  enable_https_traffic_only = true
  min_tls_version          = "TLS1_2"
  
  network_rules {
    default_action = "Deny"
    ip_rules       = var.allowed_ip_ranges
  }
  
  tags = {
    Environment = "Production"
    ManagedBy   = "Terraform"
  }
}
```

**Standards:**
- Use descriptive resource names
- Include inline comments for complex logic
- Group related arguments together
- Always specify security-related settings
- Use variables for reusable values
- Include tags for resource management

#### Azure CLI Style
```bash
#!/bin/bash
# Azure CLI script standards

# Set error handling
set -e

# Define variables
RESOURCE_GROUP="rg-production-eastus2"
LOCATION="eastus2"
STORAGE_ACCOUNT="stprodeastus2001"

# Create resource group
az group create \
  --name "$RESOURCE_GROUP" \
  --location "$LOCATION" \
  --tags Environment=Production ManagedBy=AzureCLI

# Create storage account with security settings
az storage account create \
  --name "$STORAGE_ACCOUNT" \
  --resource-group "$RESOURCE_GROUP" \
  --location "$LOCATION" \
  --sku Standard_GRS \
  --kind StorageV2 \
  --https-only true \
  --min-tls-version TLS1_2 \
  --allow-blob-public-access false
```

**Standards:**
- Use bash shebang and error handling
- Define variables at top of script
- Use line continuations for readability
- Include comments explaining intent
- Use quotes around variables
- Enable security features explicitly

#### KQL Query Style
```kusto
// Azure Monitor Log Analytics query
// Purpose: Identify storage account throttling events

AzureMetrics
| where ResourceProvider == "MICROSOFT.STORAGE"
| where MetricName == "Throttling"
| where TimeGenerated >= ago(24h)
| summarize 
    ThrottleCount = count(),
    AvgThrottle = avg(Total)
    by bin(TimeGenerated, 1h), ResourceId
| where ThrottleCount > 10
| order by TimeGenerated desc
| project 
    TimeGenerated,
    ResourceId,
    ThrottleCount,
    AvgThrottle
```

**Standards:**
- Include purpose comment at top
- Use proper indentation for readability
- Name aggregated columns clearly
- Filter early to optimize performance
- Use meaningful variable names
- Add time range filters

### Azure Naming Conventions

Follow [Microsoft CAF naming standards](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming):

```
Resource Type Prefix Examples:
- rg-         Resource groups (rg-production-eastus2)
- vnet-       Virtual networks (vnet-hub-eastus2)
- snet-       Subnets (snet-web-tier)
- nsg-        Network security groups (nsg-web-tier)
- st          Storage accounts (stprodeastus2001)
- kv-         Key vaults (kv-prod-eastus2)
- aks-        AKS clusters (aks-production-eastus2)
- vm-         Virtual machines (vm-web-01)
```
### Visual and Documentation Standards

- **Mermaid diagrams** for all architecture visualizations
- **Code syntax highlighting** with appropriate language identifiers
- **Tables** for feature comparisons, sizing guides, and configurations
- **Markdown formatting** following GitHub Flavored Markdown (GFM)
- **Relative links** for internal repository references
- **Absolute links** for external Microsoft documentation

## Submission Process

### Step 1: Setup Development Environment

```bash
# Fork and clone the repository
git clone https://github.com/YOUR-USERNAME/whitepapers.git
cd whitepapers

# Create a feature branch
git checkout -b feature/storage-security-compliance

# Create your whitepaper in the appropriate category folder
code storage/azure-storage-security-compliance.md
```

### Step 2: Write Your Whitepaper

1. **Copy the Template**: Use `templates/whitepaper-template.md` as your starting point
2. **Follow Structure**: Include all 12 required core sections
3. **Write Terraform Code**: Create complete, tested IaC examples
4. **Create Diagrams**: Add Mermaid diagrams for architecture visualization
5. **Add KQL Queries**: Include monitoring and diagnostic queries
6. **Document Operations**: Provide Azure CLI commands for common tasks
7. **Link References**: Add links to official Microsoft documentation

### Step 3: Test Your Code

```bash
# Validate Terraform
cd terraform-examples/
terraform init
terraform validate
terraform fmt -check

# Test Azure CLI commands (in a non-production subscription)
az login
# Run each command and verify output

# Validate Mermaid diagrams
# Use: https://mermaid.live/ for preview and validation
```

### Step 4: Quality Assurance Checklist

Before submitting, verify:

**Content Quality:**
- [ ] All 12 core sections completed
- [ ] Executive summary clearly articulates value
- [ ] Table of contents with working anchor links
- [ ] Technical depth appropriate for target audience
- [ ] No marketing language or sales pitches

**Code Quality:**
- [ ] Terraform code validates without errors
- [ ] Azure CLI commands tested and verified
- [ ] KQL queries return expected results
- [ ] All code includes inline comments
- [ ] Variables used instead of hardcoded values

**Security Standards:**
- [ ] Private endpoints used where applicable
- [ ] Managed identities over service principals
- [ ] Key Vault for secrets management
- [ ] Network security groups properly configured
- [ ] RBAC with least privilege principle

**Visual Elements:**
- [ ] Mermaid diagrams render correctly
- [ ] Architecture diagrams show all key components
- [ ] Tables formatted properly
- [ ] Code blocks use correct syntax highlighting

**References:**
- [ ] All external links verified and active
- [ ] Microsoft documentation links current
- [ ] Internal relative links work correctly
- [ ] No broken images or diagrams

**Formatting:**
- [ ] Spell check completed
- [ ] Grammar check completed
- [ ] Consistent heading hierarchy
- [ ] Proper Markdown formatting

### Step 5: Submit Pull Request

```bash
# Stage and commit your changes
git add storage/azure-storage-security-compliance.md
git commit -m "Add Azure Storage Security and Compliance whitepaper"

# Push to your fork
git push origin feature/storage-security-compliance
```

1. **Create PR**: Open a pull request against the `main` branch
2. **Complete Template**: Fill out all sections of the PR template
3. **Add Labels**: Apply relevant category and status labels
4. **Link Issues**: Reference any related issue numbers
5. **Request Review**: Tag maintainers for review
6. **Describe Changes**: Provide clear summary of what the whitepaper coversI commands)

#### 5. Infrastructure as Code
- **Terraform Examples** (mandatory): Complete, tested, production-ready configurations
- **Azure CLI Commands**: Operational tasks, deployment, management
- **ARM/Bicep Templates**: Alternative IaC options where appropriate

#### 6. References and Appendices
- Microsoft Learn documentation links
- Architecture Center references
- Troubleshooting guides
- Configuration checklists
- Additional resources

### Content Quality Requirements

#### Technical Accuracy
- ✅ All commands tested against latest Azure CLI/PowerShell versions
- ✅ Terraform code validated with `terraform validate` and `terraform plan`
- ✅ Azure service features verified as Generally Available (GA)
- ✅ API versions current and supported
- ✅ Links verified and pointing to active Microsoft documentation

#### Code Standards
- All code must be production-ready, not proof-of-concept
- Include error handling and validation
- Add inline comments explaining complex logic
- Follow Azure naming conventions and tagging standards
- Use variables and parameterization, avoid hardcoded values
- Include backend configuration for Terraform state management

#### Security Integration
- Security practices embedded throughout (not a separate section)
- Principle of least privilege in RBAC examples
- Network isolation with private endpoints where applicable
- Encryption at rest and in transit configurations
- Secrets management with Key Vault integration
- Identity-based authentication over keys/secrets

#### Practical Value
- Real-world scenarios and use cases
- Decision frameworks with trade-off analysis
- Troubleshooting common issues
- Performance benchmarking data
- Cost estimation examples
- Migration considerations from on-premises or other platforms
Before submitting:
- [ ] Spell check and grammar check
- [ ] Verify all Azure CLI commands and PowerShell scripts
- [ ] Test any deployment templates or configuration files
- [ ] Ensure architecture diagrams are clear and accurate
- [ ] Validate all external links
- [ ] Review against the style guide

### Step 4: Submit Pull Request

1. Commit your changes with descriptive commit messages
2. Push your branch to your fork
3. Create a pull request against the main repository
4. Fill out the pull request template completely
5. Request review from repository maintainers

## Review Process

### Initial Review

- Repository maintainers will review for:
  - Adherence to template and style guidelines
  - Technical accuracy (preliminary check)
  - Appropriate categorization
  - Completeness of required sections

### Technical Review

- Subject matter experts will review for:
  - Technical accuracy and best practices
  - Practical applicability
  - Security considerations
  - Performance implications

### Final Review

- Final editorial review for:
  - Clarity and readability
  - Consistency with other whitepapers
  - Proper formatting and style
  - Complete references and links

### Timeline

- Initial review: 3-5 business days
- Technical review: 5-10 business days
- Final review: 2-3 business days
- Total process: 10-18 business days

## Style Guide

### Writing Style

- **Tone:** Professional, informative, and authoritative
- **Voice:** Active voice preferred over passive voice
- **Tense:** Present tense for current capabilities, future tense for planned features
- **Audience:** Assume technical background but explain complex concepts

### Formatting Standards

#### Headers
```markdown
# H1 - Document Title
## H2 - Major Sections
### H3 - Subsections
#### H4 - Minor Subsections
```

#### Code Blocks
```bash
# Use appropriate language identifiers
az group create --name myResourceGroup --location eastus
```

#### Tables
| Service | Use Case | Cost Model |
|---------|----------|------------|
| Azure VMs | Compute workloads | Pay-per-hour |

#### Links
- Use descriptive link text: [Azure Documentation](https://docs.microsoft.com/azure/)
- Avoid "click here" or generic text

### Technical Standards

#### Azure CLI Examples
- Use latest Azure CLI syntax
- Include resource group and location parameters
- Show expected output where helpful

#### PowerShell Examples
- Use Azure PowerShell Az module
- Include error handling where appropriate
- Follow PowerShell best practices

#### ARM Templates/Bicep
- Use latest template schema
- Include parameter descriptions
- Follow Azure Resource Manager best practices

## Resources

### Microsoft Documentation
- [Azure Documentation](https://docs.microsoft.com/azure/)
- [Azure Architecture Center](https://docs.microsoft.com/azure/architecture/)
- [Microsoft Learn](https://docs.microsoft.com/learn/)

### Tools
- [Azure CLI](https://docs.microsoft.com/cli/azure/)
- [Azure PowerShell](https://docs.microsoft.com/powershell/azure/)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Draw.io](https://draw.io/) for diagrams

### Style References
- [Microsoft Writing Style Guide](https://docs.microsoft.com/style-guide/)
- [Azure naming conventions](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/naming-and-tagging)

## Questions or Help Needed?

If you have questions about contributing or need help with your whitepaper:

1. Check existing issues for similar questions
2. Create a new issue with the "question" label
3. Provide as much detail as possible about your question or challenge

Thank you for contributing to the Azure community knowledge base!*