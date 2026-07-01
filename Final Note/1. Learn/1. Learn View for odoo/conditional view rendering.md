হ্যাঁ, **Conditional Rendering** অবশ্যই Odoo 19-এ আছে। তবে Odoo 17/18/19-এ এর syntax আগের version (v16 এবং তার আগে)-এর তুলনায় পরিবর্তন হয়েছে। তাই অনেক পুরোনো tutorial দেখলে বিভ্রান্তি হতে পারে।

## Odoo 19-এ Conditional Rendering কোথায় ব্যবহার হয়?

```text
Views
│
├── readonly
├── invisible
├── required
├── groups
├── domain
├── context
├── attrs (❌ Removed in Odoo 17+)
└── decoration-* (List View)
```

---

# 1. Invisible

```xml
<field name="discount"
       invisible="state != 'draft'"/>
```

অর্থাৎ `state` যদি `draft` না হয়, তাহলে field hide হবে।

---

# 2. Readonly

```xml
<field name="amount"
       readonly="state == 'done'"/>
```

---

# 3. Required

```xml
<field name="reason"
       required="state == 'cancel'"/>
```

---

# 4. Groups

```xml
<field name="salary"
       groups="hr.group_hr_manager"/>
```

শুধু নির্দিষ্ট group-এর user দেখতে পারবে।

---

# 5. Button Visibility

```xml
<button
    name="action_confirm"
    type="object"
    string="Confirm"
    invisible="state != 'draft'"/>
```

---

# 6. Notebook Page

```xml
<page
    string="Finance"
    invisible="is_student"/>
```

---

# 7. Group

```xml
<group
    invisible="gender == 'male'">

    <field name="pregnancy_date"/>

</group>
```

---

# 8. Decoration (List View)

```xml
<list>

    <field name="state"
           decoration-success="state == 'done'"
           decoration-danger="state == 'cancel'"
           decoration-warning="state == 'draft'"/>

</list>
```

---

# 9. Domain (Conditional Records)

```xml
<field
    name="teacher_id"
    domain="[('department','=','CSE')]"/>
```

---

# 10. Context

```xml
<field
    name="student_id"
    context="{'default_state':'draft'}"/>
```

---

# ❌ Old Syntax (Odoo 16 পর্যন্ত)

```xml
<field
    name="discount"
    attrs="{'invisible':[('state','!=','draft')]}"/>
```

এটি **Odoo 17, 18, 19-এ আর ব্যবহার করা হয় না**।

---

# ✅ New Syntax (Odoo 17/18/19)

```xml
<field
    name="discount"
    invisible="state != 'draft'"/>
```

---

# Enterprise Project-এ সবচেয়ে বেশি ব্যবহৃত Conditional Features

```text
★★★★★

invisible

readonly

required

groups

domain

context

decoration-success

decoration-danger

decoration-warning
```

---

## Odoo 19 View Learning Checklist

```text
★★★★★ Basic Views
-------------------
Form
List
Kanban
Search

★★★★★ Form Layout
-------------------
Sheet
Group
Notebook
Page
Header
Footer
Button
Field
Label
Separator

★★★★★ Conditional Rendering
-------------------
invisible
readonly
required
groups
domain
context
decoration-*

★★★★★ Widgets
-------------------
statusbar
badge
priority
boolean_toggle
many2many_tags
image
email
phone
url
monetary
progressbar
html

★★★★★ Navigation
-------------------
Menu
Action
Window Action

★★★★★ Advanced
-------------------
Calendar
Graph
Pivot
Activity
Gantt
Chatter
```

**সংক্ষেপে:** হ্যাঁ, Conditional Rendering Odoo 19-এর একটি গুরুত্বপূর্ণ অংশ। তবে এখন `attrs` এবং `states`-এর বদলে `invisible`, `readonly`, `required` ইত্যাদি attribute-এ সরাসরি Python-style expression ব্যবহার করা হয়। এটা Odoo 17+ এর অন্যতম বড় পরিবর্তন।
