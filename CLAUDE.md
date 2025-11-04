# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## About This Repository

This is an Appsmith application repository synchronized with Git. Appsmith is a low-code platform for building internal tools. The application structure is defined in JSON files that represent the UI components, data sources, queries, and business logic.

## Repository Structure

```
├── application.json       # Main application configuration (theme, positioning, pages list)
├── metadata.json         # Schema version metadata for Appsmith compatibility
├── theme.json           # UI theme configuration
├── pages/               # Page definitions
│   └── Page1/
│       └── Page1.json   # Page layout and widget configurations (DSL format)
```

## Application Architecture

### Page Structure
- Each page is defined in its own subdirectory under `pages/`
- Page definitions use a JSON DSL (Domain Specific Language) format
- The `dsl` object in each page contains the widget tree with properties like:
  - Layout properties: `topRow`, `bottomRow`, `leftColumn`, `rightColumn`
  - Styling: `backgroundColor`, `containerStyle`
  - Behavior: `dynamicBindingPathList`, `dynamicTriggerPathList`

### Application Configuration
- `application.json` defines global settings:
  - `pages`: Array of page references with default page marked
  - `applicationDetail` and `unpublishedApplicationDetail`: Published and draft versions
  - `appPositioning.type`: Layout system (FIXED or AUTO)
  - `themeSetting`: Controls `appMaxWidth`, `density`, and `sizing`

### Version Information
- `applicationVersion`: Appsmith app schema version (currently 2)
- `evaluationVersion`: JavaScript evaluation engine version
- `fileFormatVersion`: Git sync file format version (in metadata.json)
- `clientSchemaVersion` and `serverSchemaVersion`: Compatibility tracking

## Development Workflow

### Viewing the Application
The application is deployed at: https://ecappsmith.entropiacero.com/applications/690a1259f50d0b1fbf77939e/pages/690a1259f50d0b1fbf7793a0

### Making Changes
Changes to this repository should be made through the Appsmith UI editor, which will automatically sync to Git. Direct JSON editing is possible but should be done carefully:

1. Maintain JSON structure integrity
2. Preserve all schema version numbers
3. Ensure widget IDs remain unique within pages
4. Keep `gitSyncId` values intact

### Git Sync Behavior
- The Appsmith instance automatically commits changes made in the UI
- `gitSyncId` fields link application entities to Git commits
- Both published and unpublished versions are tracked in the JSON files

## Key Concepts

### Widget System
Widgets are the building blocks of Appsmith pages. The root widget is always `MainContainer` (widgetId "0") of type `CANVAS_WIDGET`. All other widgets are children in the DSL tree.

### Layout System
- Grid-based layout with `snapColumns` and `snapRows`
- Position defined by row/column ranges (top/bottom row, left/right column)
- `parentColumnSpace` and `parentRowSpace` define grid cell sizes

### Dynamic Bindings
- `dynamicBindingPathList`: Widget properties bound to JavaScript expressions
- `dynamicTriggerPathList`: Event handlers with JavaScript code
- These enable reactive behavior and data binding
