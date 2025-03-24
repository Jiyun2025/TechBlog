---
title: "📓Markdown Dictionary"
excerpt: "📍 Notice"

categories:
  - 📍 Notice
tags:
  - [Markdown, PRJ_25, Notice]

permalink: /📍 Notice/Markdown/

toc: true
toc_sticky: true

date: 2025-03-24
last_modified_at: 2025-03-24
---

# Markdown for writing blog 
---

## ✅ Introduction to Markdown

💡 Markdown is a lightweight markup language that allows you to write documents using simple syntax.  
It is widely used in GitHub, Jekyll blogs, and technical documentation.

---

## ✅ Headings

💡 Use `#` to create headings.  
The number of `#` symbols determines the heading level.

```markdown
# Heading 1

## Heading 2

### Heading 3

#### Heading 4

##### Heading 5

###### Heading 6
```

### 🔽 Output

> # Heading 1  
> ## Heading 2  
> ### Heading 3  
> #### Heading 4  
> ##### Heading 5  
> ###### Heading 6

---

## ✅ Horizontal Rule

💡 Use `---` or `***` to insert a horizontal divider.

```markdown
---
```

### 🔽 Output

---

---

## ✅ Text Styling

💡 Apply styles like bold, italic, and strikethrough to your text.

```markdown
This is the **bold** text, and this is the _italic_ text.  
Let's do ~~strikethrough~~.
```

### 🔽 Output

This is the **bold** text, and this is the _italic_ text.  
Let's do ~~strikethrough~~.

---

## ✅ Blockquotes

💡 Use `>` to create blockquotes.  
Helpful for highlighting important notes or references.

```markdown
> Don't forget to code your dream.
```

### 🔽 Output

> Don't forget to code your dream.

---

## ✅ Bullet List

💡 Use `-` or `*` to create unordered lists.  
Indent to create sub-items.

```markdown
Fruits:

- Apple
- Lemon
  - Orange
  - Grape
```

### 🔽 Output

Fruits:

- Apple
- Lemon
  - Orange
  - Grape

---

## ✅ Numbered List

💡 Use numbers followed by a dot to create ordered lists.  
Numbers don't have to be sequential — they'll be auto-numbered.

```markdown
Numbers:

1. First
2. Second
3. Third
```

### 🔽 Output

Numbers:

1. First  
2. Second  
3. Third

---

## ✅ Links

💡 Use `[text](URL)` format to create a hyperlink.

```markdown
Click [here](https://example.com/)
```

### 🔽 Output

Click [here](https://example.com/)

---

## ✅ Images

💡 Use `![alt text](image URL)` format to insert an image.

```markdown
![logo](/assets/images/meee.png)
```

### 🔽 Output

![man](/assets/images/meee.png)

---

## ✅ Tables

💡 Use `|` and `-` to create tables.  
You can align columns using the following syntax:

- :---: → center alignment  
- :--- → left alignment  
- ---: → right alignment

```markdown
| Header | CenterAligned | LeftAligned | RightAligned |
|--------|:-------------:|------------|-------------:|
| Cell1  |     Cell2     | Cell3      |       Cell4  |
| Cell1  |     Cell2     | Cell3      |       Cell4  |
```

### 🔽 Output

| Header | CenterAligned | LeftAligned | RightAligned |
|--------|:-------------:|------------|-------------:|
| Cell1  |     Cell2     | Cell3      |       Cell4  |
| Cell1  |     Cell2     | Cell3      |       Cell4  |

---

## ✅ Code Block

💡 Use triple backticks (```) to define a block of code.  
Specify the language for syntax highlighting.

```markdown
To print message in the console, use `console.log('your message')` and..
```

````markdown
```python
def hello():
    print("Hello, Markdown!")
```
````

### 🔽 Output

To print message in the console, use `console.log('your message')` and..

```python
def hello():
    print("Hello, Markdown!")
```

---

## ✅ Check List

💡 Use `- [ ]` for unchecked and `- [x]` for checked items.  
GitHub renders checkboxes you can interact with.

```markdown
- [x] Completed task
- [ ] Task in progress
- [ ] Task to be added
```

### 🔽 Output

- [x] Completed task  
- [ ] Task in progress  
- [ ] Task to be added
"""

### ✅ Lists - Unordered list

```
- Item
* Item
+ Item
```

### 🔽 Output
- Item
* Item
+ Item

### ✅ Nested Lists 

```
- Item 1
  - Subitem 1
    - Sub-subitem
```
### 🔽 Output

- Item 1
  - Subitem 1
    - Sub-subitem
   
      
### ✅ Collabsible section
```
<details>
  <summary>Click to expand</summary>

  Hidden content goes here!

</details>
```

### 🔽 Output
<details>
  <summary>Click to expand</summary>

  Hidden content goes here!

</details>

### ✅ Mentions & References (GitHub specific)
@username
#issue-number




### ✅Jiyun's Quick Emoji Dictionary

⚠️ Important: This action is irreversible.  
🚨 Warning: Make sure to back up your data.  
❗Caution: This feature is deprecated.  
🔴 Critical: Immediate attention required.  
✅ Done: All tasks completed.  
🟢 Success: Your code has passed all tests.  
🎉 Congratulations: You did it!  
👏 Well done: Great job on finishing this!  
🔍 Note: This step is optional but recommended.  
ℹ️ Info: For more details, check the documentation.  
💡 Tip: You can use shortcuts to speed things up.  
📌 Reminder: Don’t forget to commit your changes.  
⏰ Deadline: Submit by March 31st.  
🗓️ Schedule: Meeting every Monday at 10 AM.  
📆 ETA: Expected release is Q2 2025.  
🛠️ Dev Note: Still under construction.  
⚙️ Config: Update your settings in `config.yaml`.  
💾 Save: Remember to save your work frequently.  
🧪 Test: Run unit tests before pushing changes.  
🚧 Work in Progress: Feature not yet complete.  
🔄 In Review: Awaiting feedback from team.  
📝 Draft: Not finalized yet.  
📁 Folder: Located in `/src/utils/`  
📄 File: See `README.md` for instructions.  
🧱 Code Block: Use triple backticks for blocks.  
⬇️ Scroll down for more info  
🔝 Back to top  
➡️ Next Step  
⬅️ Previous Step  
🙋 Question: Can someone clarify this?  
👥 Team: Assigned to @username and @teammember  
📣 Announcement: Sprint starts next week!  
📬 Contact: Email us at support@example.com  
