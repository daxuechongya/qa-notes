### Generate Mood Images – Test Cases

#### TC01 Page Initialization
**Steps**
1. Open the *Generate Mood Images* page

**Expected Result**
- Page loads successfully  
- Generate button is disabled (greyed out)  
- Source Images area is empty  

---
#### TC02 Add One Valid SKU
**Steps**
1. Search for a valid SKU  
2. Click **Add SKU**

**Expected Result**
- Added SKUs shows (1)  
- One SKU card is displayed  
- Corresponding WBG image appears in Source Images  
- Source Images count = 1  
- Generate button becomes enabled  

---
#### TC03 Add Invalid SKU
**Steps**
1. With an existing valid SKU, search for an invalid SKU

**Expected Result**
- Added SKUs count increases by 1  
- Invalid SKU card appears without image  
- Error message shown: `SKU not found in PIM`  
- No new image added to Source Images  
- Source Images count remains unchanged  
---

#### TC04 Remove Invalid SKU
**Steps**
1. Click ❌ on the invalid SKU card

**Expected Result**
- Invalid SKU is removed    
- Source Images remain unchanged

---
#### TC05 Add Multiple Valid SKUs (6)
**Steps**
1. Search and add 6 valid SKUs

**Expected Result**
- Added SKUs shows (6)  
- Six SKU cards displayed  
- Source Images shows WBG1–WBG6  
- Source Images count = 6  

---

#### TC06 Remove a Single SKU
**Steps**
1. Remove any one SKU card

**Expected Result**
- SKU card is removed  
- Corresponding Source Image is removed  
- Source Images count updates correctly  

---

#### TC07 Clear All
**Steps**
1. Click **Clear All**

**Expected Result**
- All SKU cards are removed  
- Source Images area is cleared  
- Generate button becomes disabled  

---
#### TC08 Drag & Drop WBG Images (Limit Validation)
**Steps**
1. Drag 1–5 WBG images into Source Images  
2. Attempt to drag a 6th image

**Expected Result**
- First 5 images are added successfully  
- No response when exceeding the limit  
- Source Images max = 5  

---
#### TC09 Source Images Navigation
**Steps**
1. Click left and right navigation arrows

**Expected Result**
- Images navigate correctly  
- Active image index updates correctly  

---
#### TC10 Added SKUs Scroll Behavior
**Steps**
1. Add 10 SKUs

**Expected Result**
- Added SKUs panel supports scrolling  
- Page layout does not expand infinitely  

---
#### TC11 Template Generate (Upload / Click Image)
**Steps**
1. Upload or select one image  
2. Select a template  
3. Click **Generate**

**Expected Result**
- Image is generated successfully  
- Accept / Reject popup appears  
- Dashboard status:  
  - Accept → `accepted`  
  - Reject → `rejected`  
  - No action → `completed`  
- SKU = User ID  
- Prompt Name = Template name  
- Kind = `manual`  

---

#### TC12 Prompt Generate (No Mandatory Popup)
**Steps**
1. Search for a SKU  
2. Enter a prompt  
3. Click **Generate**

**Expected Result**
- Image is generated successfully  
- No forced Accept / Reject popup  
- User can manually Accept / Reject later  

---
#### TC13 Mixed SKU and Upload Images
**Steps**
1. Add 3 valid SKUs  
2. Upload 2 source images  
3. Add 2 more valid SKUs

**Expected Result**
- Added SKUs count = 5  
- Source Images count = 7  
- Counts are handled independently and correctly  

---
#### TC14 Upload Only + Template Generate
**Steps**
1. Upload multiple source images  
2. Select a template  
3. Click **Generate**

**Expected Result**
- Image is generated successfully  

---
#### TC15 Upload Only + Prompt Generate
**Steps**
1. Upload multiple source images  
2. Enter a prompt  
3. Click **Generate**

**Expected Result**
- Image is generated successfully  

---
#### TC16 Regenerate Flow
**Steps**
1. Upload one image  
2. Generate and Accept  
3. Modify the prompt  
4. Click **Regenerate**

**Expected Result**
- New image is generated  
- Updated prompt is applied  
- Regenerate record appears in Dashboard  

---
#### TC17 Duplicate SKU Validation
**Steps**
1. Add the same valid SKU twice

**Expected Result**
- Duplicate SKU is prevented or warning is shown  
- Source Images are not duplicated  

---
#### TC18 Remove a Source Image
**Steps**
1. Add multiple source images  
2. Remove one image

**Expected Result**
- Only the selected image is removed  
- Source Images count updates correctly  

---
#### TC19 Clear Source Images Before Generate
**Steps**
1. Remove all source images

**Expected Result**
- Generate button becomes disabled  
- Generate action is not allowed

#### TC20 Upload Non-Image File
**Steps**
1. Upload a non-image file (e.g., PDF, TXT)

**Expected Result**
- Error message is displayed  
- File is not added to Source Images  

---
#### TC21 Upload Oversized Image
**Steps**
1. Upload an image exceeding size limits

**Expected Result**
- Size limit error is shown  
- Upload fails without affecting existing images  

---
#### TC22 Upload Duplicate Image
**Steps**
1. Upload the same image twice

**Expected Result**
- Duplicate upload is blocked or warning is shown  

---
#### TC23 Reorder Mixed Source Images
**Steps**
1. Add SKU-based images and uploaded images  
2. Reorder images

**Expected Result**
- Images can be reordered freely  
- Generate uses the current order  

---
#### TC24 Dashboard Log Validation
**Steps**
1. Successfully generate an image  
2. Open Dashboard

**Expected Result**
- SKU / User ID is correct  
- Prompt / Template name is correct  
- Kind is correct  
- Status matches user action  

---
#### TC25 Multi-Tab Behavior
**Steps**
1. Open multiple browser tabs  
2. Perform Generate actions

**Expected Result**
- Actions do not interfere with each other  
- Dashboard records are accurate  

---

#### TC26 Prompt Boundary Validation
**Steps**
1. Enter a very long prompt  
2. Enter special characters / emojis

**Expected Result**
- Length limits enforced or safely handled  
- Generate remains stable  

---
#### TC27 Template Switch Validation
**Steps**
1. Select Template A  
2. Switch to Template B  
3. Click Generate

**Expected Result**
- Template B is used  
- Dashboard record is correct  

---
#### TC28 Accept / Reject Idempotency
**Steps**
1. Click Accept or Reject multiple times on the same result

**Expected Result**
- Final status is consistent  
- No duplicate Dashboard records  

---
#### TC29 Close Page During Generation
**Steps**
1. Start Generate  
2. Close the page before completion

**Expected Result**
- Generation status is traceable in Dashboard  
- No corrupted or partial records  
















































