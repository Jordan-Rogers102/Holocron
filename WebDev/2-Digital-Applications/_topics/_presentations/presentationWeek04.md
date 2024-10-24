# Welcome to Week 4

Focus: Resume Builder

---
# Resume Builder

Three components:
1. Creating Resume Entries
2. Editing Resume Entries
3. Displaying complete Resume

---

# Database

All the experience data will be stored in one table. 

![resumeERD](resumeERD.png)

`userID` is the current user's id from the `user` table.

note: Both work and education experience will be stored in one table, as they are both very similar data required.
The boolean `experienceWork` identifies it as work (true) or education (false).

---
# Code Updates

Model-View-Controller

A more complex version of the TODO app.

Creating:
- Templates (View),
- Database & `model.py` (Model)
- `app.py` & `forms.py` (Controller)

---
# Resume Build

![resumeBuildTemplateFormEntry](resumeBuildTemplateFormEntry.png)

---

# Resume Edit

![resumeEditPreview](resumeEditPreview.png)

---

# Resume Display

![resumeDisplayCardExample2](resumeDisplayCardExample2.png)

---
# Improvements?

What else goes on a resume?

![resumeExampleWikiCommons](resumeExampleGenerated.png)

note: - Personal information
	- Name
	- Contact Details
	- Photo?
- Referees
	- Name
	- Contact Details
What database changes would need to be made to support these additions?
---

# Questions?

If you have any questions, please ask!