# Legacy VarSeq Project Workflows

This repository contains VarSeq pipeline tasks for managing legacy cohort projects and adding samples to existing variant frequency analyses.

## Prerequisites

- Project template files (.vsproject format)
  - Default templates are provided: `Legacy_Frequency_Cohort_Template_GRCh37.vsproject-template` and `Legacy_Frequency_Cohort_Template_GRCh38.vsproject-template`
- Sample vcf files for import
- Appropriate read/write permissions

## Tasks

The repository contains the following tasks:

### Create Cohort (`create_settings.task.yaml`)

Creates initial settings for a VarSeq cohort project.

Parameters:
- `project_name`: The name of the cohort to create
- `project_template`: The project template file path for new projects
- `project_base_path`: The base path where the project will be created and stored

### Add Samples to Cohort (`update_project.task.yaml`)

Updates an existing VarSeq cohort project by adding new sample files.

Parameters:
- `project_base_path`: The base path where the project will be created and stored
- `project_name`: The base name for the new project (timestamp will be appended)
- `files_to_add`: Directory containing the files to be added to the cohort
- `project_template`: The project template file path for new projects

## Workflows

### Add Samples to Cohort Variant Frequencies (`legacy_project_cohort.workflow.yaml`)

This workflow adds new samples to an existing legacy VarSeq cohort project.

Process Overview:
1. Automatically finds the most recent project version using file timestamps
2. Creates a new timestamped project directory to ensure uniqueness
3. Imports new files into the project
4. Downloads required sources
5. Executes saved exports
6. Handles both updating existing projects and creating new ones from templates

## Usage

1. Create initial cohort settings:
   - Run the Create Cohort task to set up project parameters
   - Specify project name, template file (use provided default templates or your own), and base path

2. Add samples to an existing cohort:
   - Use the "Add Samples to Cohort Variant Frequencies" workflow
   - Select the directory containing your new sample files
   - The workflow will automatically handle project versioning

## Output

- A `project_params.txt` file containing project configuration
- New timestamped project directories
- Updated VarSeq project files with imported samples
- Exported analysis results

## Notes

- The workflow requires significant resources (8 CPU cores, 16GB memory)
- Projects are automatically timestamped to prevent naming conflicts
- The system handles both creating new projects from templates and updating existing ones
- Error handling includes continuing on errors during task execution
- All VarSeq pipeline operations are logged for debugging and monitoring
