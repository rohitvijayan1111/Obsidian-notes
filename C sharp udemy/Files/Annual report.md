# AIIA Report Portal — Detailed Page Specifications

## Overview

This document provides pixel-perfect textual specifications for all 7 report module pages. Each page is described in detail to enable accurate UI mockup generation and development.

---

# PAGE 1: CREATE REPORT (Wizard)

## Route: `/reports/new`

## Layout Structure

- **Full page layout** with centered content
- **Max-width container:** 900px centered on page
- **Background:** Light gray (#f7f8fa)

## Page Sections

### Section 1: Header (Top)

**Position:** Top of page, sticky on scroll  
**Height:** 80px  
**Background:** White with bottom border (1px solid #e0e4ea)  
**Components:**

- **Logo/Title (left):** "AIIA Annual Report Portal" | Font: Bold 18px | Color: #1a1a2e
- **Progress Indicator (center):**
    - 5 numbered dots (1-5) representing wizard steps
    - Connected by line
    - Active step: blue circle with white number
    - Completed steps: green circle with checkmark
    - Future steps: gray circle with number
    - Step labels below dots: "Basics", "Structure", "Deadlines", "Workflow", "Review"
    - Total height: 60px | spacing: 60px between dots horizontally
- **Button area (right):** "Cancel" button (outline style, 8px padding)

### Section 2: Wizard Content (Main)

**Position:** Below header  
**Padding:** 40px 30px  
**Min-height:** calc(100vh - 80px - 100px)

#### STEP 1: REPORT BASICS

**Title:** "Create New Annual Report" (size 24px, bold, color #1a1a2e)  
**Subtitle:** "Configure basic report details" (size 13px, color #666)  
**Spacing:** 24px below title

**Form Fields (vertical stack, gap: 20px):**

1. **Report Name** (required field, marked with red asterisk *)
    
    - Label: "Report Name" (11px, color #666)
    - Input field: width 100%, height 40px, border 1px solid #dde1e7, border-radius 6px
    - Placeholder text: "e.g., Annual Report 2026"
    - Focus state: border color #4f8ef7, shadow: 0 0 0 3px rgba(79, 142, 247, 0.1)
2. **Description** (optional)
    
    - Label: "Description" (11px, color #666)
    - Text area: width 100%, height 100px, border 1px solid #dde1e7, border-radius 6px
    - Placeholder: "Brief description of this report cycle..."
    - Focus state: border color #4f8ef7, shadow: 0 0 0 3px rgba(79, 142, 247, 0.1)
3. **Reporting Year** (required field *)
    
    - Label: "Reporting Year" (11px, color #666)
    - Dropdown field: width 100%, height 40px
    - Options: [2026, 2025, 2024, 2023...]
    - Selected value displayed: "2026"
    - Dropdown arrow on right side
4. **Institute** (required field *)
    
    - Label: "Institute" (11px, color #666)
    - Searchable dropdown: width 100%, height 40px
    - Options: List of institutes (AIIA, etc.)
    - Placeholder: "Select institute..."
5. **Use Template** (optional)
    
    - Label: "Use Template" (11px, color #666)
    - Radio buttons (2 options, horizontal layout):
        - Option A: "Start from scratch" (selected by default)
        - Option B: "Use existing template"
    - Conditional: If Option B selected, show dropdown below:
        - Template selector: width 100%, height 40px
6. **Default Language** (required field *)
    
    - Label: "Default Language" (11px, color #666)
    - Dropdown: width 100%, height 40px
    - Options: ["English", "Hindi"]
    - Selected: "English"

**Button Group (bottom, spacing 12px between buttons, margin-top: 30px):**

- "Back" button (outline style, disabled on step 1) | width: 120px
- "Next" button (primary style, blue background) | width: 120px
- "Cancel" button (outline style) | width: 120px
- Alignment: Right-aligned

---

#### STEP 2: SECTION STRUCTURE

**Title:** "Define Report Structure" (size 24px, bold)  
**Subtitle:** "Create sections and subsections for your report" (size 13px, color #666)

**Main Content Area:**

**Left Panel (width: 280px, border-right: 1px solid #e0e4ea):**

- **Label:** "Section Tree" (12px, bold)
- **Add Section Button:** "+ Add Top-Level Section" | width: 100% | height: 36px | primary style
- **Tree View:** Below button, height: 400px, overflow-y: auto
    - Hierarchical display of sections
    - Each section shows:
        - Expand/collapse icon (chevron, rotates 90° when expanded)
        - Section name (editable on click)
        - Delete icon (trash can)
    - Indentation: 20px per level
    - Section colors:
        - Top-level sections: Background light blue on hover
        - Subsections: Slightly indented, normal background
    - Each section has "+ Add Subsection" button on hover
    - Drag-drop handle icon (6 dots) on left for reordering

**Right Panel (flex: 1, padding: 20px):**

- **Currently Selected Section:** (box with border, padding 15px, background #f7f8fa)
    
    - Display: "No section selected" (if none)
    - OR show section details if selected:
        - **Section Name:** Input field, width 100%, height 40px
        - **Description:** Text area, width 100%, height 80px
        - **Position:** Display only (read-only) - "Position: 1"
        - **Subsections Count:** Display only - "Contains X subsections"
        - **Delete Button:** Danger style, width 100px, height 36px
- **Default Template Structure (helpful for users, collapsible section):**
    
    - **Title:** "Suggested Structure (you can customize)"
    - Expandable list showing standard sections:
        1. Committees
        2. General Administration
        3. Hospital
        4. Academic
        5. Research
        6. Miscellaneous
        7. Finance
    - Checkbox beside each - select to auto-add
    - **Button:** "Add Selected Sections" (secondary style)

**Button Group (bottom):**

- "Back", "Next", "Cancel" buttons (same as Step 1)

---

#### STEP 3: DEADLINES

**Title:** "Set Report Deadlines" (size 24px, bold)  
**Subtitle:** "Define submission and review deadlines for each department" (size 13px, color #666)

**Content Area:**

**Top Info Box (background: #e3f2fd, border-left: 4px solid #4f8ef7, padding: 12px, margin-bottom: 20px):**

- Text: "Set deadlines for when departments should submit their sections and when reviews should be completed."

**Main Deadline Configuration (2-column layout, gap: 30px):**

**Column 1: Institute-Level Deadlines (width: 50%)**

- **Label:** "Institute Deadlines" (13px, bold)
- **Spacing:** 16px

1. **Report Start Date**
    
    - Label: "Report Start Date" (11px, color #666)
    - Date picker input: width 100%, height 40px
    - Format: "DD/MM/YYYY"
    - Calendar icon on right
2. **Report End Date**
    
    - Label: "Report End Date" (11px, color #666)
    - Date picker: width 100%, height 40px
3. **Submission Deadline**
    
    - Label: "Overall Submission Deadline" (11px, color #666)
    - Date + time picker: width 100%, height 40px
    - Format: "DD/MM/YYYY HH:MM"
4. **Review Timeline**
    
    - Label: "Review Start Date" (11px, color #666)
    - Date picker: width 100%, height 40px
    - Label: "Review End Date" (11px, color #666)
    - Date picker: width 100%, height 40px

**Column 2: Department-Specific Overrides (width: 50%)**

- **Label:** "Department Deadline Overrides" (13px, bold)
- **Subtitle:** "Leave blank to use institute defaults" (11px, color #888)
- **Spacing:** 16px

**Table (width: 100%, border: 1px solid #e0e4ea, border-radius: 6px):**

- **Header row** (background: #f7f8fa, bold, 12px):
    - Column 1: "Department" (width: 40%)
    - Column 2: "Submission Deadline" (width: 30%)
    - Column 3: "Review Deadline" (width: 30%)
- **Data rows** (height: 45px each, border-bottom: 1px solid #f0f2f5):
    - Department name (text)
    - Date picker (clickable field)
    - Date picker (clickable field)
    - Hover state: background #f9f9f9
- **Empty row at bottom:** "+ Add Department Override"
- **Max-height:** 250px, overflow-y: auto

**Button Group (bottom):**

- "Back", "Next", "Cancel" buttons

---

#### STEP 4: WORKFLOW

**Title:** "Configure Approval Workflow" (size 24px, bold)  
**Subtitle:** "Define the review chain for this report" (size 13px, color #666)

**Content Area:**

**Option 1: Predefined Workflows (Radio button: "Use Predefined Workflow", checked by default)**

**Workflow Selector (2-column grid, gap: 20px):**

**Option A: Standard Workflow**

- Card layout: width: calc(50% - 10px), border: 2px solid #e0e4ea, border-radius: 8px, padding: 16px
- **Title:** "Standard Approval Chain" (13px, bold)
- **Description:** "Contributor → Head of Department → Publication Cell → Director's Office" (12px, color #666)
- **Visual:** Horizontal flow boxes:
    - [Contributor] → [HoD] → [Publication Cell] → [Director]
    - Boxes: height 40px, background #e3f2fd, border 1px solid #90caf9, border-radius 4px
    - Arrows: "→" color #ccc, size 16px
- **Button:** "Select This" (outline style) OR "Selected" (primary style if chosen)

**Option B: Custom Workflow**

- Card layout: similar to Option A
- **Title:** "Custom Workflow" (13px, bold)
- **Description:** "Design your own approval chain" (12px, color #666)
- **Visual:** Placeholder showing "Customizable steps..."
- **Button:** "Configure" (outline style)

**Option 2: Custom Workflow Configuration (Radio button: "Create Custom Workflow")**

- Hidden by default, shows when selected

**Custom Builder (border: 1px solid #e0e4ea, border-radius: 8px, padding: 20px, background: #f9f9f9):**

- **Title:** "Build Your Workflow"
- **Instructions:** "Add steps in the order they should occur" (11px, color #666)
- **Step List (similar to section tree):**
    - Each step displays:
        - Step number circle (1, 2, 3...)
        - Step type dropdown (Submit, Review, Approve, Lock)
        - Role required field
        - Optional checkbox ("Is optional")
        - Timeout field (hours)
        - Delete button
        - Drag-drop handle for reordering
    - Min: 2 steps, Max: 10 steps
- **Add Button:** "+ Add Step" (secondary style, width: 150px)

**Button Group (bottom):**

- "Back", "Next", "Cancel" buttons

---

#### STEP 5: REVIEW & CREATE

**Title:** "Review & Create Report" (size 24px, bold)  
**Subtitle:** "Verify all settings before creating" (size 13px, color #666)

**Summary Sections (each section: border-left: 4px solid #4f8ef7, background: #f9f9f9, padding: 15px, margin-bottom: 15px, border-radius: 4px):**

1. **Report Details**
    
    - Name: "Annual Report 2026"
    - Institute: "AIIA"
    - Year: "2026"
    - Default Language: "English"
    - Edit link (text, color: #4f8ef7, cursor: pointer)
2. **Structure Overview**
    
    - "X top-level sections configured"
    - "X total subsections"
    - List of section names (max 5 visible, "...and X more" if more)
    - Edit link
3. **Deadlines Summary**
    
    - Report Period: "01/01/2026 - 31/12/2026"
    - Submission Deadline: "30/11/2026 23:59:00"
    - Review Period: "01/11/2026 - 15/12/2026"
    - Y department(s) with custom deadlines
    - Edit link
4. **Workflow Summary**
    
    - Selected Workflow: "Standard Approval Chain"
    - Steps:
        1. Contributor submits
        2. HoD reviews
        3. Publication Cell reviews
        4. Director approves
    - Edit link

**Checkbox Section (margin-top: 20px):**

- Checkbox: "I confirm the above configuration is correct"
- Text: "This report will be created and can be edited later." (11px, color #666)

**Button Group (bottom):**

- "Back" button (outline style)
- "Create Report" button (primary style, green/success color, width: 150px, height: 40px)
- "Cancel" button (outline style)

**Success Message (hidden initially, shown on creation):**

- Background: #e8f5e9, border-left: 4px solid #43a047, padding: 15px, border-radius: 4px
- Message: "Report created successfully! Redirecting..." (color: #2e7d32)

---

# PAGE 2: REPORT STRUCTURE

## Route: `/reports/{reportId}/structure`

## Layout Structure

- **Full page with sidebar + main content**
- **Sidebar width:** 220px
- **Main content area:** flex: 1

## Sidebar (Left)

**Background:** White, border-right: 1px solid #e0e4ea

**Sections:**

1. **AIIA Logo & Report Info** (padding: 16px, border-bottom: 1px solid #e0e4ea)
    
    - **Logo:** "AIIA" (14px, bold, color: #1a1a2e)
    - **Subtitle:** "Report Portal" (10px, color: #888)
    - **Spacing:** 12px
2. **Report Quick Info** (padding: 16px, background: #f9f9f9, border-bottom: 1px solid #e0e4ea)
    
    - **Report Name:** "Annual Report 2026" (12px, bold)
    - **Status:** Badge - "In Progress" (small badge, size 10px)
    - **Year:** "2026" (11px, color: #666)
    - **Spacing:** 8px between items
3. **Navigation Menu** (padding: 8px 0)
    
    - Menu items (font: 12px):
        - **Dashboard** (icon: home) - link to /dashboard
        - **Reports** (icon: folder) - link to /reports
        - **Active Report:**
            - **Overview** (icon: eye) - link to /reports/{id}
            - **Structure** (icon: tree) - current page, highlighted
            - **Content** (icon: edit) - link to /reports/{id}/structure
            - **Assign** (icon: users) - link to /reports/{id}/assign
            - **Compile** (icon: download) - link to /reports/{id}/compile
        - **Settings** (icon: gear) - admin settings
    - Active item: background #e8f0fe, left border 3px solid #4f8ef7
    - Inactive items: hover background #f9f9f9

## Main Content Area (Right)

### Top Section: Header & Filters

**Topbar** (padding: 20px, background: white, border-bottom: 1px solid #e0e4ea)

- **Title:** "Report Structure" (left, 18px, bold)
- **Breadcrumb:** "Reports > Annual Report 2026 > Structure" (left below title, 11px, color: #666)
- **Button Group (right):**
    - "View Summary" button (outline style)
    - "Configure Sections" button (outline style)
    - "Export Structure" button (outline style)

**Filters Bar** (padding: 12px 20px, background: #f7f8fa, border-bottom: 1px solid #e0e4ea)

- **Language Selector:** "Language: English ▼" (dropdown, color: #666)
- **View Mode:** Toggle buttons:
    - "Tree View" (active)
    - "Card View"
- **Search:** Input field with icon (search icon on left)
    - Placeholder: "Search sections..."
    - Width: 250px

### Middle Section: Department Progress Overview (Optional Toggle)

**Collapsible Box** (padding: 16px, background: #e3f2fd, border-radius: 6px, margin: 16px 20px)

- **Title:** "Completion Status by Department" (click to expand/collapse)
- **Content (when expanded):**
    - **Grid:** 4 columns, gap 12px
    - Each card shows:
        - Department name (bold, 12px)
        - Progress bar: width 100%, height 8px
        - Completion %: "85%" (12px, bold)
        - Assigned sections: "12/14" (11px, color #666)

### Main Content: Section Hierarchy Tree

**Tree Container** (padding: 20px, background: white, margin: 0 20px 20px 20px, border: 1px solid #e0e4ea, border-radius: 8px)

**Root Level** (first item, no indentation):

- **Container:** background #1a1a2e, padding 12px 16px, border-radius 6px, margin-bottom 8px
- **Content:**
    - Report icon (folder icon, color: white)
    - Report name (bold, 13px, color: white) - "Annual Report 2026"
    - Status badge (small, 10px) - "In Progress"
    - Info: "N sections, X% complete" (11px, color: #aaa)

**Section Nodes** (indented tree structure):

**Each Section Item:**

- **Container:**
    
    - Background: white
    - Border: 1px solid #e0e4ea
    - Border-radius: 6px
    - Padding: 12px
    - Margin: 8px 0 8px 20px (indentation for subsections)
    - Height: 56px
    - Display: flex, align-items: center, gap: 12px
    - Hover state: background #f9f9f9, border-color #c5d8ff
- **Left Icons:**
    
    - Expand/collapse chevron (if has children)
    - Section type icon (folder for section, document for subsection)
- **Content (flex: 1):**
    
    - **Row 1:** Section name (bold, 13px, color #1a1a2e)
    - **Row 2:** "Assigned to: Dr. Sharma, Research Dept" (11px, color #666)
- **Center Badge:**
    
    - Status badge (10px font):
        - Not Started: gray
        - In Progress: blue
        - Submitted: yellow
        - Under Review: purple
        - Approved: green
        - Locked: dark gray
- **Right Metadata (text-align: right):**
    
    - Progress bar (width: 60px, height: 6px)
    - Below: "8/12" (11px, color #666)
    - Below: Deadline info (if exists): "Due: 30/11" (10px, color #888)
- **Action Icons (on hover):**
    
    - Edit icon (pencil) - opens editor
    - Assign icon (users) - opens assign modal
    - Comments icon (speech bubble) - shows comment count badge
    - More options (three dots) - dropdown menu:
        - View
        - Edit
        - Assign
        - Access Control
        - View Comments
        - Delete

**Collapsed View:**

- When section collapsed, shows:
    - Chevron pointing right
    - Section name
    - Status badge
    - "N subsections" count
- Children not visible

**Expanded View:**

- Chevron pointing down
- Section details visible
- All subsections listed below with 40px additional indentation

### Bottom Section: Legend

**Legend Box** (padding: 12px, background: #f7f8fa, border-top: 1px solid #e0e4ea)

- **Title:** "Status Legend" (bold, 11px)
- **Status indicators (inline, gap 16px):**
    - Not Started: gray badge - "Not Started"
    - In Progress: blue badge - "In Progress"
    - Submitted: yellow badge - "Submitted"
    - Under Review: purple badge - "Under Review"
    - Approved: green badge - "Approved"
    - Locked: dark badge - "Locked"

---

# PAGE 3: CONTENT EDITOR

## Route: `/reports/{reportId}/sections/{sectionId}/edit`

## Layout Structure

- **Two-column layout:**
    - **Left Panel:** 300px (Block List)
    - **Right Panel:** flex: 1 (Block Editor)
    - **Gap:** 16px
    - **Padding:** 20px

## Top Header (Sticky)

**Fixed Header** (height: 70px, background: white, border-bottom: 1px solid #e0e4ea, padding: 16px 20px)

- **Left Section:**
    
    - **Breadcrumb:** "Annual Report 2026 > Research Activities > Publications" (11px, color: #666)
    - **Title:** "Publications" (18px, bold, color: #1a1a2e)
- **Center Section:**
    
    - **Language Tabs** (horizontal, gap: 0):
        - Tab 1: "English" (12px font, padding: 8px 16px)
            - Background: white, border-bottom: 3px solid #4f8ef7
            - Status badge: small "Current" badge (green)
        - Tab 2: "Hindi" (12px font, padding: 8px 16px)
            - Background: white
            - Status badge: small "Draft" badge (yellow)
        - Tab 3: "+ Add Language" (12px, color: #4f8ef7, cursor: pointer)
    - **Divider line below tabs**
- **Right Section:**
    
    - **Status Buttons:**
        - "Save Draft" button (outline, 36px height)
        - "Submit" button (primary style, disabled if incomplete)
        - Version dropdown: "Version 3 ▼" (outline style)

## Left Panel: Block List

**Panel Container:**

- Background: white
- Border: 1px solid #e0e4ea
- Border-radius: 8px
- Height: calc(100vh - 200px)
- Display: flex, flex-direction: column
- Overflow: hidden

**Header** (padding: 12px 16px, background: #f7f8fa, border-bottom: 1px solid #e0e4ea)

- **Title:** "Content Blocks" (bold, 12px)
- **Block Count:** "(4 blocks)" (11px, color: #666)

**Block List Container** (flex: 1, overflow-y: auto, padding: 8px)

**Each Block Item:**

- **Container:**
    
    - Background: white
    - Border: 1px solid #e0e4ea
    - Border-radius: 6px
    - Padding: 10px
    - Margin: 6px 0
    - Cursor: pointer
    - Hover state: background #f9f9f9, border-color #c5d8ff
    - Active state: background #e8f0fe, border-color #4f8ef7
- **Content (display: flex, gap: 8px, align-items: center):**
    
    - **Block Type Icon** (left, 16px size):
        - Text icon (T) for rich_text
        - Table icon for table
        - Image icon for image
        - File icon for file_attachment
        - List icon for checklist
    - **Block Info (flex: 1):**
        - **Row 1:** Block name or type (12px, bold, color: #1a1a2e)
        - **Row 2:** "Position N" or description (11px, color: #888)
    - **Required Badge** (if is_required = true):
        - Small red badge or asterisk (*)

**Add Block Button** (bottom of list, margin: 12px 8px)

- Button: "+ Add New Block" (outline style, width: 100%, height: 36px)
- Dropdown on click showing block types:
    - Rich Text
    - Table
    - Image
    - File Attachment
    - Checklist

**Footer** (padding: 12px, border-top: 1px solid #e0e4ea)

- **Info text:** "Drag to reorder blocks" (11px, color: #888)

---

## Right Panel: Block Editor

**Panel Container:**

- Background: white
- Border: 1px solid #e0e4ea
- Border-radius: 8px
- Padding: 24px
- Min-height: calc(100vh - 200px)
- Display: flex, flex-direction: column

**No Block Selected State:**

- Center message: "Select a block from the left to edit" (14px, color: #888)
- Icon: Large document icon (color: #ddd)

**Block Editor (when selected):**

### Block Properties Header

**Section:** "Block Properties"

- **Row 1:** Block Type (readonly)
    
    - Label: "Type:" (bold, 11px)
    - Value: "Rich Text Block" or "Table" etc. (11px)
- **Row 2:** Required Checkbox
    
    - Checkbox + label: "This block is required"
    - Checked state: checkbox ticked, label bold
    - Unchecked state: checkbox empty
- **Row 3:** Position & Numbering
    
    - Label: "Position:" (bold, 11px)
    - Value: "Block 1 of 4" (11px)
    - Reorder buttons: ↑ ↓ (small arrow buttons)

**Divider:** 1px solid #e0e4ea, margin: 16px 0

---

### Block Content Editor (Dynamic based on block type)

#### BLOCK TYPE 1: Rich Text

**Title:** "Content" (bold, 12px, margin-bottom: 12px)

**Editor Container:**

- Background: white
- Border: 1px solid #dde1e7
- Border-radius: 6px
- Min-height: 300px
- Font: Segoe UI, 13px, color: #222

**Toolbar (height: 40px, background: #f7f8fa, border-bottom: 1px solid #e0e4ea, padding: 6px 12px):**

- **Row 1:**
    - Undo/Redo buttons (small icons, disabled gray)
    - Divider (1px)
    - Heading buttons: H1, H2, H3 (toggle buttons)
    - Divider
    - Bold (B), Italic (I), Underline (U) buttons
    - Divider
    - Bullet list, Numbered list buttons
    - Divider
    - Link button (with URL input on click)
    - Image button (opens image upload)
    - Divider
    - Text color, Highlight color buttons
    - Divider
    - Clear formatting button

**Content Area:**

- Editable area below toolbar
- Placeholder: "Start typing your content..."
- Line-height: 1.6
- Padding: 12px

**Character Count:** (below editor, right-aligned)

- "123 characters | 24 words | Guidance: 500-1000 words recommended" (11px, color: #888)

---

#### BLOCK TYPE 2: Table

**Title:** "Table Data" (bold, 12px)

**Table Configuration:**

- **Info Box:** "Define columns first, then add rows" (11px, color: #666, background: #e3f2fd)

**Column Configuration Section:**

- **Label:** "Columns" (bold, 11px)
- **Column List (each item, flex layout, gap: 8px, margin: 8px 0):**
    - Column name input field (width: 150px, height: 32px)
    - Column type dropdown: "Text" (width: 100px)
    - Delete button (small trash icon)
- **Add Column Button:** "+ Add Column" (secondary style, height: 32px, width: 140px)

**Divider:** margin: 16px 0

**Table Data Section:**

- **Label:** "Table Data" (bold, 11px)
- **Table Editor (similar to spreadsheet):**
    - Header row: Column names (background: #e3f2fd, bold)
    - Data rows: Editable cells (height: 32px each)
    - Each cell: input field with auto-complete
    - Last row: empty row for adding new entries
    - Row numbers on left (1, 2, 3...)
    - Delete row button on hover (right side)
    - Add row button at bottom: "+ Add Row"

**Row Count:** "4 rows" (11px, color: #666)

---

#### BLOCK TYPE 3: Image

**Title:** "Image" (bold, 12px)

**Upload Area:**

- **Drag-drop zone:**
    - Background: #f9f9f9
    - Border: 2px dashed #dde1e7
    - Border-radius: 8px
    - Padding: 40px
    - Text center: "Drag image here or click to browse" (13px, color: #666)
    - Icon: Large image icon (color: #ddd)
    - Supported formats: PNG, JPG, GIF, WebP (11px, color: #888)
    - Max file size: 5MB (11px, color: #888)

**After Upload (image preview):**

- **Preview Container:**
    - Image display (max-height: 250px, width: auto)
    - File name below: "photo.jpg" (12px)
    - File size below: "2.5 MB" (11px, color: #666)
    - "Remove" button (red, small)

**Image Properties (below preview):**

- **Caption Input:**
    
    - Label: "Caption" (11px)
    - Text area: width 100%, height 60px
    - Placeholder: "Enter image caption..."
- **Alt Text Input:**
    
    - Label: "Alt Text" (11px)
    - Input field: width 100%, height 36px
    - Placeholder: "Describe the image for accessibility..."
- **Image Size:**
    
    - Label: "Size" (11px)
    - Options (radio buttons):
        - "Small (30%)"
        - "Medium (60%)" (selected by default)
        - "Large (100%)"

---

#### BLOCK TYPE 4: File Attachment

**Title:** "File Attachment" (bold, 12px)

**Upload Area (similar to image):**

- Drag-drop zone with file icon
- "Drag file here or click to browse" text
- Supported: PDF, DOCX, XLSX, PPTX, etc.
- Max: 25MB

**After Upload:**

- **File Display:**
    - File icon (based on type)
    - File name (12px, bold)
    - File size: "2.5 MB" (11px, color: #666)
    - Upload date (11px, color: #888)
    - "Remove" button

**File Properties:**

- **Display Name:**
    
    - Label: "Display Name" (11px)
    - Input field: width 100%, height 36px
    - Default: original filename
- **Description:**
    
    - Label: "Description" (11px)
    - Text area: width 100%, height 60px

---

#### BLOCK TYPE 5: Checklist

**Title:** "Checklist Items" (bold, 12px)

**Checklist Items List:**

- **Each item (flex layout, gap: 12px, margin: 8px 0):**
    - Checkbox (readonly or always unchecked in edit mode)
    - Item text input field (width: 100%, height: 36px)
    - Delete button (trash icon)

**Add Item Button:** "+ Add Item" (secondary style, height: 32px, width: 120px)

**Item Count:** "N items" (11px, color: #666)

---

### Translation Panel (visible when language tab switched)

**When viewing Hindi tab:**

- **Info Box:** "This is a translation of the English version. Edit the Hindi translation below." (11px, color: #666, background: #fff8e1)
- Original English content shown as reference (read-only, background: #f9f9f9)
- Hindi content editor below (editable)
- Status: "Draft" (yellow badge) or "Complete" (green badge)
- Button: "Mark as Complete" (outline style)

---

### Comments Section (Right sidebar, collapsible)

**Comments Sidebar** (width: 280px, border-left: 1px solid #e0e4ea)

- **Header:** "Comments" (bold, 12px)
- **Comment Count:** "(3)" (11px)
- **Auto-refresh indicator:** "Live updates" (10px, color: #4f8ef7)

**Comments List (height: 300px, overflow-y: auto):**

- **Each comment:**
    - Author avatar (28px circle)
    - Author name (bold, 12px)
    - Timestamp (11px, color: #888) - "2 hours ago"
    - Comment text (12px, color: #444)
    - "Reply" link (11px, color: #4f8ef7)
    - "Resolve" link (11px, color: #4f8ef7)

**Add Comment Section (bottom):**

- **Input:** Text area, width 100%, height 60px
- **Placeholder:** "Add a comment..."
- **Button:** "Post Comment" (primary style, width: 100%, height: 32px)

---

### Bottom Action Bar (Sticky)

**Container** (position: fixed, bottom: 0, left: 0, right: 0, height: 60px, background: white, border-top: 1px solid #e0e4ea, padding: 12px 20px)

**Content:**

- **Left:** "Changes auto-saved" (11px, color: #43a047, with checkmark icon)
- **Center:** "Block 3 of 4 - Publications Table"
- **Right:**
    - "Preview" button (outline style)
    - "Save Draft" button (primary style)

---

# PAGE 4: ASSIGN SECTIONS

## Route: `/reports/{reportId}/assign`

## Layout Structure

- **Two-column layout with modal overlay**
- **Left Panel:** 320px (Section Tree)
- **Right Panel:** flex: 1 (Assignment Configuration)
- **Padding:** 20px

## Top Header

**Title:** "Assign Sections to Contributors" (18px, bold)  
**Subtitle:** "Select sections and assign to users/departments" (12px, color: #666)

---

## Left Panel: Section Tree with Checkboxes

**Container:**

- Background: white
- Border: 1px solid #e0e4ea
- Border-radius: 8px
- Padding: 12px
- Max-height: calc(100vh - 150px)
- Overflow-y: auto

**Header:**

- "Sections to Assign" (bold, 12px)
- "Select all" checkbox (right-aligned)

**Tree Structure:**

- **Root:** checkbox + "Annual Report 2026" (bold, 12px)
- **Section 1:** checkbox + "Research Activities" (indented 20px)
    - **Subsection 1a:** checkbox + "Publications" (indented 40px)
    - **Subsection 1b:** checkbox + "Patents" (indented 40px)
- **Section 2:** checkbox + "Financial Summary" (indented 20px)
- etc.

**Interactions:**

- Parent checkbox: when checked, all children auto-checked
- Children unchecked: parent becomes indeterminate (dash icon)
- Checked sections: background highlight #e8f0fe
- Count display: "3 sections selected" (at bottom, 11px)

---

## Right Panel: Assignment Configuration

**Configuration Tabs (horizontal, gap: 12px):**

- **Tab 1:** "Assign To" (active by default)
- **Tab 2:** "Set Deadlines"
- **Tab 3:** "Access Control"

### TAB 1: ASSIGN TO

**Subsection 1: Select Assignees**

- **Label:** "Assign To" (bold, 12px)
- **Info:** "Selected sections: 3" (11px, color: #666)

**Selection Options (radio buttons):**

- Option 1: "Assign to specific users"
- Option 2: "Assign to department" (selected by default)

**If Option 1: Assign to Users**

- **User Search:** Searchable multiselect
    - Placeholder: "Search users..."
    - Autocomplete dropdown showing matching users
    - Selected users shown as chips: [Dr. Sharma ×] [Dr. Mehta ×]
    - Chip background: #e8f0fe, text: #1a5dc8

**If Option 2: Assign to Department**

- **Department Dropdown:**
    - Width: 100%, height: 40px
    - Options: [Department of Research, Finance Dept, Admin Dept...]
    - Selected value displayed

**Subsection 2: Review Assignments**

- **Table:**
    - Columns:
        - "Section" (40%)
        - "Assigned To" (35%)
        - "Status" (15%)
        - "Action" (10%)
    - Rows (one per section):
        - Section name
        - Assignee(s) names or department
        - Status badge: "Not Assigned" or "Assigned"
        - Delete button (trash icon)

**Subsection 3: Bulk Actions**

- **Buttons:**
    - "Clear All Assignments" (danger style, outline)
    - "Save Assignments" (primary style)

---

### TAB 2: SET DEADLINES

**Instruction:** "Set individual deadlines for each assigned section" (11px, color: #666)

**Table:**

- **Columns:**
    
    - "Section" (30%)
    - "Assigned To" (30%)
    - "Submission Deadline" (20%)
    - "Review Deadline" (15%)
    - "Notes" (5%)
- **Rows (one per assignment):**
    
    - Section name
    - Assignee name
    - Date + time picker (clickable, shows calendar on click)
    - Date + time picker (clickable)
    - Text input for notes (clickable)

**Buttons:**

- "Use Institute Defaults" (secondary style, outline)
- "Save Deadline Changes" (primary style)

---

### TAB 3: ACCESS CONTROL

**Instruction:** "Configure who can view, edit, review, or approve each section" (11px, color: #666)

**Access Matrix:**

- **Columns:**
    
    - "Section" (20%)
    - "Principal (User/Dept)" (25%)
    - "View" (13.75%)
    - "Edit" (13.75%)
    - "Review" (13.75%)
    - "Approve" (13.75%)
- **Rows:**
    
    - Section name
    - Principal name
    - Radio buttons (one per access level):
        - View: radio button
        - Edit: radio button
        - Review: radio button
        - Approve: radio button
    - Selected option: filled radio button, background row: light blue
    - Hover: background #f9f9f9

**Add Access Button:** "+ Grant Access to Another User/Dept" (secondary style)

- Opens form:
    - Principal selector (dropdown)
    - Access level selector (radio buttons)
    - Add button
    - Cancel button

**Buttons (bottom):**

- "Save Access Changes" (primary style)

---

## Bottom Action Bar

**Container** (position: fixed, bottom: 0, left: 0, right: 0, height: 60px, background: white, border-top: 1px solid #e0e4ea, padding: 12px 20px)

**Content:**

- **Left:** "3 sections selected for assignment" (12px)
- **Right:**
    - "Cancel" button (outline style)
    - "Save All Changes" button (primary style)

---

# PAGE 5: REVIEW SCREEN

## Route: `/reports/{reportId}/sections/{sectionId}/review`

## Layout Structure

- **Three-column layout:**
    - **Left Panel:** 200px (Workflow Steps)
    - **Center Panel:** flex: 1 (Content Review)
    - **Right Panel:** 320px (Review Actions)
    - **Padding:** 20px
    - **Gap:** 16px

## Top Header (Sticky)

**Fixed Header** (height: 70px, background: white, border-bottom: 1px solid #e0e4ea, padding: 16px 20px)

- **Left Section:**
    
    - **Breadcrumb:** "Annual Report 2026 > Research Activities > Publications > Review" (11px, color: #666)
    - **Title:** "Review: Publications" (18px, bold)
- **Right Section:**
    
    - **Status Badge:** "Pending Review" (yellow badge, 12px)
    - **Reviewer Info:** "You are reviewing as: Head of Department" (11px, color: #666)

---

## Left Panel: Workflow Pipeline

**Container:**

- Background: white
- Border: 1px solid #e0e4ea
- Border-radius: 8px
- Padding: 12px

**Title:** "Review Pipeline" (bold, 12px, margin-bottom: 16px)

**Workflow Steps (vertical display):**

- **Step 1: Contributor (COMPLETED)**
    
    - Background: #e8f5e9 (light green)
    - Content:
        - Checkmark icon (green, size 20px)
        - Step name: "Contributor" (bold, 12px)
        - Status: "Submitted" (green, 11px)
        - By: "Dr. Sharma" (11px, color: #666)
        - Date: "2024-11-25 10:30 AM" (10px, color: #888)
    - Height: 80px, padding: 12px
- **Step 2: Head of Department (CURRENT)**
    
    - Background: #e3f2fd (light blue)
    - Border-left: 4px solid #4f8ef7
    - Content:
        - Circle with "2" (blue background, white text, size 20px)
        - Step name: "Head of Department" (bold, 12px, color: #1565c0)
        - Status: "Under Review" (blue, 11px)
        - By: "YOU - Pending" (bold, 11px, color: #1565c0)
    - Height: 80px, padding: 12px
- **Step 3: Publication Cell (PENDING)**
    
    - Background: #f5f5f5 (light gray)
    - Content:
        - Circle with "3" (gray background, color: #888)
        - Step name: "Publication Cell" (12px, color: #888)
        - Status: "Pending" (gray, 11px)
    - Height: 70px, padding: 12px
    - Opacity: 0.6
- **Step 4: Director's Office (PENDING)**
    
    - Background: #f5f5f5
    - Content:
        - Circle with "4" (gray background)
        - Step name: "Director's Office" (12px, color: #888)
        - Status: "Pending" (gray, 11px)
    - Height: 70px, padding: 12px
    - Opacity: 0.6

---

## Center Panel: Content Review

**Container:**

- Background: white
- Border: 1px solid #e0e4ea
- Border-radius: 8px
- Padding: 20px
- Max-height: calc(100vh - 150px)
- Overflow-y: auto

**Title:** "Submitted Content (Version 3)" (bold, 14px, margin-bottom: 16px)

**Content Block Rendering (read-only):**

**For each content block:**

- **Block Header:**
    
    - Block number & type: "Block 1 - Publications Table" (bold, 12px)
    - Status: Badge showing "Submitted" or "Pending Review"
    - Required indicator: Red asterisk if required
- **Block Content:**
    
    - **If Rich Text:**
        
        - Rendered HTML-like text display (formatted, headings, lists visible)
        - Background: #f9f9f9
        - Padding: 12px
        - Border-radius: 4px
        - Font: 13px, line-height: 1.6
    - **If Table:**
        
        - Read-only table display (no editing)
        - Header row: background #f0f5ff, bold
        - Data rows: normal display
        - Row count info: "4 rows × 5 columns"
    - **If Image:**
        
        - Image preview (max-height: 300px)
        - Caption below (italic, 12px)
        - File info: "filename.jpg | 2.5MB"
    - **If File:**
        
        - File icon + name as clickable link
        - File size & type info
    - **If Checklist:**
        
        - Read-only checklist items (bullets)
        - Checkmarks shown if completed
- **Block Divider:** 1px solid #e0e4ea, margin: 20px 0
    

**Submission Details (below all content):**

- **Submitted by:** "Dr. Sharma, Contributor" (11px)
- **Submitted at:** "2024-11-25 10:30 AM" (11px)
- **Version:** "Version 3" (11px)

---

## Right Panel: Review Actions

**Container:**

- Background: white
- Border: 1px solid #e0e4ea
- Border-radius: 8px
- Padding: 16px
- Max-height: calc(100vh - 150px)
- Overflow-y: auto

### Subsection 1: Assignment Info

**Header:** "Assignment Details" (bold, 12px)

- Section: "Publications" (11px)
- Department: "Research" (11px)
- Deadline: "30/11/2024 23:59" (11px)
- Status indicator: "On Track" (green badge, 11px) or "Overdue" (red)

**Divider:** margin: 12px 0

### Subsection 2: Comments Thread

**Header:** "Comments & Feedback" (bold, 12px, margin-bottom: 12px)

**Existing Comments (height: 200px, overflow-y: auto):**

- **Each comment:**
    - Avatar (20px circle, initials)
    - Author name (bold, 11px)
    - Timestamp (10px, color: #888)
    - Comment text (11px, color: #444)
    - Thread replies (indented 20px)
    - Reply link (11px, color: #4f8ef7)

**Comment Input Area:**

- **Textarea:** width: 100%, height: 70px, border: 1px solid #dde1e7, border-radius: 4px
- **Placeholder:** "Add your review comments here..."
- **Button Below:** "Post Comment" (primary style, width: 100%, height: 32px)

**Divider:** margin: 12px 0

### Subsection 3: Review Action Form

**Header:** "Your Review Decision" (bold, 12px, margin-bottom: 12px)

**Decision Buttons (2-column layout, gap: 12px):**

1. **Approve Button**
    
    - Large button: width: 100%, height: 50px
    - Background: #43a047 (green)
    - Text: "✓ Approve" (16px, bold, white)
    - Hover: darker green
    - Click: reveals approval form below
2. **Send Back Button**
    
    - Large button: width: 100%, height: 50px
    - Background: #f57c00 (orange)
    - Text: "↶ Send Back" (16px, bold, white)
    - Hover: darker orange
    - Click: reveals feedback form below

**Conditional Form 1: Approval Form (shown when "Approve" clicked)**

- **Header:** "Confirm Approval" (bold, 12px)
- **Checkbox:** "I approve this submission" (checkbox + label)
- **Reviewer Notes (optional):**
    - Textarea: width: 100%, height: 60px
    - Placeholder: "Add approval notes (optional)..."
- **Signature Capture (optional):**
    - Checkbox: "Include digital signature"
    - Hidden by default, shows when checked:
        - Name field (pre-filled with reviewer name)
        - Timestamp (auto-filled, read-only)
        - Signature box: "Sign with mouse, touch, or stylus" (placeholder)
- **Buttons:**
    - "Confirm & Approve" (green, width: 100%, height: 36px)
    - "Cancel" (outline, width: 100%, height: 36px)

**Conditional Form 2: Feedback Form (shown when "Send Back" clicked)**

- **Header:** "Provide Feedback" (bold, 12px)
- **Feedback Textarea:**
    - Width: 100%, height: 80px
    - Placeholder: "Describe what needs to be corrected..."
    - Required field (marked with *)
- **Issue Type Dropdown (optional):**
    - Label: "Issue Type" (11px)
    - Options: ["Content missing", "Formatting issue", "Data error", "Other"]
- **Buttons:**
    - "Send Back with Feedback" (orange, width: 100%, height: 36px)
    - "Cancel" (outline, width: 100%, height: 36px)

---

# PAGE 6: COMPILE REPORT

## Route: `/reports/{reportId}/compile`

## Layout Structure

- **Full page with header and content area**
- **Padding:** 20px
- **Max-width:** 1200px, centered

## Top Header

**Title:** "Compile & Export Report" (18px, bold)  
**Subtitle:** "Generate final approved report in Word or PDF format" (12px, color: #666)

---

## Main Content Area

### Subsection 1: Pre-Compilation Status Check

**Status Box (padding: 16px, background: #e3f2fd, border-left: 4px solid #4f8ef7, border-radius: 4px, margin-bottom: 20px):**

- **Title:** "Compilation Status" (bold, 12px)
- **Content:**
    - ✓ "Report structure defined" (11px)
    - ✓ "All required sections assigned" (11px)
    - ? "18/20 sections approved" (11px, color: #f57f17, with warning icon)
    - ✗ "2 sections still under review" (11px, color: #e53935)
    - Info: "You can compile the report with pending sections. Only approved content will be included." (11px)

**Action Box (background: #fff8e1, border-left: 4px solid #f57c00, padding: 12px, margin-bottom: 20px):**

- Message: "2 sections are not yet approved. Compilation will skip these sections. Continue?" (11px)
- Buttons:
    - "Wait for Approvals" (outline, small)
    - "Proceed with Current Approved Sections" (primary, small)

---

### Subsection 2: Compilation Configuration

**Configuration Panels (2-column layout, gap: 20px):**

**Column 1: Output Settings (width: 50%)**

**Card 1: Report Scope**

- **Title:** "Report Scope" (bold, 12px, margin-bottom: 12px)
- **Checkboxes (vertical stack, gap: 8px):**
    - ☑ "Include Front Matter (Title page, TOC)"
    - ☑ "Include Table of Contents"
    - ☑ "Include Section Numbering (1, 1.1, 1.1.1, etc.)"
    - ☑ "Include Page Numbers"
    - ☑ "Include Figures & Images"
    - ☑ "Include Appendices"

**Card 2: Content Language**

- **Title:** "Content Language" (bold, 12px, margin-bottom: 12px)
- **Options (radio buttons, vertical):**
    - ( ) "English Only"
    - ( ) "Hindi Only"
    - (●) "Bilingual (English & Hindi)" (selected by default)
        - Sub-options (when bilingual selected):
            - "Separate documents (EN + HI)" (selected)
            - "Mixed layout (EN on left, HI on right)"
- **Visual:** "Bilingual layout preview" (small preview image)

**Column 2: Export Format (width: 50%)**

**Card 1: Output Format**

- **Title:** "Export Format" (bold, 12px, margin-bottom: 12px)
    
- **2 Format Options (as cards, width: 48% each, border: 2px solid #e0e4ea, padding: 12px, cursor: pointer):**
    
    **Option 1: Word Document (DOCX)**
    
    - Icon: Word icon (large, 40px)
    - Title: "Microsoft Word" (bold, 12px)
    - Extension: ".docx" (10px, color: #666)
    - Description: "Editable document, best for sharing and further editing" (10px, color: #666)
    - Border: 2px solid #dde1e7
    - Hover: background #f9f9f9
    - Selected: border-color #4f8ef7, background #e8f0fe
    
    **Option 2: PDF Document (PDF)**
    
    - Icon: PDF icon (large, 40px)
    - Title: "Adobe PDF" (bold, 12px)
    - Extension: ".pdf" (10px, color: #666)
    - Description: "Read-only format, best for distribution and archiving" (10px, color: #666)
    - Border: 2px solid #dde1e7
    - Selected state: border-color #4f8ef7, background #e8f0fe

**Card 2: PDF-Specific Options (shown if PDF selected)**

- **Options (checkboxes):**
    - ☑ "Embed fonts"
    - ☑ "Create bookmarks from headings"
    - ☑ "Compress images for file size"
    - ☑ "Add watermark: CONFIDENTIAL" (optional)

---

### Subsection 3: Report Preview

**Tab Group (horizontal, gap: 0, margin-top: 20px, margin-bottom: 20px):**

- **Tab 1:** "Preview" (active)
- **Tab 2:** "Settings"
- **Tab 3:** "History"

**Tab 1 Content: Preview**

- **Container:** border: 1px solid #e0e4ea, border-radius: 8px, padding: 20px, background: white
- **Content (height: 400px, overflow-y: auto):**
    - **Preview of report structure:**
        - "ANNUAL REPORT 2026 | All India Institute of Ayurveda" (center, 18px, bold)
        - "Report Period: 01/01/2026 - 31/12/2026" (center, 12px)
        - Horizontal line divider
        - Table of Contents section:
            - "1. Research Activities"
            - " 1.1 Publications"
            - " 1.2 Patents"
            - "2. Financial Summary"
        - Horizontal line divider
        - Sample section page:
            - "1. RESEARCH ACTIVITIES" (14px, bold)
            - Sample text from first section
            - "[Table preview]"
            - "Next section preview..." (grayed out)

**Tab 2 Content: Settings (hidden by default)**

- Compilation settings (metadata like creator, subject, etc.)

**Tab 3 Content: History (hidden by default)**

- List of previous compilations with timestamps

---

### Subsection 4: Compilation Action

**Compilation Box (border: 1px solid #e0e4ea, border-radius: 8px, padding: 20px, background: #f9f9f9, margin-top: 20px):**

**Title:** "Ready to Compile" (bold, 14px)  
**Info:** "This will generate a final report with all approved sections in the selected format(s)." (11px, color: #666)

**Buttons (gap: 12px, margin-top: 16px):**

1. **Download Report Button**
    
    - Primary style (blue, #4f8ef7)
    - Height: 44px
    - Width: auto (200px)
    - Icon: Download icon (left)
    - Text: "Generate & Download" (bold, 13px)
    - Disabled state: grayed out if no format selected
    - Click: triggers compilation, shows progress
2. **Cancel Button**
    
    - Outline style
    - Height: 44px
    - Text: "Cancel"

**Progress Indicator (shown after compilation starts):**

- Progress bar (width: 100%, height: 8px)
- Background: #e0e4ea
- Fill color: #4f8ef7
- Percentage text: "45% - Generating document..." (12px)
- Estimated time: "~2 minutes remaining" (11px, color: #888)

**Success Message (shown on completion):**

- Background: #e8f5e9
- Border-left: 4px solid #43a047
- Text: "✓ Report compiled successfully! Download link below." (bold, 12px)
- Link: "Download Report" (underline, color: #1b5e20)
- Link: "View in browser" (underline, color: #1b5e20)

---

# PAGE 7: REPORT STATUS & HISTORY

## Route: `/reports/{reportId}`

## Layout Structure

- **Full page with header and content grid**
- **Padding:** 20px
- **Max-width:** 1400px, centered

## Top Header

**Title:** "Annual Report 2026 - Overview" (18px, bold)  
**Breadcrumb:** "Reports > Annual Report 2026" (11px, color: #666)

---

## Main Content Area

### Section 1: Report Metadata Cards (Grid)

**Grid Layout:** 4 columns, gap: 16px, margin-bottom: 20px

**Card 1: Report Status**

- Background: white, border: 1px solid #e0e4ea, border-radius: 8px, padding: 16px
- **Title:** "Status" (11px, color: #666)
- **Value:** Badge - "In Progress" (blue badge, size 12px)
- **Subtext:** "3 sections approved, 2 under review" (11px, color: #888)

**Card 2: Progress**

- **Title:** "Overall Progress" (11px, color: #666)
- **Value:** "60%" (24px, bold, color: #1a1a2e)
- **Progress bar below:** width: 100%, height: 8px, 60% filled (blue)
- **Subtext:** "12 of 20 sections approved" (11px, color: #888)

**Card 3: Deadline Info**

- **Title:** "Submission Deadline" (11px, color: #666)
- **Value:** "30 Nov 2026" (18px, bold)
- **Indicator:** "On Track ✓" (green, 11px)
- **Subtext:** "15 days remaining" (11px, color: #888)

**Card 4: Report Period**

- **Title:** "Reporting Period" (11px, color: #666)
- **Value:** "01 Jan - 31 Dec 2026" (13px, bold)
- **Subtext:** "Annual cycle" (11px, color: #888)

---

### Section 2: Status Timeline

**Container:** border: 1px solid #e0e4ea, border-radius: 8px, padding: 20px, background: white, margin-bottom: 20px

**Title:** "Report Lifecycle" (bold, 13px, margin-bottom: 16px)

**Timeline (horizontal flow):**

- **Step 1: Created** (circle with checkmark, green background)
    
    - Date: "01 Oct 2026"
    - Status: "Completed"
- **Arrow:** →
    
- **Step 2: Sections Assigned** (circle with checkmark, green background)
    
    - Date: "05 Oct 2026"
    - Status: "Completed"
- **Arrow:** →
    
- **Step 3: Content Capture** (circle with number 3, blue background)
    
    - Date: "In Progress"
    - Status: "12/20 sections filled"
- **Arrow:** →
    
- **Step 4: Review** (circle with number 4, gray background)
    
    - Date: "Pending"
    - Status: "Waiting for submissions"
- **Arrow:** →
    
- **Step 5: Compilation** (circle with number 5, gray background)
    
    - Date: "Pending"
    - Status: "Not started"
- **Arrow:** →
    
- **Step 6: Archive** (circle with number 6, gray background)
    
    - Date: "Pending"
    - Status: "Not started"

---

### Section 3: Section Progress Table

**Container:** border: 1px solid #e0e4ea, border-radius: 8px, overflow: hidden, margin-bottom: 20px

**Header:** padding: 12px 16px, background: #f7f8fa

- **Title:** "Section Completion Status" (bold, 12px)
- **Filter buttons (right):** "All", "In Progress", "Approved", "Locked"

**Table:**

- **Columns:**
    
    - "Section" (25%)
    - "Assigned To" (20%)
    - "Status" (15%)
    - "Deadline" (15%)
    - "Completion" (15%)
    - "Action" (10%)
- **Rows (height: 50px each, border-bottom: 1px solid #f0f2f5):**
    
    - **Row 1:**
        
        - Section name: "Research Activities" (bold, 12px)
        - Assigned: "Research Dept" (11px)
        - Status badge: "In Progress" (blue)
        - Deadline: "30 Nov" (11px)
        - Completion: "8/12 subsections" (11px, color: #666)
        - Action: "View" link (color: #4f8ef7)
    - **Row 2:**
        
        - Section: "Publications" (indented, 12px)
        - Assigned: "Dr. Sharma" (11px)
        - Status: "Approved" (green badge)
        - Deadline: "20 Nov" (green checkmark ✓)
        - Completion: "100%" with progress bar
        - Action: "View" link
    - **Row 3:**
        
        - Section: "Patents" (indented)
        - Assigned: "Dr. Mehta" (11px)
        - Status: "Under Review" (purple badge)
        - Deadline: "30 Nov" (11px)
        - Completion: "90%" with progress bar
        - Action: "View" link
    - **Rows 4-N:** Similar structure for all sections
        

**Footer:** "Showing 20 sections" (11px, color: #888)

---

### Section 4: Activity Feed

**Container:** border: 1px solid #e0e4ea, border-radius: 8px, padding: 20px, background: white

**Title:** "Recent Activity" (bold, 13px, margin-bottom: 16px)

**Activity List (height: 300px, overflow-y: auto):**

**Each Activity Item:**

- **Timeline marker:** Vertical line with circle (color varies by event type)
- **Event details (flex: 1):**
    - **Title:** "Dr. Sharma submitted Publications section" (bold, 12px)
    - **Timestamp:** "2 hours ago" (11px, color: #888)
    - **Details:** "3 content blocks submitted for HoD review" (11px, color: #666)
    - **Metadata:** User avatar + name

**Activity Types (color-coded):**

- Submission: Blue circle
- Approval: Green circle
- Sent Back: Orange circle
- Lock: Gray circle
- System: Purple circle

**Sample Activities:**

1. "Report created by Institute Admin" (4 days ago)
2. "Sections assigned to Research Department" (4 days ago)
3. "Dr. Sharma started editing Publications" (3 days ago)
4. "Dr. Mehta submitted Patents section" (2 days ago)
5. "HoD approved Publications" (2 hours ago)
6. "2 sections sent back for revision" (1 hour ago)

**Load More Button:** "Load More Activities" (centered, outline style, margin-top: 12px)

---

## Bottom Navigation

**Fixed Footer** (position: fixed, bottom: 0, left: 0, right: 0, height: 60px, background: white, border-top: 1px solid #e0e4ea, padding: 12px 20px)

**Buttons (right-aligned, gap: 12px):**

- "Edit Structure" button (outline)
- "Assign Sections" button (outline)
- "View Full Report" button (primary)

---

# GLOBAL DESIGN SYSTEM

## Colors

- **Primary Blue:** #4f8ef7
- **Dark Background:** #1a1a2e
- **Light Background:** #f7f8fa
- **Card Background:** #fff
- **Border Color:** #e0e4ea
- **Text Primary:** #1a1a2e
- **Text Secondary:** #666
- **Text Tertiary:** #888
- **Status Green:** #43a047
- **Status Orange:** #f57c00
- **Status Red:** #e53935
- **Status Yellow:** #f57f17
- **Status Purple:** #6a1b9a
- **Status Blue:** #1565c0

## Typography

- **Page Title:** 24px, bold, color: #1a1a2e
- **Section Title:** 18px, bold, color: #1a1a2e
- **Card Title:** 14px, bold, color: #1a1a2e
- **Label:** 12px, bold, color: #666
- **Body Text:** 12px, color: #222
- **Small Text:** 11px, color: #888
- **Metadata:** 10px, color: #aaa

## Spacing

- **Padding Standard:** 16px
- **Gap Standard:** 12px
- **Border Radius Standard:** 6px
- **Border Width:** 1px (normal), 2px (emphasis)

## Interactive Elements

- **Button Height Standard:** 36px
- **Input Height Standard:** 40px
- **Border Radius Buttons:** 5px
- **Focus State:** 3px blue outline with 10% opacity shadow

## Responsive Breakpoints

- **Desktop:** 1400px+
- **Tablet:** 768px - 1399px
- **Mobile:** <768px (not prioritized in phase 1)

---

# IMPLEMENTATION PRIORITIES

## Phase 1: Foundation

1. Page layout structure and routing
2. Sidebar navigation
3. Topbar and header components
4. Button and badge components
5. Form input components

## Phase 2: Core Pages

6. Create Report wizard (all 5 steps)
7. Report Structure page
8. Report Status & History page

## Phase 3: Content Editing

9. Content Editor page (all block types)
10. Block editors (rich text, table, image, file, checklist)
11. Comments system

## Phase 4: Workflow

12. Assign Sections page
13. Review Screen page
14. Approval actions and workflows

## Phase 5: Compilation

15. Compile Report page
16. Export functionality (backend integration)
17. Final polish and testing