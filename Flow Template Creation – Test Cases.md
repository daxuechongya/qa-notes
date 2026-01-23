## Template Creation – Test Cases

### TC01｜Successful Creation (Required Fields Only)

**Precondition:**  
User is logged in and has permission to create templates  

**Test Data:**
- Template Name: valid  
- Feature Type: selected  
- Flow Mode: selected  

**Steps:**
1. Open the Create Template dialog  
2. Fill in all required fields  
3. Click Create Template  

**Expected Result:**
- Template is created successfully  
- Dialog closes  
- New template appears in the list  
- Success message is displayed  

---

### TC02｜Successful Creation (All Fields Filled In)

**Steps:**
1. Fill in all fields  
2. Click Create Template  

**Expected Result:**
- All data is saved correctly  

---

### TC03｜Create a Public Template

**Test Data:**  
- Check “Make this template public”  

**Steps:**
1. Fill required fields  
2. Click Create  

**Expected Result:**
- Template is created  
- Template is marked as Public  

---

### TC04｜Cancel Template Creation

**Steps:**
1. Enter any value  
2. Click Cancel  

**Expected Result:**
- Dialog closes  
- No template is created  

---

### TC05｜Creation Fails When Required Fields Are Missing

**Steps:**
1. Leave required fields empty  
2. Click Create Template  

**Expected Result:**
- Creation is blocked  
- Required field error is shown  

---

### TC06｜Submit Form Using Enter Key

**Steps:**
1. Press Enter in any input field  

**Expected Result:**
- Valid form → Submitted  
- Invalid form → Not submitted; errors displayed  

---

### TC07｜Create Button Enable/Disable Logic

**Steps:**
1. Leave all fields empty  
2. Fill all required fields  
3. Clear one required field  

**Expected Result:**
- Missing required → Button disabled  
- All required filled → Button enabled  
- Required missing again → Button disabled  

---

### TC08｜Prevent Duplicate Submission

**Steps:**
1. Click Create Template multiple times  

**Expected Result:**
- Only one template created  
- Button enters loading state or becomes disabled  

---

### TC09｜Dialog Scroll Behavior

**Steps:**
1. Scroll inside the dialog  

**Expected Result:**
- All fields accessible  
- No layout issues  

---

### TC10｜No Dirty Data When Creation Fails

**Steps:**
1. Trigger a front-end or back-end error  

**Expected Result:**
- No template created  
- No partial or empty data appears in the list  

---

## Field Validation Test Cases

### Template Name

#### TC11｜Template Name Empty
**Expected Result:** Required field error is shown  

#### TC12｜Leading/Trailing Spaces in Name
**Expected Result:** Trimmed or rejected (per system rules)  

#### TC13｜Minimum Name Length
**Test Values:** 0, 1, 2  
**Expected Result:** 0 invalid; ≥1 valid  

#### TC14｜Maximum Name Length
**Test Values:** 100, 101  
**Expected Result:** Length exceeded → blocked or error  

#### TC15｜Duplicate Name
**Expected Result:** Allowed or rejected depending on business logic  

#### TC16｜Special Characters in Name
**Expected Result:** XSS not executed; invalid characters handled correctly  

#### TC17｜Name with Only Spaces or Symbols
**Expected Result:** Invalid name  

---

### Description

#### TC18｜Description Optional
**Expected Result:** Field can be left empty  

#### TC19｜Description Long Text Performance
**Expected Result:** No lag or crash  

#### TC20｜Description Line Break Preservation
**Expected Result:** Line breaks saved and displayed  

#### TC21｜Description XSS Protection
**Expected Result:** `<script>alert(1)</script>` is escaped  

---

### Feature Type (Required Dropdown)

#### TC22｜Feature Type Not Selected
**Expected Result:** Required field error  

#### TC23｜Feature Type Dropdown Options Render Correctly
**Expected Result:** All options appear correctly  

#### TC24｜Feature Type Keyboard Navigation
**Expected Result:** Up/Down to navigate; Enter to select  

#### TC25｜Feature Type Clear Selection
**Expected Result:** Field stays required  

---

### Flow Mode (Required Dropdown)

#### TC26｜Flow Mode Not Selected
**Expected Result:** Required field error  

#### TC27｜Flow Mode Dependency with Feature Type (If any)
**Expected Result:** Incompatible combinations blocked  

#### TC28｜Flow Mode Default Value Behavior
**Expected Result:** Matches design expectation  

---

### Category

#### TC29｜Category Free Text Input
**Expected Result:** Saved correctly  

#### TC30｜Category Max Length
**Expected Result:** Exceeding length is blocked  

#### TC31｜Category Formatting Kept
**Expected Result:** Case and spaces preserved  

---

### Tags

#### TC32｜Tags Optional
**Expected Result:** Allowed to leave empty  

#### TC33｜Tags Comma Splitting
**Expected Result:** Split into tags and trimmed spaces  

#### TC34｜Duplicate Tags Handling
**Expected Result:** Deduplicated or kept per system rules  

#### TC35｜Tags Count Limit
**Expected Result:** Error when exceeding limit  

#### TC36｜Single Tag Length Limit
**Expected Result:** Exceeding length blocked  

#### TC37｜Tags Special Characters / Emoji
**Expected Result:** Handled according to rules  

#### TC38｜Tags Mixed Language Input
**Expected Result:** Saved correctly  

---

### Public Checkbox

#### TC39｜Public Checkbox Default State
**Expected Result:** Unchecked  

#### TC40｜Public Checkbox Toggle Behavior
**Expected Result:** Toggle state persists  

#### TC41｜Public/Private Save Validation
**Expected Result:** Saved Public/Private state matches user selection 
