# IDOR Vulnerability Challenge - Product Review Edit
## OWASP Juice Shop - Final Project
### Web Security Course | Azrieli College of Engineering

**Student:** Tehila Raviv  
**Track:** B - Adding a challenge to Juice Shop  
**GitHub Repository:** https://github.com/Azrieli-College-of-Engineering/final-project-tehila-raviv

---

## 📁 Project Structure

**IMPORTANT: All project documentation is in the `PROJECT-DOCUMENTATION/` folder:**
```
PROJECT-DOCUMENTATION/
├── REPORT.pdf                          ← 2-page final report (START HERE)
├── REPORT.docx                         ← Same report in Word format
├── README.md                           ← This file
├── vulnerable-code/
│   ├── updateProductReviews.vulnerable.ts   ← Vulnerable backend (IDOR vulnerability)
│   └── product-details.component.html       ← Frontend with edit button
├── fixed-code/
│   └── updateProductReviews.fixed.ts        ← Secure backend (fix applied)
└── screenshots/                        ← Attack demonstration screenshots
    ├── 1-edit-button-visible.png
    ├── 2-edit-dialog-open.png
    ├── 3-exploit-success.png
    ├── 4-fix-403-error.png
    └── 5-own-review-edit-works.png
```

---

## 📝 Quick Summary

**Vulnerability:** IDOR (Insecure Direct Object Reference) in product review editing  
**Type:** OWASP A01:2021 - Broken Access Control  
**Impact:** Any authenticated user can edit any other user's product reviews

**What was added:**
1. Edit button visible on all reviews (frontend change)
2. Backend API accepts any review ID without ownership verification (vulnerability)
3. Authorization check added in fixed version (solution)

---

## 🎯 How to Review This Project

### Option 1: Read the Documentation (Recommended)
1. **Start with:** `PROJECT-DOCUMENTATION/REPORT.pdf` - Complete 2-page report
2. **View screenshots:** `PROJECT-DOCUMENTATION/screenshots/` - Attack demonstration
3. **Compare code:**
   - Vulnerable: `PROJECT-DOCUMENTATION/vulnerable-code/updateProductReviews.vulnerable.ts`
   - Fixed: `PROJECT-DOCUMENTATION/fixed-code/updateProductReviews.fixed.ts`

### Option 2: Run the Code
The main repository files have been modified:
- `routes/updateProductReviews.ts` - Currently contains the FIXED version
- `frontend/src/app/product-details/product-details.component.html` - Contains edit button

**To test the VULNERABLE version:**
```bash
# Replace the fix with vulnerable version
cp PROJECT-DOCUMENTATION/vulnerable-code/updateProductReviews.vulnerable.ts routes/updateProductReviews.ts
npm run build:server
npm start
# Follow exploitation steps in report
```

**To test the FIXED version:**
```bash
# Use current master branch (already contains fix)
npm start
# Try to edit another user's review → 403 Forbidden
```

---

## 🔍 Quick Exploitation Demo

**Setup:**
1. Register two users: `test1@test.com`, `test2@test.com`
2. Each user submits a product review

**Attack (with vulnerable version):**
1. Log in as test1
2. Click the edit button on test2's review
3. Change the review text
4. Review is successfully changed! (IDOR vulnerability confirmed)

**Defense (with fixed version):**
1. Same steps as above
2. Server returns: `403 Forbidden - You can only edit your own reviews`

---

## 📚 Additional Information

**Modified Files:**
- `routes/updateProductReviews.ts` (backend)
- `frontend/src/app/product-details/product-details.component.html` (frontend)

**Key Changes:**
- Added visible edit button for all reviews (frontend)
- Added authorization check: `author === logged-in user email` (backend fix)
- Returns 403 error when trying to edit others' reviews (backend fix)

**Sources:**
- OWASP Top 10 A01:2021
- PortSwigger IDOR Guide
- OWASP Juice Shop Repository

---
