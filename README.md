# OCT Project Template v1.0

This repository is the standard starting point for OCT projects.

The template provides a common repository structure and integrates shared
GitHub Actions workflows maintained in:

```text
Ulvea-OCT/workflows
```

The template is intentionally lightweight. Shared workflow implementation and
technical documentation are maintained centrally in the workflow repository.

## Repository Structure

```text
.
├── .github/
│   └── workflows/
├── docs/
├── roadmaps/
└── README.md
```

- `.github/workflows/` contains the workflows enabled by the template.
- `docs/` contains project/template-specific documentation.
- `roadmaps/` contains roadmap files only.
- `README.md` provides the general entry point for the template.

## OCT Workflows

This template consumes reusable workflows from:

```text
Ulvea-OCT/workflows
```

### Workflow versions used by this template

| Workflow | Version | Purpose |
|---|---:|---|
| Roadmap to GitHub Project | v1.0 | Parse, validate, schedule and optionally apply project roadmaps |

The version shown above is the version intended for the `template-repo-v1.0`
baseline.

Technical implementation details belong to the
`Ulvea-OCT/workflows` repository rather than being duplicated here.

## Roadmap to GitHub Project

The template includes the caller for the Roadmap to GitHub Project workflow.

The reusable workflow is referenced using:

```yaml
uses: Ulvea-OCT/workflows/.github/workflows/roadmap-to-project.yml@v1.0
```

The caller workflow is normally:

```text
.github/workflows/roadmap-to-project.yml
```

The workflow processes roadmap files stored under:

```text
roadmaps/
```

## Roadmaps

The `roadmaps/` directory is reserved exclusively for roadmap files.

A typical project contains:

```text
roadmaps/
└── <project>-roadmap.md
```

The roadmap format must match the schema expected by the referenced workflow
version.

For technical details about roadmap parsing, scheduling, secrets, permissions,
dry-run behaviour, and apply behaviour, refer to the documentation in the
`Ulvea-OCT/workflows` repository.

## Getting Started

When creating a project from this template:

1. Create the repository from `template-repo-v1.0`.
2. Review the workflows under `.github/workflows/`.
3. Add the project roadmap under `roadmaps/`.
4. Configure the required GitHub Organization Secrets.
5. Run the available workflow in dry-run mode where supported.
6. Review the result.
7. Enable operations that modify GitHub after validation succeeds.

## Workflow Configuration

The template contains the **caller configuration** for shared workflows.

The shared workflow implementation is not copied into the project repository.

This means that a project repository typically contains:

```text
.github/workflows/
└── roadmap-to-project.yml
```

while the implementation is maintained centrally in:

```text
Ulvea-OCT/workflows
```

This separation allows the workflow implementation to be maintained once and
consumed by multiple projects.

## Updating a Workflow Version

Workflow versions are updated explicitly in the caller workflow.

For example, moving from:

```yaml
uses: Ulvea-OCT/workflows/.github/workflows/roadmap-to-project.yml@v1.0
```

to:

```yaml
uses: Ulvea-OCT/workflows/.github/workflows/roadmap-to-project.yml@v1.1
```

changes the version consumed by the project.

The project should be tested after changing the workflow version.

The template itself should only change its baseline version when a new template
release is intentionally created.

## Adding Another Workflow

When a new shared workflow becomes part of the standard OCT template:

1. add its caller under `.github/workflows/`;
2. reference an explicit version from `Ulvea-OCT/workflows`;
3. add the workflow and version to the table in this README;
4. document any project-specific configuration in `docs/`.

Example:

```text
.github/workflows/
├── roadmap-to-project.yml
└── release.yml
```

with:

```yaml
uses: Ulvea-OCT/workflows/.github/workflows/release.yml@v1.0
```

## Documentation Responsibilities

Documentation is intentionally split between the two repositories.

### `template-repo-v1.0`

Documents:

- the purpose of the template;
- repository structure;
- workflows enabled by the template;
- workflow versions used by the template;
- project-specific configuration;
- getting started instructions.

### `Ulvea-OCT/workflows`

Documents:

- workflow implementation;
- reusable workflow inputs and outputs;
- composite actions;
- permissions;
- secrets;
- parsing and scheduling behaviour;
- technical troubleshooting;
- workflow development and release procedures.

This prevents technical workflow documentation from being duplicated across
every repository created from the template.
