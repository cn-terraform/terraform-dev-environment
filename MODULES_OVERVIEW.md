# Module inventory

This is a snapshot of the 20 submodules configured in `.gitmodules` and checked out when this catalog was prepared. Module directories are independent repositories, not Terraform child modules in a shared root. A module's README and code are authoritative; descriptions below are short orientation hints.

## Modules

| Area | Module | What it provides |
|---|---|---|
| Foundation | `terraform-aws-networking` | AWS base networking, including subnet configurations |
| Compute | `terraform-aws-ec2-asg` | EC2 Auto Scaling Group |
| Compute | `terraform-aws-nomad` | Nomad servers and clients on AWS |
| Containers | `terraform-aws-ecs-cluster` | ECS cluster |
| Containers | `terraform-aws-ecs-fargate` | Composite ECS Fargate deployment |
| Containers | `terraform-aws-ecs-fargate-service` | ECS Fargate service composition |
| Containers | `terraform-aws-ecs-fargate-task-definition` | ECS task definition |
| Containers | `terraform-aws-ecs-fargate-scheduled-task` | Scheduled ECS Fargate task |
| Containers | `terraform-aws-ecs-service-autoscaling` | ECS service autoscaling |
| Containers | `terraform-aws-ecs-alb` | Application Load Balancer configuration for ECS use |
| Storage / logging | `terraform-aws-logs-s3-bucket` | S3 bucket for logs |
| Storage / web | `terraform-aws-s3-static-website` | Static website hosting on S3 |
| Observability | `terraform-aws-cloudwatch-logs` | CloudWatch Logs resources |
| Observability | `terraform-aws-flow-log` | AWS flow logging (README still contains placeholder text) |
| Delivery | `terraform-aws-ci-cd-system` | CI/CD system composed around ECS Fargate |
| Delivery | `terraform-aws-jenkins` | Jenkins on AWS |
| Delivery | `terraform-aws-nexus` | Sonatype Nexus on AWS |
| Delivery | `terraform-aws-sonarqube` | SonarQube on AWS |
| DNS | `terraform-aws-route53` | Route 53 resources |
| Starter | `terraform-module-template` | Template for new Terraform modules (README still contains placeholder text) |

## Internal Terraform module references observed in source

These are registry/module `source` references in the checked-out Terraform files, not Git submodule relationships. Recheck source files when relying on this snapshot.

| Consumer | Internal module sources |
|---|---|
| `terraform-aws-ci-cd-system` | `networking`, `jenkins`, `sonarqube`, `nexus` |
| `terraform-aws-ecs-alb` | `logs-s3-bucket` |
| `terraform-aws-ecs-fargate` | `ecs-cluster`, `ecs-fargate-task-definition`, `ecs-fargate-service` |
| `terraform-aws-ecs-fargate-service` | `ecs-alb`, `ecs-service-autoscaling` |
| `terraform-aws-jenkins` | `cloudwatch-logs`, `ecs-cluster`, `ecs-fargate-task-definition`, `ecs-fargate-service` |
| `terraform-aws-nexus` | `cloudwatch-logs`, `ecs-fargate` |
| `terraform-aws-s3-static-website` | `logs-s3-bucket` |
| `terraform-aws-sonarqube` | `cloudwatch-logs`, `ecs-fargate` |

Other module sources observed include `terraform-aws-modules/acm/aws` and `cloudposse/ecs-container-definition/aws`. Providers (such as `hashicorp/aws`, `hashicorp/null`, or `hashicorp/random`) are separate from module sources. For complete constraints and references inspect each module's `versions.tf` and source files.

## Repository observations

- All 20 entries in `.gitmodules` were initialized in the inspected checkout. The root repository pins their commits; reported `main` branches and tags describe that checkout only and are not guaranteed to remain current.
- Modules generally have `main.tf`, `variables.tf`, `outputs.tf`, `versions.tf`, a README, a pre-commit configuration, and GitHub Actions workflow, but this is not uniform. Examples and CI validation scope also vary.
- Module READMEs include generated Terraform docs in several repositories, but documentation quality is uneven. `terraform-aws-flow-log` has a misspelled generic title, placeholder `Complete` sections, and an empty `main.tf`; its `examples/test` directory appears to exercise SonarQube, so confirm module intent before using it. `terraform-module-template` also has placeholder README sections. `terraform-aws-logs-s3-bucket` has placeholder prose despite containing S3 resource implementation. Treat these as module-repository documentation/implementation gaps; they were not changed from the umbrella repository.
- Composite modules such as `terraform-aws-ci-cd-system` and `terraform-aws-ecs-fargate` show `No resources` in generated README tables because they compose child modules. Check module references and child behavior rather than interpreting that table as absence of infrastructure.
- Version constraints and hook versions vary substantially across modules. Follow the target module's own compatibility contract rather than applying one umbrella-wide version assumption.
