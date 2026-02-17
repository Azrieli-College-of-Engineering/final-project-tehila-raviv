\# IDOR Vulnerability Challenge - Product Review Edit

\## OWASP Juice Shop - Final Project

\### Web Security Course | Azrieli College of Engineering

\*\*Student:\*\* Tehila Raviv  

\*\*Track:\*\* B - Adding a challenge to Juice Shop



---



\## Project Overview

This project adds an IDOR (Insecure Direct Object Reference) vulnerability 

challenge to the OWASP Juice Shop application. The challenge demonstrates 

how an attacker can edit other users' product reviews by manipulating 

review IDs in API requests.



---



\## Vulnerability Description

\*\*Type:\*\* IDOR - Insecure Direct Object Reference  

\*\*Location:\*\* `routes/updateProductReviews.ts`  

\*\*OWASP Category:\*\* A01:2021 - Broken Access Control



The vulnerability exists because the update review API endpoint accepts 

any review ID without verifying that the review belongs to the 

authenticated user.



---



\## Files Modified

1\. `routes/updateProductReviews.ts` - Backend API (vulnerable + fixed)

2\. `frontend/src/app/product-details/product-details.component.html` - Added Edit button



---



\## How to Reproduce the Vulnerability



\### Setup:

1\. Clone and run Juice Shop locally

2\. Register two test users:

&nbsp;  - test1@test.com / Test123!

&nbsp;  - test2@test.com / Test123!

3\. Add a product review as each user



\### Exploit Steps:

1\. Log in as test1@test.com

2\. Open any product with reviews

3\. Click the Edit (pencil) button on test2's review

4\. Change the review text and click Submit

5\. Review is successfully changed - IDOR confirmed!



\### OR via Browser Console:

```javascript

fetch('/rest/products/reviews', {

&nbsp; method: 'PATCH',

&nbsp; headers: {

&nbsp;   'Content-Type': 'application/json',

&nbsp;   'Authorization': 'Bearer ' + localStorage.getItem('token')

&nbsp; },

&nbsp; body: JSON.stringify({

&nbsp;   id: 'TARGET\_REVIEW\_ID',

&nbsp;   message: 'Hacked review!'

&nbsp; })

}).then(r => r.json()).then(console.log)

```



---



\## The Fix

Added authorization check in `routes/updateProductReviews.ts`:

\- Only update review if author matches logged-in user email

\- Returns 403 Forbidden if ownership check fails



---



\## Project Structure

```

PROJECT-DOCUMENTATION/

├── README.md                    

├── vulnerable-code/

│   ├── updateProductReviews.vulnerable.ts  

│   └── product-details.component.html      

├── fixed-code/

│   └── updateProductReviews.fixed.ts       

└── screenshots/                            

```

