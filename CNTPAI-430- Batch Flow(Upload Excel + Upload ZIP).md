# Batch Image Generation — Full Test Suite (Manual vs Agent)

---

## Template Rules (Business Logic)

- **Manual template**
  - No AI feedback
  - Display **all original generated images** according to `num_images`

- **Agent template**
  - Has AI selection (AI feedback details are **out of scope**)
  - Display **only 1 final image**

---

## Scope

- **Batch list & status progression (basic)**
- **Upload**
  - Excel / ZIP
  - File type & size validation
  - Comma-separated templates
  - Mixed templates
- **Content validation & error handling**
  - SKU / template / `num_images`
  - Special characters
  - Duplicate SKUs
- **Processing**
  - Status & counters consistency
  - Concurrent batches
- **Batch Details**
  - Manual vs Agent image display rule
  - Errors
  - Search / filter
  - Delete → Regenerate
- **Publish to Salsify**
  - Single image
  - Multi-image (if supported)
  - Multi-SKU batch
  - Idempotency
  - Pre-publish property mapping check
- **Performance**
  - Big files
  - Concurrency
- **Accessibility (minimal)**

## End-to-End (E2E — No AI Feedback Specifics)

### PR-TC-001 (P0) E2E: Excel → Processing → Batch Details → Publish

**Steps**
1. Upload an Excel with valid SKUs, **Manual** template, `num_images = 3`
2. Wait until batch processing completes
3. Open **Batch Details**
4. Select one generated image → click **Publish SKUs**

**Expected**
- Status transitions: `QUEUED → PROCESSING → COMPLETED`
- Batch Details shows **3 original images** (Manual behavior)
- Publish succeeds:
  - SKU status = **PUBLISHED**
  - **Published At** timestamp shown

> **Note**  
> If the environment lacks the PIM property mapping for `mood_image_auto`, all PB tests will block until fixed.

---

## Upload

### UP-TC-001 (P1) Accept `.xlsx`
- **Expected:** File accepted; batch created and queued

### UP-TC-002 (P1) Accept `.xls`
- **Expected:** File accepted; batch created and queued

### UP-TC-003 (P1) Reject `.csv`
- **Expected:** Rejected with message  
  > “Only .xlsx, .xls files are allowed.”  
  Batch not queued

### UP-TC-004 (P1) Required Columns Missing / Renamed / Case / Extra Spaces
- **Expected:** Clear validation message pinpointing problematic columns  
  (case / space tolerance per design)

### UP-TC-005 (P1) Excel > 25MB
- **Expected:** Upload blocked with max-size message

### UP-TC-006 (P1) ZIP Valid (Excel + `/images`)
- **Expected:** Validation passes; processing starts; images correctly matched by **Image Name**

### UP-TC-007 (P1) ZIP Missing `/images` or Name Mismatch
- **Expected:** Clear error listing missing/mismatched samples  
  Valid rows continue **or** batch fails (per design)

### UP-TC-008 (P1) ZIP > 100MB
- **Expected:** Upload blocked with max-size message

### UP-TC-009 (P1) ZIP Contains Disallowed Files (`.exe`, `.js`)
- **Expected:** Upload blocked with disallowed file type message

### UP-TC-010 (P2) Comma-Separated Templates
**Input example:** `double_bed, shadow_add_model`  
- **Expected:**  
  - Parsed as multiple templates  
  - Each template processed independently  
  - Stats correct  
  - Failures clearly identify the template

### UP-TC-011 (P2) Mixed Templates in One File (Manual + Agent)
- **Expected:** Both templates processed correctly; behavior isolated per template type

---

## Error & Validation

### ER-TC-001 (P0) Non-existent / Text SKUs
**Data:** Invalid numeric SKUs + text SKU (e.g. `eira`)  
- **Expected:**  
  - Error: *“Product not found in Salsify or missing WBG image”*  
  - Valid SKUs continue processing

### ER-TC-002 (P0) Invalid Template Name
- **Expected:**  
  - Error: *“Generate Prompt failed”*  
  - Valid template SKUs unaffected

### ER-TC-003 (P0) Mixed Validity (~50% broken rows)
- **Expected:**  
  - Batch not interrupted  
  - Valid SKUs complete  
  - Errors recorded clearly per row

### ER-TC-004 (P0) Non-numeric `num_images`
**Examples:** `three`, `3 images`, `3!`, `4-5`  
- **Expected:** Unified validation error; batch not started

### ER-TC-005 (P0) `num_images = 0` (Lower bound)
- **Expected:** HTTP 400; batch not started

### ER-TC-006 (P0) `num_images = 10` (Upper bound)
- **Expected:** HTTP 400; batch not started

### ER-TC-007 (P1) `num_images = 9` (Max valid)
- **Expected:**
  - Manual: **9 images** displayed
  - Agent: **1 final image** displayed

### ER-TC-008 (P2) Special Characters
**Examples**
- Category: `Beds & Frames*`, `Chairs/Tables`, `Sofas@Home`
- Product Type: `Bed-Frame`, `Chair+Stool`, `Table~Desk`

- **Expected:** Field may be empty; no crash; valid rows continue

### ER-TC-009 (P1) Duplicate SKUs
- **Expected:** De-duplicated; single generation; stats not double-counted

---

## Processing & Status

### PR-TC-002 (P1) Status & Counters Consistency
- **Expected:**
  - Status: `QUEUED → PROCESSING → COMPLETED / FAILED`
  - `Total = Success + Failed`
  - `Started ≤ Completed`

### PR-TC-003 (P1) Concurrent Batches (5–10)
- **Expected:** Stable queue; no stuck jobs; counters accurate

> **Note:** PR-TC-004 and PR-TC-005 intentionally excluded

---

## Batch Details

### DT-TC-001 (P1) Manual Template Display
- **Input:** `num_images = 2`
- **Expected:** 2 original images shown

### DT-TC-002 (P1) Agent Template Display
- **Input:** `num_images = 2 or 3`
- **Expected:** Only 1 final image shown

### DT-TC-003 (P1) Error Column Clarity
- **Expected:** Clear, readable per-row errors

### DT-TC-004 (P2) Search / Filter / Pagination
- **Expected:** Accurate filtering; stable pagination

### DT-TC-005 (P1) Delete → Regenerate (Manual)
- **Expected:** Images cleared; status reset; regeneration shows original images

### DT-TC-006 (P1) Delete → Regenerate (Agent)
- **Expected:** Images cleared; status reset; regeneration shows 1 final image

---

## Publish to Salsify

### PB-TC-001 (P0) Single Image Publication
- **Expected:**  
  - Attribute **AI Mood Image** created/updated  
  - SKU status **PUBLISHED**  
  - Timestamp correct  
  - Image accessible in Salsify

### PB-TC-002 (P1) Multi-image Publication (if supported)
- **Expected:** All selected images uploaded and accessible

### PB-TC-003 (P1) Multi-SKU Batch Publication
- **Expected:** Progress visible; partial failures reported clearly

### PB-TC-004 (P0) Idempotency
- **Expected:** Existing content updated; no duplicate attributes

### PB-TC-005 (P0) Missing PIM Property Mapping
- **Expected:** UI blocks publish with clear guidance

---

## Performance

### PERF-TC-001 (P1) Large ZIP (~100MB)
- **Expected:** Progress feedback; no UI freeze; clear failure if rejected

### PERF-TC-002 (P1) Concurrent Batches
- **Expected:** Stable queue; accurate counters

### PERF-TC-003 (P2) Large SKU Count (e.g., 10k)
- **Expected:** Chunking works; continuous progress; SLA respected


## Recommended Test Data

| File Name | Description |
|----------|-------------|
| **batch_min.xlsx** | Minimal valid dataset with required columns and valid SKU/template values |
| **batch_manual_num3.xlsx** | Manual template with `num_images = 3`; used to verify all original images are displayed |
| **batch_agent_num3.xlsx** | Agent template with `num_images = 3`; used to validate that only one final image is displayed |
| **batch_invalid_template.xlsx** | Contains invalid or unsupported template names |
| **batch_nonexistent_sku.xlsx** | Includes non-existent numeric SKUs and a text SKU (e.g. `eira`) |
| **batch_num_images_edge.xlsx** | Edge cases for `num_images`: `0`, `10`, `9`, and non-numeric values |
| **batch_special_chars.xlsx** | Category and Product Type fields containing special characters |
| **batch_dup_sku.xlsx** | Duplicate SKUs to verify de-duplication behavior |
| **batch_comma_templates.xlsx** | Comma-separated template list in a single row |
| **batch_ok.zip** | ZIP package with Excel file and matching images |
| **batch_mismatch_images.zip** | ZIP package with missing or mismatched image names |
| **batch_heavy.zip** | Large ZIP file (~100MB) used for performance and stress testing |
