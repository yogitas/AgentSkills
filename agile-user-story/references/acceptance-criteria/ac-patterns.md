# ✅ Acceptance Criteria Patterns

Common AC patterns by story type.
Use these to seed better AC in your stories or validate agent output before refinement.

All AC is written **from the user's perspective** using Given/When/Then.

---

## 📝 Forms & Input

- Given I submit the form with all required fields empty, when I click submit, then I see inline validation errors on each required field
- Given I enter an invalid format (e.g. bad email), when I click submit, then I see a clear error message explaining the expected format
- Given I submit a valid form, when the action succeeds, then I see a success message and the form resets / I am redirected
- Given the form has unsaved changes, when I navigate away, then I am prompted to confirm before leaving

---

## 🔐 Authentication & Permissions

- Given I am not logged in, when I try to access a protected page, then I am redirected to the login page
- Given I am a read-only user, when I try to perform an edit action, then I see a message explaining I don't have permission
- Given my session has expired, when I try to take an action, then I am prompted to log in again without losing my context

---

## 🔔 Notifications & Feedback

- Given an action completes successfully, when I see the result, then a success notification appears and dismisses after [X] seconds
- Given an action fails, when I see the result, then I see an error message with a clear next step (retry, contact support, etc.)
- Given a background process is running, when I wait, then I see a loading indicator so I know something is happening

---

## 🔍 Search & Filtering

- Given I enter a search term, when results load, then only items matching the term are displayed
- Given my search returns no results, when the page loads, then I see an empty state with a suggestion (clear filters, try different term)
- Given I apply a filter, when I refresh the page, then my filter is preserved

---

## 📊 Lists & Tables

- Given there are more items than fit on one page, when I scroll or paginate, then I can access all items
- Given I sort a column, when the list updates, then items are correctly ordered by that column
- Given the list is empty, when I view the page, then I see an empty state that explains why and offers a next action

---

## 📁 File Upload

- Given I upload a supported file type, when the upload completes, then the file appears in the list with its name and size
- Given I upload an unsupported file type, when I select the file, then I see an error explaining accepted formats
- Given I upload a file that exceeds the size limit, when I select it, then I see a clear error with the size limit stated

---

## 🗑️ Destructive Actions (Delete / Remove)

- Given I click a delete action, when the confirmation appears, then I must explicitly confirm before the item is removed
- Given I confirm deletion, when the action completes, then the item is removed and I see a confirmation message
- Given deletion fails, when the error occurs, then the item is NOT removed and I see an error message

---

## 📱 Responsive / Mobile

- Given I am on a mobile viewport, when I view the page, then all key actions are accessible without horizontal scrolling
- Given I am on a touch device, when I interact with [component], then it responds correctly to touch gestures

---

## 💳 Payments & Transactions

- Given I submit a payment, when it is processing, then I see a loading state and cannot submit again
- Given a payment succeeds, when the confirmation loads, then I see a reference number and summary of what was paid
- Given a payment fails, when the error is returned, then I see a human-readable reason and a suggested next step (retry, use different method, contact support)

---

## 🔔 Email / Notification Triggers

- Given [triggering action], when it completes, then I receive an email confirmation within [X minutes]
- Given I have disabled email notifications, when [triggering action] occurs, then I do NOT receive an email
- Given the email is sent, when I open it, then the content accurately reflects the action that triggered it
