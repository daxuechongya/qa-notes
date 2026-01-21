#### TC01: History log should be created after prompt generation

**Steps:**
1. Single mood generation  
2. Select from product catalog  
3. Enter a SKU and confirm  
4. Select a template  
5. Click **Generate Prompt**

**Expected Result:**
- A new record should appear in the **History panel**
- `Kind` should be **PROMPT_CREATED**

---

#### TC02: History log after image generation

**Steps:**
1. Single mood generation  
2. Select from product catalog  
3. Enter a SKU and confirm  
4. Use AI template  
5. Select a template and generate prompt  
6. After prompt is generated successfully, click **Generate Image**

**Expected Result:**
- **SKU**: Corresponding SKU is recorded  
- **Prompt Name**: Corresponding prompt name is recorded  
- **AI**: Gemini  
- **Status**: Complete  
- **Kind**: IMAGES_COMPLETED  
- **System Prompt**: Template content  
- **Used Prompt**: Generated prompt  

---

#### TC03: Kind should change after “Try Agent Feedback”

**Steps:**
1. Single mood generation  
2. Select from product catalog  
3. Enter a SKU and confirm  
4. Use AI template  
5. Select a template and generate prompt  
6. Generate image successfully  
7. Click **Try Agent Feedback**

**Expected Result:**
- **Status** should change to **Feedback Submitted**  
- **Kind** should change to **FEEDBACK_SUBMITTED**

---

#### TC04: Regenerate image by clicking “Improve Image”

**Steps:**
1. Single mood generation  
2. Select from product catalog  
3. Enter a SKU and confirm  
4. Use AI template  
5. Select a template and generate prompt  
6. Generate image successfully  
7. (Optional) Try Agent Feedback  
8. Click **Improve Image** and regenerate successfully  

**Expected Result:**
- **SKU**: Corresponding SKU is recorded  
- **Prompt Name**: Corresponding prompt name is recorded  
- **AI**: Gemini  
- **Status**: Complete  
- **Kind**: IMAGES_COMPLETED  

---

#### TC05: Reject result from chat

**Steps:**
1. Single mood generation  
2. Select from product catalog  
3. Enter a SKU and confirm  
4. Use AI template  
5. Select a template and generate prompt  
6. Generate image successfully  
7. Click **Reject Result**, enter rejection reason, and submit  

**Expected Result:**
- **Status**: Rejected  
- **Kind**:  
  - **IMAGES_COMPLETED** (if *Try Agent Feedback* is not used)  
  - **FEEDBACK_SUBMITTED** (if *Try Agent Feedback* is enabled)

---

#### TC06: Accept result from chat

**Steps:**
1. Single mood generation  
2. Select from product catalog  
3. Enter a SKU and confirm  
4. Use AI template  
5. Select a template and generate prompt  
6. Generate image successfully  
7. Click **Accept**

**Expected Result:**
- **Status** should change to **Accepted**
- **Kind** should correspond to whether *Try Agent Feedback* was used
- Acceptance behavior differs based on selection:
  - Accepting **one image**
  - Accepting **two images**

---

#### TC07: Manual flow history record

**Steps:**
1. Single mood generation  
2. Select from product catalog  
3. Enter a SKU and confirm  
4. Manual configuration  
5. Select a template (or manually enter the same prompt)  
6. Generate image  

**Expected Result:**
- **SKU**: Corresponding SKU is recorded  
- **Prompt Name**: Corresponding prompt name is recorded  
- **AI**: Gemini  
- **Status**: Complete  
- **Kind**: IMAGES_COMPLETED  
- **Used Prompt**: Manual input prompt is recorded  

---

#### TC08: Upload image and generate

**Steps:**
1. Upload an image  
2. Manually enter a prompt and generate  

**Expected Result:**
- **SKU**: User ID  
- **Prompt Name**: `own_prompt`

---

#### TC09: Accept function on History panel

**Steps:**
1. Generate images (preferably using agentic flow to produce two images)

**Expected Result:**
- **Single image**:  
  - Click **Accept**, status changes to **Accepted**
- **Two images**:  
  - Checkboxes should be displayed  
  - User can select one or more images and accept

---
#### TC10: Difference in "Improve Image" behavior between Agentic Flow and Manual Flow

**Steps:**
1. Generate images using **AI Template** and click **Improve Image**  
2. Generate images using **Manual Configuration** and click **Improve Image**

**Expected Result:**
- **AI Template (Agentic Flow)**:  
  - Only **one history log** should be created for the image  
- **Manual Configuration**:  
  - **Two history logs** should be created:  
    1. One for the original image  
    2. One for the improved image
---

#### Unclear Part / Open Question

- When a log is **Rejected** or **Accepted** from the **History panel**,  
  what should happen to the corresponding **Chat record**?
  - Should the chat status sync with history?
  - Should the chat become read-only or display the final decision?




























  
