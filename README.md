# FHIR IG Development Tools

A collection of shell utilities for working with FHIR Implementation Guides (IGs), specifically designed for HL7 Australia projects.

## Tools Overview

### Core FHIR Tools

#### `getPub`
Downloads the latest FHIR IG Publisher and creates soft links in input-cache folders of IGs.
```bash
./getPub [directory]
```
- **Default directory**: `~/Development/hl7au`
- **Function**: Downloads publisher.jar to a central location and creates symbolic links in each IG's input-cache folder
- **Benefits**: Saves disk space and ensures all IGs use the same publisher version

#### `getValidator`
Downloads the latest FHIR Validator for validation tasks.
```bash
./getValidator [directory]
```
- **Default directory**: `~/jar`
- **Function**: Downloads the FHIR validator for local validation

#### `igdiff`
Compares two versions of FHIR IG pages using an online diff service.
```bash
./igdiff <old_url> <new_url>
```
- **Function**: URL-encodes the inputs and generates an HTML diff using htmldiff.pl service
- **Output**: Creates an HTML file in `~/temp/` with the differences highlighted

### GitHub Integration

#### `draftIssue`
Creates draft GitHub issues for HL7 Australia FHIR IG projects.
```bash
./draftIssue <project_id> "<title>" "<body>"
```
- **Project IDs**:
  - 10 = eRequesting
  - 24 = AU Core
  - 20 = AU PS B for C
  - 25 = AU PS B for WS
- **Requirements**: GitHub CLI (`gh`) must be installed and authenticated

### File Management

#### `copyIG`
Efficiently copies IG directories while excluding build artifacts.
```bash
./copyIG <source_directory> <destination_directory>
```
- **Function**: Uses rsync to copy IGs while excluding common build artifacts and temporary files

### Search Tools

#### `pyfind`
Searches through Python scripts while ignoring common library folders.
```bash
./pyfind <search_term>
```
- **Function**: Shallow search through Python files, excluding standard library locations

#### `search-loinc`
Tool for searching LOINC terminology (details to be documented).

#### `valTests`
Validation test utilities (details to be documented).

## Prerequisites

### Required Tools
- **Bash/Shell**: All scripts require bash or sh
- **curl**: For downloading files (getPub, getValidator)
- **Python 3**: For URL encoding (igdiff)
- **Java**: For running FHIR tools (getPub, getValidator)
- **GitHub CLI**: For issue creation (draftIssue)
- **rsync**: For file copying (copyIG)

### Installation
1. Clone this repository
2. Make scripts executable:
   ```bash
   chmod +x getPub getValidator igdiff draftIssue copyIG pyfind search-loinc valTests
   ```
3. Add to your PATH or create symlinks in your `~/bin` directory

## Directory Structure

These tools expect a typical FHIR IG development structure:
```
~/Development/hl7au/
├── ig-project-1/
│   └── input-cache/
├── ig-project-2/
│   └── input-cache/
└── publisher/
    └── publisher.jar
```

## Usage Examples

### Setting up a new development environment
```bash
# Download the latest publisher and set up links
./getPub ~/Development/hl7au

# Download the validator
./getValidator ~/tools/jar
```

### Comparing IG versions
```bash
# Compare two versions of a structure definition
./igdiff "https://build.fhir.org/ig/hl7au/au-fhir-core/StructureDefinition-au-patient.html" \
         "https://build.fhir.org/ig/hl7au/au-fhir-core/branches/feature-branch/StructureDefinition-au-patient.html"
```

### Creating GitHub issues
```bash
# Create an issue for the eRequesting project
./draftIssue 10 "Fix terminology binding" "The ValueSet binding needs to be updated for XYZ element"
```

### Copying IG projects
```bash
# Copy an IG while excluding build artifacts
./copyIG ~/Development/hl7au/source-ig ~/Development/hl7au/target-ig
```

## Contributing

Feel free to submit issues and enhancement requests. Please ensure scripts are tested on macOS and common Linux distributions.

## License

These tools are provided as-is for FHIR IG development workflows.