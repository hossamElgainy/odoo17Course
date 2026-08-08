# Odoo 17 Development — Complete Professional Documentation
# Asset Maintenance Management

> **Odoo 17 Senior Developer / Mentor Documentation**
>
> الغرض من الـ README دي إنك تتعلم Odoo 17 من الصفر لحد مستوى Professional من خلال مشروع عملي واحد: **Asset Maintenance Management**.
>
> التركيز هنا مش على حفظ Syntax، لكن على فهم:
>
> - ليه الـ Concept موجود؟
> - المشكلة اللي بيحلها؟
> - إمتى أستخدمه؟
> - إمتى ماستخدموش؟
> - إيه اللي بيحصل داخل Odoo؟
> - إزاي أكتبه بطريقة Production-ready؟
> - إيه الـ Common Mistakes والـ Errors؟
> - إزاي أعمل Debugging وRefactoring؟
>
> كل أمثلة الـ Backend والـ ORM والـ Security والـ Reports والـ APIs والـ OWL هتتبني على نفس المشروع.

---

# 📌 Table of Contents

1. [Project Overview](#1-project-overview)
2. [Learning Methodology](#2-learning-methodology)
3. [Module Fundamentals](#3-module-fundamentals)
4. [Models & Fields](#4-models--fields)
5. [ORM](#5-orm)
6. [Relations](#6-relations)
7. [Business Logic](#7-business-logic)
8. [Views](#8-views)
9. [Actions & Menus](#9-actions--menus)
10. [Security](#10-security)
11. [Advanced Odoo](#11-advanced-odoo)
12. [Reports](#12-reports)
13. [Controllers & APIs](#13-controllers--apis)
14. [OWL / Frontend](#14-owl--frontend)
15. [Performance](#15-performance)
16. [Testing](#16-testing)
17. [Professional Development](#17-professional-development)
18. [Production Checklist](#18-production-checklist)
19. [Final Project Roadmap](#19-final-project-roadmap)

---

# 1. Project Overview

## 1.1 فكرة المشروع

إحنا هنبني نظام اسمه:

**Asset Maintenance Management**

النظام ده مسؤول عن إدارة أصول الشركة ومتابعة صيانتها.

مثلاً الشركة عندها:

- Laptops
- Printers
- Servers
- Air Conditioners
- Network Devices
- Vehicles
- Production Machines

كل Asset له:

- Category
- Code
- Purchase information
- Current state
- Location
- Responsible person
- Maintenance history

ولو حصلت مشكلة:

```text
Asset
  ↓
Maintenance Request
  ↓
Approval
  ↓
Technician Assignment
  ↓
Maintenance
  ↓
Spare Parts
  ↓
Completion
  ↓
Maintenance History
```

---

## 1.2 Models الرئيسية

هنبني Models زي:

```text
asset.asset
asset.category
asset.technician
asset.maintenance.request
asset.maintenance.request.line
asset.spare.part
asset.asset.transfer
```

---

## 1.3 Maintenance Request Workflow

```text
Draft
   ↓
Submitted
   ↓
Approved
   ↓
In Progress
   ↓
Done
```

وفي أي مرحلة مناسبة ممكن:

```text
Cancelled
```

مثال Business Flow:

```text
User creates request
        ↓
Submit
        ↓
Supervisor approves
        ↓
Technician assigned
        ↓
Technician starts work
        ↓
Spare parts consumed
        ↓
Technician completes work
        ↓
Request becomes Done
        ↓
Asset maintenance history updated
```

---

## 1.4 Roles

```text
User
  ↓
Technician
  ↓
Supervisor
  ↓
Manager
  ↓
Admin
```

مثلاً:

| Feature | User | Technician | Supervisor | Manager | Admin |
|---|---:|---:|---:|---:|---:|
| View Assets | ✓ | ✓ | ✓ | ✓ | ✓ |
| Create Asset | ✗ | ✗ | ✗ | ✓ | ✓ |
| Edit Asset | ✗ | ✗ | ✗ | ✓ | ✓ |
| Retire Asset | ✗ | ✗ | ✗ | ✓ | ✓ |
| Create Request | ✓ | ✓ | ✓ | ✓ | ✓ |
| Submit Request | ✓ | ✓ | ✓ | ✓ | ✓ |
| Approve Request | ✗ | ✗ | ✓ | ✓ | ✓ |
| Assign Technician | ✗ | ✗ | ✓ | ✓ | ✓ |
| Start Work | ✗ | ✓ | ✓ | ✓ | ✓ |
| Complete Work | ✗ | ✓ | ✓ | ✓ | ✓ |

---

# 2. Learning Methodology

كل Topic في الـ Documentation دي بيتشرح بنفس الطريقة:

1. **يعني إيه؟**
2. **المشكلة اللي بيحلها**
3. **إمتى أستخدمه؟**
4. **إمتى ماستخدموش؟**
5. **Syntax الأساسي**
6. **Example بسيط**
7. **Example من Asset Maintenance**
8. **شرح الكود بالتفصيل**
9. **إيه اللي بيحصل داخل Odoo؟**
10. **Common Mistakes**
11. **Errors محتملة وحلها**
12. **Best Practices**
13. **Production Example**
14. **Task للتطبيق**

المهم إن أي Concept جديد يتربط بالـ Architecture بتاعة المشروع.

---

# 3. Module Fundamentals

## 3.1 يعني إيه Module؟

الـ Module هو Package بيضيف Business Functionality جديدة لـ Odoo.

مثلاً:

```text
sale
purchase
stock
account
```

وإحنا:

```text
asset_maintenance
```

الـ Module ممكن يحتوي:

```text
Python
XML
CSV
JavaScript
CSS
QWeb
Security
Data
Tests
```

---

## 3.2 Module Structure

Production-like structure:

```text
asset_maintenance/
│
├── __init__.py
├── __manifest__.py
│
├── models/
│   ├── __init__.py
│   ├── asset.py
│   ├── asset_category.py
│   ├── technician.py
│   ├── maintenance_request.py
│   ├── maintenance_request_line.py
│   ├── spare_part.py
│   └── asset_transfer.py
│
├── views/
│   ├── asset_views.xml
│   ├── asset_category_views.xml
│   ├── technician_views.xml
│   ├── maintenance_request_views.xml
│   ├── spare_part_views.xml
│   ├── asset_transfer_views.xml
│   └── menus.xml
│
├── security/
│   ├── security.xml
│   └── ir.model.access.csv
│
├── data/
│   ├── sequence.xml
│   ├── cron.xml
│   └── mail_template.xml
│
├── reports/
│   ├── maintenance_report.xml
│   └── maintenance_report_templates.xml
│
├── wizard/
│   ├── __init__.py
│   └── asset_transfer_wizard.py
│
├── controllers/
│   ├── __init__.py
│   └── api.py
│
├── static/
│   └── src/
│       ├── js/
│       ├── xml/
│       └── css/
│
├── tests/
│   ├── __init__.py
│   ├── test_asset.py
│   ├── test_maintenance.py
│   └── test_security.py
│
└── demo/
    └── demo.xml
```

مش لازم كل folder يكون موجود من أول يوم.

---

## 3.3 `__manifest__.py`

هو بطاقة تعريف الـ Module بالنسبة لـ Odoo.

```python
{
    'name': 'Asset Maintenance Management',
    'version': '17.0.1.0.0',
    'summary': 'Asset and Maintenance Management System',

    'description': """
        Manage company assets,
        maintenance requests,
        technicians,
        spare parts and transfers.
    """,

    'author': 'Your Company',
    'category': 'Operations',

    'depends': [
        'base',
        'mail',
    ],

    'data': [
        'security/security.xml',
        'security/ir.model.access.csv',
        'data/sequence.xml',
        'views/asset_views.xml',
        'views/asset_category_views.xml',
        'views/technician_views.xml',
        'views/maintenance_request_views.xml',
        'views/spare_part_views.xml',
        'views/menus.xml',
        'reports/maintenance_report.xml',
    ],

    'assets': {
        'web.assets_backend': [
            'asset_maintenance/static/src/js/**/*.js',
            'asset_maintenance/static/src/xml/**/*.xml',
            'asset_maintenance/static/src/css/**/*.css',
        ],
    },

    'installable': True,
    'application': True,
}
```

### أهم الحقول

#### `name`

اسم الـ Module الظاهر للمستخدم.

```python
'name': 'Asset Maintenance Management'
```

الـ technical name هو اسم الـ folder:

```text
asset_maintenance
```

---

#### `version`

إصدار الـ Module.

```python
'version': '17.0.1.0.0'
```

---

#### `depends`

الـ Odoo Modules اللي لازم تكون متوفرة قبل Module بتاعنا.

```python
'depends': [
    'base',
    'mail',
]
```

لو بنستخدم:

```python
_inherit = ['mail.thread', 'mail.activity.mixin']
```

لازم `mail` تكون dependency.

---

#### `data`

ملفات XML/CSV التي يتم تحميلها.

```python
'data': [
    'security/security.xml',
    'security/ir.model.access.csv',
    'views/asset_views.xml',
]
```

الترتيب مهم لما ملف يعتمد على records اتعملت في ملف سابق.

---

#### `demo`

بيانات تجريبية.

```python
'demo': [
    'demo/demo.xml',
]
```

مفيدة في development/testing، لكن لا نعتمد عليها كـ business configuration في Production.

---

#### `assets`

ملفات Frontend:

```python
'assets': {
    'web.assets_backend': [
        'asset_maintenance/static/src/js/**/*.js',
        'asset_maintenance/static/src/xml/**/*.xml',
        'asset_maintenance/static/src/css/**/*.css',
    ],
}
```

---

#### `installable`

```python
'installable': True
```

---

#### `application`

```python
'application': True
```

---

## 3.4 `__init__.py`

Root:

```python
from . import models
from . import controllers
```

---

## 3.5 `models/__init__.py`

```python
from . import asset
from . import asset_category
from . import technician
from . import maintenance_request
from . import maintenance_request_line
from . import spare_part
from . import asset_transfer
```

لو نسيت import، الملف ممكن يكون موجود لكن الـ model لا يتم تحميله.

---

## 3.6 Data Files

Data files هي XML/CSV files Odoo بيعملها load.

أمثلة:

```text
security/security.xml
security/ir.model.access.csv
data/sequence.xml
data/cron.xml
data/mail_template.xml
views/*.xml
reports/*.xml
```

الفرق المهم:

- **Data** = records/configuration يتم تحميلها.
- **Code** = Python business logic.
- **Views** = UI definitions.
- **Security** = access control.

---

## 3.7 Assets

Assets هي ملفات frontend اللي Odoo بيجمعها في asset bundles.

أمثلة:

```text
static/src/js
static/src/xml
static/src/css
```

Backend bundle:

```python
'web.assets_backend'
```

وده مهم للـ OWL والـ custom dashboards والـ client actions.

---

## 3.8 Module Loading Flow

بشكل مبسط:

```text
Odoo
 ↓
Read manifest
 ↓
Resolve dependencies
 ↓
Load Python modules
 ↓
Register models
 ↓
Load XML/CSV data
 ↓
Load security/views/actions
 ↓
Build frontend assets
```

---

## 3.9 Common Errors

### File not found

```text
FileNotFoundError
```

غالباً path في manifest غلط.

### Model doesn't exist

غالباً:

```python
from . import model_file
```

ناقص.

### View not found

ممكن XML مش مضاف في `data`.

### External ID not found

غالباً record اتستخدم قبل ما يتعمل، أو module dependency ناقصة، أو XML ID غلط.

---

## 3.10 Task

أنشئ:

```text
asset_maintenance/
├── __init__.py
├── __manifest__.py
└── models/
    ├── __init__.py
    └── asset.py
```

واعمل أول model:

```python
from odoo import models, fields


class Asset(models.Model):
    _name = 'asset.asset'
    _description = 'Company Asset'

    name = fields.Char(
        string='Asset Name',
        required=True,
    )
```

---

# 4. Models & Fields

## 4.1 يعني إيه Model؟

الـ Model هو تمثيل Business Entity داخل Odoo.

مثلاً:

```text
Asset
Technician
Maintenance Request
Spare Part
```

كل واحد ممكن يبقى Model.

---

## 4.2 المشكلة اللي بيحلها

بدل ما تكتب SQL لكل حاجة، Odoo بيديك ORM layer.

```python
self.env['asset.asset'].search(...)
```

بدل:

```sql
SELECT ...
```

وده بيساعد في:

- Security
- Relationships
- Business Logic
- Transactions
- ORM abstraction
- Reusability

---

## 4.3 `_name`

```python
class Asset(models.Model):
    _name = 'asset.asset'
```

ده الـ technical model name.

بعدها:

```python
self.env['asset.asset']
```

---

## 4.4 `_description`

```python
_description = 'Company Asset'
```

وصف للـ model.

مفيد للوضوح والـ metadata.

---

## 4.5 `_rec_name`

Odoo محتاج يعرف يعرض إيه كاسم للrecord في Many2one وغيرها.

مثلاً:

```python
_rec_name = 'asset_code'
```

لو عندنا:

```python
asset_code = fields.Char(required=True)
name = fields.Char()
```

الـ Many2one ممكن يعرض `asset_code`.

---

# 4.6 Fields

## Char

```python
name = fields.Char(
    string='Asset Name',
    required=True,
)
```

للنصوص القصيرة.

استخدمه في:

- Name
- Code
- Serial Number

---

## Text

```python
description = fields.Text()
```

للنصوص الطويلة.

---

## Integer

```python
quantity = fields.Integer()
```

للقيم الصحيحة.

---

## Float

```python
unit_cost = fields.Float()
```

للقيم العشرية.

---

## Boolean

```python
active = fields.Boolean(default=True)
```

لـ flags.

---

## Date

```python
purchase_date = fields.Date()
```

للتاريخ فقط.

---

## Datetime

```python
start_datetime = fields.Datetime()
```

للتاريخ والوقت.

---

## Selection

```python
state = fields.Selection(
    [
        ('draft', 'Draft'),
        ('submitted', 'Submitted'),
        ('approved', 'Approved'),
        ('in_progress', 'In Progress'),
        ('done', 'Done'),
        ('cancelled', 'Cancelled'),
    ],
    default='draft',
)
```

مناسب للـ state machine.

---

## Binary

```python
document = fields.Binary()
```

للملفات أو البيانات الثنائية.

---

# 4.7 Field Attributes

## `required`

```python
name = fields.Char(required=True)
```

معناه المستخدم لازم يدخل قيمة.

لكن مهم:

> `required=True` مش بديل عن Business Validation.

---

## `readonly`

```python
seq = fields.Char(readonly=True)
```

يمنع التعديل من الـ UI في الظروف المعتادة، لكن لا تعتبره Security mechanism.

---

## `default`

```python
state = fields.Selection(
    [...],
    default='draft',
)
```

ممكن:

```python
request_date = fields.Date(default=fields.Date.today)
```

---

## `copy`

بيحدد هل field يتنسخ لما record يتعمل لها duplicate.

```python
seq = fields.Char(copy=False)
```

مثلاً sequence unique، غالباً لا تريد نسخه.

---

## `index`

```python
asset_code = fields.Char(index=True)
```

مفيد للحقول اللي بيحصل عليها search/filter بكثرة.

لكن ما تعملش index لكل field بدون سبب.

---

## `tracking`

```python
state = fields.Selection(
    [...],
    tracking=True,
)
```

مع `mail.thread`، التغيير يظهر في Chatter.

---

# 4.8 Asset Model

```python
class Asset(models.Model):
    _name = 'asset.asset'
    _description = 'Company Asset'
    _rec_name = 'name'

    name = fields.Char(
        string='Asset Name',
        required=True,
        index=True,
    )

    asset_code = fields.Char(
        string='Asset Code',
        required=True,
        copy=False,
        index=True,
    )

    description = fields.Text()

    purchase_cost = fields.Float()

    purchase_date = fields.Date()

    active = fields.Boolean(
        default=True,
    )

    state = fields.Selection(
        [
            ('draft', 'Draft'),
            ('running', 'Running'),
            ('broken', 'Broken'),
            ('retired', 'Retired'),
        ],
        default='draft',
        tracking=True,
    )
```

---

# 4.9 Validation

لو `purchase_cost` لا يجوز تكون سالبة:

```python
from odoo import api


@api.constrains('purchase_cost')
def _check_purchase_cost(self):
    for record in self:
        if record.purchase_cost < 0:
            raise ValidationError(
                'Purchase cost cannot be negative.'
            )
```

الفكرة:

> Field attribute مناسب للـ structural requirement، لكن business rule تحتاج validation.

---

# 4.10 Common Mistakes

### استخدام Float لكل الأرقام

لو quantity لازم تكون integer، استخدم Integer.

### `readonly=True` على security

الـ readonly في view/field مش Security.

### `required=True` مع Business Rule معقد

اعمل constraint.

### index على كل fields

ده ممكن يزيد تكلفة الكتابة والتخزين بدون فائدة.

---

# 4.11 Production Best Practice

اختار field type حسب معنى البيانات، مش حسب شكلها.

مثلاً:

```text
Asset Code       → Char
Purchase Cost    → Float
Purchase Date    → Date
Maintenance Time → Datetime
State            → Selection
Active           → Boolean
Description      → Text
```

---

# 4.12 Task

طوّر `asset.asset` ليحتوي على:

- Name
- Asset Code
- Description
- Purchase Cost
- Purchase Date
- Active
- State

وبعدين اعمل validation تمنع `purchase_cost < 0`.

---

# 5. ORM

## 5.1 يعني إيه ORM؟

ORM = Object Relational Mapping.

بمعنى إنك بتتعامل مع Database records كـ Python objects/recordsets بدل كتابة SQL في كل business operation.

```text
Python Model
      ↓
     ORM
      ↓
PostgreSQL
```

---

# 5.2 `env`

الـ environment بيوفر access للـ:

- Models
- Current user
- Context
- Company
- Database cursor

مثال:

```python
assets = self.env['asset.asset']
```

ده معناه:

> هاتلي model `asset.asset` من الـ current Odoo environment.

---

## Current User

```python
self.env.user
```

---

## Current Company

```python
self.env.company
```

---

## Context

```python
self.env.context
```

---

# 5.3 Recordsets

لما تعمل:

```python
assets = self.env['asset.asset'].search([])
```

`assets` مش Python list عادية.

ده **Recordset**.

ممكن يحتوي:

```text
0 records
1 record
100 records
```

---

# 5.4 `create()`

```python
asset = self.env['asset.asset'].create({
    'name': 'Laptop 01',
    'asset_code': 'AST-001',
})
```

`create()` بيعمل record جديد.

### داخل Odoo

```text
Python
 ↓
ORM
 ↓
Access checks
 ↓
create overrides
 ↓
Defaults / conversions
 ↓
Database INSERT
 ↓
Record returned
```

---

# 5.5 Batch Create

Production best practice:

بدل:

```python
for vals in values:
    self.env['asset.asset'].create(vals)
```

لو عندك كمية كبيرة، استخدم batch creation حسب السيناريو والـ API المناسب.

وفي overrides لازم تراعي إن عمليات create ممكن تتعامل مع مجموعة records/values.

---

# 5.6 `write()`

```python
asset.write({
    'state': 'broken',
})
```

لتعديل records.

لو:

```python
assets.write({
    'state': 'retired',
})
```

ممكن تعدل كل records في recordset مرة واحدة.

---

# 5.7 `unlink()`

```python
asset.unlink()
```

بيحذف record.

لكن Production systems غالباً محتاجة business policy تمنع الحذف لبعض records.

مثلاً Asset لها Maintenance History لا يفضل حذفها عشوائياً.

---

# 5.8 `search()`

```python
assets = self.env['asset.asset'].search([
    ('state', '=', 'broken'),
])
```

---

# 5.9 `search_count()`

```python
count = self.env['asset.asset'].search_count([
    ('state', '=', 'broken'),
])
```

مفيد لما محتاج العدد فقط.

---

# 5.10 `browse()`

```python
asset = self.env['asset.asset'].browse(asset_id)
```

مهم تفهم إن `browse()` مش معناها بالضرورة إنه نفذ SELECT فوراً لكل field.

هو بيعمل recordset مبني على IDs، والقراءة الفعلية للبيانات بتحصل عند الحاجة.

---

# 5.11 `read()`

```python
assets.read([
    'name',
    'state',
])
```

بيرجع data representation مناسبة لعمليات low-level/serialization في بعض الحالات.

لكن في business code غالباً التعامل مع recordsets أفضل.

---

# 5.12 `search_read()`

```python
assets = self.env['asset.asset'].search_read(
    [('state', '=', 'broken')],
    ['name', 'asset_code', 'state'],
)
```

مفيد في بعض data retrieval scenarios لما عايز search + read.

لكن لا تستخدمه كقاعدة عامة بدل ORM recordsets في كل business logic.

---

# 5.13 `mapped()`

```python
names = assets.mapped('name')
```

لو عندك:

```text
Asset 1
Asset 2
Asset 3
```

هترجع values الخاصة بالـ field.

وممكن تستخدم relational paths:

```python
technicians = requests.mapped('technician_id')
```

---

# 5.14 `filtered()`

```python
broken_assets = assets.filtered(
    lambda asset: asset.state == 'broken'
)
```

مهم تعرف إن filtering في Python مش نفس filtering في Database.

لو dataset ضخم، الأفضل domain على database:

```python
self.env['asset.asset'].search([
    ('state', '=', 'broken')
])
```

---

# 5.15 `sorted()`

```python
assets = assets.sorted(
    key=lambda asset: asset.purchase_date
)
```

---

# 5.16 `ensure_one()`

لو method لازم تشتغل على record واحد:

```python
def action_start(self):
    self.ensure_one()
```

لو method اتنفذت على أكتر من record هتطلع exception.

استخدمها لما business operation منطقيًا single-record.

ما تستخدمهاش لمجرد العادة.

---

# 5.17 Domains

Domain هو filter expression.

```python
[
    ('state', '=', 'broken')
]
```

مثال:

```python
[
    ('state', '=', 'broken'),
    ('purchase_cost', '>', 1000),
]
```

ده AND.

OR باستخدام `|`:

```python
[
    '|',
    ('state', '=', 'broken'),
    ('state', '=', 'retired'),
]
```

---

# 5.18 Context

Context dictionary بيمرر metadata للعملية.

مثلاً:

```python
self.with_context(
    from_maintenance=True
)
```

وبعدين:

```python
if self.env.context.get('from_maintenance'):
    ...
```

Context مناسب لتغيير behavior بطريقة عامة.

لكن ما تستخدموش كبديل لكل business field.

---

# 5.19 `sudo()`

```python
self.env['asset.asset'].sudo().search([])
```

بيشغل العملية بصلاحيات superuser-like environment.

لكن:

> `sudo()` مش "حل لأي access error".

استخدامه ممكن يتجاوز security checks.

مثلاً لو API endpoint بيستخدم `sudo()` بدون تصميم أمني، ممكن expose records للمستخدمين الغلط.

---

# 5.20 Common ORM Mistakes

### N+1 queries

```python
for request in requests:
    print(request.technician_id.name)
```

لو البيانات مش prefetched بشكل مناسب، ممكن تسبب query patterns غير فعالة.

### استخدام SQL بدون داعي

أغلب business operations المفروض تبدأ بالـ ORM.

### `sudo()` بدون فهم

ممكن يعمل security vulnerability.

### `filtered()` على آلاف records

لو filter ممكن يتعمل Domain، اعمله في database.

---

# 5.21 Task

اعمل methods:

```python
get_broken_assets()
get_asset_count()
get_asset_by_code()
```

واستخدم:

- `search`
- `search_count`
- `browse`
- `mapped`

---

# 6. Relations

## 6.1 Many2one

Asset Category عندها Assets كتير:

```text
Category
   │
   ├── Asset 1
   ├── Asset 2
   └── Asset 3
```

في Asset:

```python
category_id = fields.Many2one(
    'asset.category',
    string='Category',
    required=True,
)
```

ده أهم relation غالباً في Odoo.

---

## 6.2 One2many

Maintenance Request لها Spare Part Lines كتير:

```text
Maintenance Request
   ├── Line 1
   ├── Line 2
   └── Line 3
```

```python
request_line_ids = fields.One2many(
    'asset.maintenance.request.line',
    'request_id',
)
```

والـ inverse:

```python
request_id = fields.Many2one(
    'asset.maintenance.request',
)
```

---

## 6.3 Many2many

مثلاً Request ممكن تحتاج أكتر من Technician والعكس.

```python
technician_ids = fields.Many2many(
    'asset.technician',
    string='Technicians',
)
```

---

## 6.4 Related Fields

مثلاً Spare Part Line:

```python
unit_cost = fields.Float(
    related='spare_part_id.unit_cost',
)
```

القيمة جاية من:

```text
line
 ↓
spare_part_id
 ↓
unit_cost
```

---

## 6.5 `ondelete`

أمثلة:

```python
ondelete='cascade'
```

```python
ondelete='restrict'
```

```python
ondelete='set null'
```

اختيارها business decision.

مثلاً Maintenance Request Line لا معنى لها بدون Request، فـ cascade ممكن يكون مناسب.

لكن Asset لا يجب حذفها لمجرد حذف Category، لذلك restrict قد يكون أكثر أماناً حسب التصميم.

---

# 6.6 Relation Tables

Many2many يحتاج relation table في database.

Odoo ممكن يديرها تلقائياً أو تحدد تفاصيلها في الحالات المتقدمة.

---

# 6.7 Command Syntax

في Odoo 17 بنستخدم `fields.Command` للتعامل مع One2many/Many2many.

مثلاً:

```python
from odoo import Command
```

إضافة:

```python
Command.create({
    'spare_part_id': part.id,
    'used_qty': 2,
})
```

ربط existing record:

```python
Command.link(part.id)
```

إلغاء link:

```python
Command.unlink(part.id)
```

استبدال الروابط:

```python
Command.set([part1.id, part2.id])
```

Clear:

```python
Command.clear()
```

دي أفضل من حفظ أرقام command tuples بشكل أعمى.

---

# 6.8 Asset Maintenance Example

```python
class MaintenanceRequest(models.Model):
    _name = 'asset.maintenance.request'

    asset_id = fields.Many2one(
        'asset.asset',
        required=True,
    )

    technician_id = fields.Many2one(
        'asset.technician',
    )

    request_line_ids = fields.One2many(
        'asset.maintenance.request.line',
        'request_id',
    )
```

---

# 6.9 Task

اعمل:

```text
Asset → Category
Maintenance Request → Asset
Maintenance Request → Technician
Maintenance Request → Spare Part Lines
Spare Part Line → Spare Part
```

---

# 7. Business Logic

## 7.1 Regular Methods

Method عادية:

```python
def action_submit(self):
    self.ensure_one()
    self.state = 'submitted'
```

مناسبة للـ business actions.

---

# 7.2 `@api.model`

مفيد methods لا تعتمد على current recordset كـ records محددة.

مثلاً:

```python
@api.model
def get_default_category(self):
    return self.env['asset.category'].search(
        [],
        limit=1,
    )
```

استخدمه لما method semantics مناسبة للعمل على model-level.

---

# 7.3 `@api.depends`

Computed field:

```python
total_cost = fields.Float(
    compute='_compute_total_cost',
)
```

```python
@api.depends(
    'maintenance_cost',
    'request_line_ids.subtotal',
)
def _compute_total_cost(self):
    for record in self:
        record.total_cost = (
            record.maintenance_cost
            + sum(record.request_line_ids.mapped('subtotal'))
        )
```

`@api.depends` بتقول للـ ORM:

> لو dependencies دي اتغيرت، computation لازم تتحدث.

---

# 7.4 Stored Computed Field

```python
total_cost = fields.Float(
    compute='_compute_total_cost',
    store=True,
)
```

الميزة:

- قيمة محفوظة في database.
- أفضل للـ search/grouping/indexing scenarios.

العيب:

- Odoo لازم يعيد حسابها عند dependencies change.
- ممكن يكون expensive لو computation معقد.

---

# 7.5 Inverse Method

لو computed field محتاج يكون editable بطريقة controlled:

```python
total_cost = fields.Float(
    compute='_compute_total_cost',
    inverse='_inverse_total_cost',
)
```

الـ inverse بيحدد إزاي التعديل على computed field يؤثر على underlying data.

ما تستخدموش إلا لو عندك semantic واضح.

---

# 7.6 `@api.constrains`

Business validation:

```python
@api.constrains('completion_date', 'request_date')
def _check_dates(self):
    for record in self:
        if (
            record.completion_date
            and record.completion_date < record.request_date
        ):
            raise ValidationError(
                'Completion date cannot be before request date.'
            )
```

---

# 7.7 `@api.onchange`

بيشتغل في UI form لما field يتغير.

مثلاً:

```python
@api.onchange('asset_id')
def _onchange_asset_id(self):
    if self.asset_id:
        self.description = (
            f'Maintenance for {self.asset_id.name}'
        )
```

مهم جدًا:

> `onchange` مش Security ولا server-side business validation.

لو request اتعملت عن طريق API/import/backend code، onchange مش شرط يحصل.

---

# 7.8 State Machines

Request:

```text
draft
submitted
approved
in_progress
done
cancelled
```

بدل إن أي method تغير state لأي قيمة:

```python
self.state = 'done'
```

اعمل business transition:

```python
def action_submit(self):
    for record in self:
        if record.state != 'draft':
            raise UserError(
                'Only draft requests can be submitted.'
            )
        record.state = 'submitted'
```

---

# 7.9 `super()`

لو بتعمل inheritance:

```python
def write(self, vals):
    result = super().write(vals)
    # custom logic
    return result
```

`super()` مهم عشان تحافظ على behavior الأصلي.

---

# 7.10 Override `create()`

مثلاً sequence:

```python
@api.model_create_multi
def create(self, vals_list):
    for vals in vals_list:
        if vals.get('seq') in (False, 'New'):
            vals['seq'] = self.env['ir.sequence'].next_by_code(
                'asset.maintenance.request'
            ) or 'New'

    return super().create(vals_list)
```

ليه `api.model_create_multi`؟

عشان تحافظ على batch create compatibility.

---

# 7.11 Override `write()`

مثلاً منع تغيير Asset بعد Done:

```python
def write(self, vals):
    for record in self:
        if record.state == 'done' and 'asset_id' in vals:
            raise UserError(
                'You cannot change the asset after completion.'
            )

    return super().write(vals)
```

---

# 7.12 Override `unlink()`

```python
def unlink(self):
    if any(record.state == 'done' for record in self):
        raise UserError(
            'Completed requests cannot be deleted.'
        )

    return super().unlink()
```

لكن في Production لازم تراجع business/security requirements قبل منع deletion.

---

# 7.13 Business Rule vs UI Rule

قاعدة مهمة:

```text
UI behavior
    ≠
Security
    ≠
Business validation
```

مثلاً:

```python
readonly=True
```

مش Security.

و:

```python
@api.onchange
```

مش server-side validation.

والـ business invariant الحقيقي يفضل enforced server-side.

---

# 7.14 Task

طبق:

- Submit
- Approve
- Start Work
- Complete
- Cancel

مع منع transitions الغلط.

---

# 8. Views

## 8.1 Form View

لعرض record واحدة وتعديلها.

```xml
<record id="asset_view_form" model="ir.ui.view">
    <field name="name">asset.asset.form</field>
    <field name="model">asset.asset</field>
    <field name="arch" type="xml">
        <form>
            <sheet>
                <group>
                    <field name="name"/>
                    <field name="asset_code"/>
                    <field name="category_id"/>
                    <field name="state"/>
                </group>
            </sheet>
        </form>
    </field>
</record>
```

---

## 8.2 List View

لعدة records.

```xml
<list>
    <field name="asset_code"/>
    <field name="name"/>
    <field name="state"/>
</list>
```

---

## 8.3 Search View

```xml
<search>
    <field name="name"/>
    <field name="asset_code"/>

    <filter
        name="broken"
        string="Broken"
        domain="[('state', '=', 'broken')]"
    />
</search>
```

---

## 8.4 Kanban

مفيد لما cards أهم من rows.

مثلاً Maintenance Requests حسب state.

---

## 8.5 Calendar

مناسب للـ scheduled maintenance.

```text
scheduled_date
```

---

## 8.6 Graph

لـ analytics.

مثلاً:

```text
Maintenance Cost by Category
```

---

## 8.7 Pivot

لـ multidimensional analysis:

```text
Technician
Category
Month
State
Cost
```

---

## 8.8 Buttons

```xml
<button
    name="action_submit"
    type="object"
    string="Submit"
    class="btn-primary"
/>
```

`type="object"` يعني ينادي Python method.

---

## 8.9 Statusbar

```xml
<field
    name="state"
    widget="statusbar"
    statusbar_visible="draft,submitted,approved,in_progress,done"
/>
```

---

## 8.10 Smart Buttons

مثلاً Asset فيها:

```text
Maintenance Requests: 12
```

الـ smart button يفتح requests الخاصة بالـ Asset.

---

## 8.11 Domains in Views

مثلاً Technician domain:

```xml
<field
    name="technician_id"
    domain="[('active', '=', True)]"
/>
```

ده يفلتر choices في UI.

---

## 8.12 Context in Views

مثلاً:

```xml
<context>
    {'default_asset_id': active_id}
</context>
```

أو داخل action:

```xml
context="{'default_asset_id': active_id}"
```

---

## 8.13 XML Inheritance

بدل ما تنسخ view كاملة، extend existing view.

```xml
<record
    id="asset_view_form_inherit"
    model="ir.ui.view"
>
    <field name="inherit_id" ref="module.asset_view_form"/>
    <field name="arch" type="xml">
        <xpath expr="//field[@name='name']" position="after">
            <field name="asset_code"/>
        </xpath>
    </field>
</record>
```

---

## 8.14 XPath

أشهر positions:

```text
inside
before
after
replace
attributes
```

استخدم XPath stable قدر الإمكان.

---

## 8.15 View Priority

لما views متعددة ترث نفس view، priority ممكن تأثر على ترتيب تطبيق inheritance.

ما تعتمدش على priority كحل للفوضى.

الأفضل architecture واضحة وXPath واضح.

---

# 8.16 Common View Errors

### External ID not found

غالباً:

- module dependency ناقصة
- XML ID غلط
- record لم يتم تحميله

### Element cannot be located in parent view

XPath لا يطابق العنصر.

### Invalid XML

Syntax XML غلط.

---

# 8.17 Task

اعمل Asset:

- List
- Form
- Search
- Kanban

وبعدين Maintenance Request:

- Form
- List
- Search
- Statusbar
- Buttons

---

# 9. Actions & Menus

## 9.1 Window Action

```xml
<record id="asset_action" model="ir.actions.act_window">
    <field name="name">Assets</field>
    <field name="res_model">asset.asset</field>
    <field name="view_mode">list,form</field>
</record>
```

دي بتقول لـ Odoo:

> لما المستخدم يفتح Assets، افتح model ده بالviews دي.

---

## 9.2 Client Actions

Client action بتشغل frontend action عن طريق registry/tag.

مثلاً OWL Dashboard.

```xml
<record id="maintenance_dashboard_action"
        model="ir.actions.client">
    <field name="name">Maintenance Dashboard</field>
    <field name="tag">asset_maintenance.dashboard</field>
</record>
```

والـ JS:

```javascript
registry.category("actions").add(
    "asset_maintenance.dashboard",
    MaintenanceDashboard
);
```

---

## 9.3 Server Actions

Server Action ينفذ server-side logic من Odoo UI automation/actions.

مفيد لبعض configurable operations، لكن business-critical logic غالباً الأفضل يبقى Python methods واضحة في module.

---

## 9.4 Menus

```xml
<menuitem
    id="asset_root_menu"
    name="Asset Maintenance"
/>

<menuitem
    id="asset_menu"
    name="Assets"
    parent="asset_root_menu"
    action="asset_action"
/>
```

Hierarchy:

```text
Asset Maintenance
├── Assets
├── Maintenance
│   └── Requests
├── Spare Parts
├── Transfers
└── Reports
```

---

# 10. Security

## 10.1 أهم مبدأ

Odoo Security طبقات.

```text
User
 ↓
Groups
 ↓
ACL
 ↓
Record Rules
 ↓
Business Logic
```

---

## 10.2 Groups

```xml
<record id="group_asset_user" model="res.groups">
    <field name="name">Asset User</field>
</record>
```

Technician:

```xml
<record id="group_asset_technician" model="res.groups">
    <field name="name">Maintenance Technician</field>
    <field name="implied_ids"
           eval="[(4, ref('group_asset_user'))]"/>
</record>
```

معنى implied group:

```text
Technician
   ↓
Asset User permissions
```

---

## 10.3 ACL

ACL تحدد هل المجموعة مسموح لها تعمل:

```text
read
write
create
unlink
```

`ir.model.access.csv` مثال:

```csv
id,name,model_id:id,group_id:id,perm_read,perm_write,perm_create,perm_unlink
access_asset_user,asset user,model_asset_asset,asset_maintenance.group_asset_user,1,0,0,0
```

---

## 10.4 ACL vs Record Rule

دي من أهم الحاجات:

### ACL

بتجاوب:

> هل المجموعة عندها permission على model أصلاً؟

### Record Rule

بتجاوب:

> من records المسموح له يشوفها أو يعدلها؟

مثال:

```text
ACL:
User can read Maintenance Requests.

Record Rule:
User can only read requests created by himself.
```

---

## 10.5 `domain_force`

مثلاً:

```xml
<field name="domain_force">
    [('requested_by_id', '=', user.id)]
</field>
```

معناه:

> المستخدم يشوف records اللي requested_by_id فيها يساوي current user.

---

## 10.6 `user.id`

في record rule:

```python
user.id
```

هو ID المستخدم الحالي.

---

## 10.7 `has_group()`

في Python:

```python
if self.env.user.has_group(
    'asset_maintenance.group_asset_supervisor'
):
    ...
```

مفيد لما business action نفسها لازم تختلف حسب role.

---

## 10.8 `sudo()`

مهم جداً:

```python
self.sudo()
```

يتجاوز access restrictions في السياق المستخدم.

لكن لازم تسأل:

> هل فعلاً عايز أتجاوز security؟

لو آه، استخدمه في مكان ضيق وواضح وvalidated.

---

## 10.9 Designing Role-based Security

مثال:

### User

```text
Read assets
Create requests
Submit requests
View own requests
```

### Technician

```text
Everything User has
+
Work on assigned requests
```

### Supervisor

```text
Approve requests
Assign technicians
View team requests
```

### Manager

```text
Manage assets
View all maintenance
Retire assets
```

### Admin

```text
Full system administration
```

---

## 10.10 Common Security Mistakes

### Mistake 1

الاعتماد على button invisible فقط.

ده UI restriction، مش Security.

### Mistake 2

استخدام `sudo()` لإخفاء access errors.

ده ممكن يحول bug إلى vulnerability.

### Mistake 3

ACL موجودة لكن Record Rule تمنع كل records.

### Mistake 4

Record Rule بتمنع manager من رؤية كل requests بسبب domain ضيق.

---

## 10.11 Task

اعمل groups:

```text
Asset User
Maintenance Technician
Asset Supervisor
Asset Manager
```

واعتمد inheritance:

```text
Supervisor
   ↓
Technician
   ↓
User
```

وبعدين اعمل ACL + Record Rules.

---

# 11. Advanced Odoo

## 11.1 Model Inheritance

في Odoo عندنا أكتر من شكل.

---

## 11.2 Extension Inheritance

توسع model موجود:

```python
class SaleOrder(models.Model):
    _inherit = 'sale.order'

    custom_field = fields.Char()
```

ده لا يعمل model جديد بنفس المعنى؛ بيضيف behavior/fields للـ existing model.

---

## 11.3 Classical / Prototype-style Inheritance

ممكن تستخدم `_name` مع `_inherit` لإنشاء model مبني على model آخر حسب التصميم.

مثال conceptually:

```python
class SpecialAsset(models.Model):
    _name = 'special.asset'
    _inherit = 'asset.asset'
```

لكن لازم تختار inheritance pattern بناءً على business architecture، مش لمجرد إعادة استخدام syntax.

---

## 11.4 Delegation Inheritance

باستخدام:

```python
_inherits = {
    'some.model': 'field_id',
}
```

مفيد لما entity عندها composition/delegation relationship.

مش هو الاختيار الافتراضي لكل inheritance.

---

## 11.5 Abstract Models

ممكن تعمل reusable base behavior:

```python
class MaintenanceMixin(models.AbstractModel):
    _name = 'maintenance.mixin'
    _description = 'Maintenance Mixin'
```

وبعدين models تستخدمه.

---

# 11.6 Mixins

Mixins بتضيف reusable behavior.

أشهر مثال:

```python
_inherit = [
    'mail.thread',
    'mail.activity.mixin',
]
```

---

# 11.7 `mail.thread`

بيضيف Chatter functionality.

مثلاً:

```python
class MaintenanceRequest(models.Model):
    _name = 'asset.maintenance.request'
    _inherit = ['mail.thread']
```

وبعدين:

```python
state = fields.Selection(
    [...],
    tracking=True,
)
```

التغييرات تظهر في Chatter.

---

# 11.8 `mail.activity.mixin`

بيسمح بالـ Activities.

مثلاً:

```text
Call technician
Inspect asset
Approve maintenance
```

---

# 11.9 Chatter

في Form view:

```xml
<chatter/>
```

وفي model:

```python
_inherit = ['mail.thread', 'mail.activity.mixin']
```

ممكن تتابع:

- State changes
- Messages
- Followers
- Activities

---

# 11.10 Wizards

Wizard هو UI مؤقت لتنفيذ action.

مثلاً:

```text
Transfer Asset
 ↓
Choose destination
 ↓
Enter reason
 ↓
Confirm
```

---

## `TransientModel`

```python
class AssetTransferWizard(models.TransientModel):
    _name = 'asset.transfer.wizard'
    _description = 'Asset Transfer Wizard'
```

Transient records مؤقتة ويتم تنظيفها.

ما تستخدمش Wizard لتخزين permanent business history.

---

# 11.11 Sequences

Maintenance Request:

```text
MR00001
MR00002
MR00003
```

sequence:

```xml
<record id="seq_maintenance_request"
        model="ir.sequence">
    <field name="name">Maintenance Request</field>
    <field name="code">asset.maintenance.request</field>
    <field name="prefix">MR</field>
    <field name="padding">5</field>
</record>
```

في Python:

```python
self.env['ir.sequence'].next_by_code(
    'asset.maintenance.request'
)
```

---

# 11.12 Cron / Scheduled Actions

مثلاً كل يوم:

```text
Find overdue maintenance requests
        ↓
Notify supervisor
```

Cron مناسب للـ recurring background work.

لكن لازم تراعى:

- idempotency
- batch processing
- performance
- failures
- logging

---

# 11.13 Automated Actions

مناسبة لبعض configuration-driven automations.

مثلاً:

```text
Asset becomes Broken
        ↓
Create Activity
```

لكن business-critical behavior المعقد غالباً الأفضل يكون explicit Python code.

---

# 11.14 Email Templates

مثلاً لما Request تتapproved:

```text
Subject:
Maintenance Request Approved

Body:
Request MR00042 has been approved.
```

Email template reusable بدل بناء email body داخل كل method.

---

# 12. Reports

## 12.1 QWeb

QWeb هو template engine يستخدم في Odoo reports وأجزاء من UI.

---

## 12.2 Report Template

Conceptually:

```xml
<template id="maintenance_report_template">
    <t t-call="web.html_container">
        <t t-foreach="docs" t-as="doc">
            <h2>
                <t t-esc="doc.seq"/>
            </h2>
        </t>
    </t>
</template>
```

---

## 12.3 Report Action

```xml
<record id="action_maintenance_report"
        model="ir.actions.report">
    <field name="name">Maintenance Report</field>
    <field name="model">asset.maintenance.request</field>
    <field name="report_type">qweb-pdf</field>
    <field name="report_name">
        asset_maintenance.maintenance_report_template
    </field>
</record>
```

---

## 12.4 Dynamic Data

داخل QWeb:

```xml
<t t-esc="doc.asset_id.name"/>
```

```xml
<t t-esc="doc.total_cost"/>
```

---

## 12.5 Report Layout

Report ممكن يحتوي:

```text
Company Header
Request Information
Asset Information
Technician
Maintenance Details
Spare Parts
Costs
Approval
Footer
```

---

## 12.6 Common Report Errors

### Wrong report name

### Wrong model

### Template XML ID غلط

### Missing `docs`

### QWeb expression error

### CSS لا يظهر كما تتوقع

---

## 12.7 Task

اعمل Maintenance Request PDF يحتوي:

- Request Number
- Asset
- Technician
- Request Date
- Completion Date
- Description
- Spare Parts
- Maintenance Cost
- Total Cost
- State

---

# 13. Controllers & APIs

## 13.1 Controllers

Controller هو HTTP interface بين external client وOdoo.

```text
Mobile App
    ↓
HTTP Request
    ↓
Odoo Controller
    ↓
ORM
    ↓
PostgreSQL
```

---

# 13.2 `@http.route`

مثال:

```python
from odoo import http


class MaintenanceAPI(http.Controller):

    @http.route(
        '/api/v1/properties',
        type='json',
        auth='user',
        methods=['POST'],
        csrf=False,
    )
    def create_request(self, **kwargs):
        ...
```

---

# 13.3 GET

مناسب للقراءة.

```text
GET /api/v1/maintenance-requests
```

---

# 13.4 POST

لإنشاء resource.

```text
POST /api/v1/maintenance-requests
```

---

# 13.5 PUT

لتحديث resource.

```text
PUT /api/v1/maintenance-requests/42
```

---

# 13.6 DELETE

للحذف لو business policy تسمح.

```text
DELETE /api/v1/maintenance-requests/42
```

---

# 13.7 Authentication

اختار authentication strategy حسب العميل:

- Odoo session/user authentication
- Token-based authentication
- OAuth / external identity integration حسب architecture

ما تعملش endpoint sensitive بـ public auth لمجرد سهولة الاختبار.

---

# 13.8 CSRF

CSRF protection مهمة خصوصاً requests المعتمدة على browser session/cookies.

لو عطلتها:

```python
csrf=False
```

لازم يكون عندك security design واضح.

---

# 13.9 `request.env`

داخل controller:

```python
request.env['asset.maintenance.request']
```

---

# 13.10 `sudo()`

مثلاً:

```python
request.env[
    'asset.maintenance.request'
].sudo().search(...)
```

لكن في API:

> لا تستخدم sudo لمجرد إن endpoint بيطلع AccessError.

حدد بالضبط أي records المستخدم مسموح له يتعامل معها.

---

# 13.11 JSON Responses

شكل response موحد:

```json
{
    "success": true,
    "message": "Maintenance request created successfully",
    "data": {
        "id": 42,
        "name": "MR00042"
    }
}
```

Error:

```json
{
    "success": false,
    "message": "Invalid asset",
    "errors": {
        "asset_id": "Asset does not exist."
    }
}
```

---

# 13.12 HTTP Status Codes

أمثلة:

```text
200 OK
201 Created
204 No Content
400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
409 Conflict
422 Unprocessable Entity
500 Internal Server Error
```

اختيار status code لازم يعكس معنى العملية.

---

# 13.13 Error Handling

ما تعملش:

```python
except Exception:
    return {"error": "Something went wrong"}
```

وبس.

لأنك محتاج:

- Logging
- Safe client response
- Correct HTTP status
- Distinguish validation/business/server failures

ما تبعتش internal stack trace للـ client في Production.

---

# 13.14 Pagination

مثلاً:

```text
GET /api/v1/maintenance-requests?page=2&limit=20
```

حساب:

```python
page = max(page, 1)
limit = min(max(limit, 1), 100)
offset = (page - 1) * limit
```

وبعدين:

```python
records = model.search(
    domain,
    offset=offset,
    limit=limit,
    order='id asc',
)

total = model.search_count(domain)
```

Response:

```json
{
    "data": [],
    "pagination": {
        "page": 2,
        "limit": 20,
        "total_records": 145,
        "total_pages": 8
    }
}
```

---

# 13.15 Filtering

مثلاً:

```text
?state=approved
```

يتحول إلى:

```python
[
    ('state', '=', 'approved')
]
```

لا تسمح للـ client يبني domain arbitrary بدون validation.

---

# 13.16 API Security

لازم تفكر في:

- Authentication
- Authorization
- Rate limiting
- Input validation
- Record access
- Sensitive fields
- Logging
- CORS حسب architecture
- CSRF
- Token storage
- Error leakage

---

# 13.17 API Architecture

الأفضل تفصل:

```text
Controller
   ↓
Validation / HTTP concerns
   ↓
Business Service / Model methods
   ↓
ORM
```

ما تحطش business logic كله داخل controller.

---

# 14. OWL / Frontend

## 14.1 OWL يعني إيه؟

OWL = Odoo Web Library.

Framework frontend مبني على reactive component architecture.

مناسب لـ:

- Dashboards
- Custom client actions
- Interactive widgets
- Custom views
- Complex UI

---

# 14.2 Component

```javascript
/** @odoo-module **/

import { Component } from "@odoo/owl";

export class MaintenanceDashboard extends Component {
    static template = "asset_maintenance.MaintenanceDashboard";

    setup() {
    }
}
```

---

# 14.3 `setup()`

المكان الأساسي لتهيئة:

- State
- Services
- Hooks
- Event-related setup

مثلاً:

```javascript
setup() {
    this.state = useState({
        requests: [],
    });
}
```

---

# 14.4 `useState`

```javascript
import { useState } from "@odoo/owl";
```

```javascript
this.state = useState({
    requests: [],
    loading: true,
});
```

لما state تتغير، OWL يعمل reactive update.

---

# 14.5 Lifecycle Hooks

## `onWillStart`

مفيد للـ async initialization قبل rendering.

```javascript
onWillStart(async () => {
    await this.loadRequests();
});
```

## `onMounted`

بعد ما component يتعمل mount في DOM.

```javascript
onMounted(() => {
    console.log("Mounted");
});
```

## `onWillUnmount`

للتنظيف:

```javascript
onWillUnmount(() => {
    // cleanup
});
```

---

# 14.6 Services

بدل التعامل المباشر مع backend infrastructure.

```javascript
const orm = useService("orm");
```

---

# 14.7 ORM Service

مثلاً:

```javascript
const requests = await this.orm.searchRead(
    "asset.maintenance.request",
    [],
    ["seq", "state", "asset_id"]
);
```

الفكرة:

```text
OWL
 ↓
ORM Service
 ↓
Odoo Backend
 ↓
ORM
 ↓
Database
```

---

# 14.8 Registry

مثلاً Client Action:

```javascript
registry.category("actions").add(
    "asset_maintenance.dashboard",
    MaintenanceDashboard
);
```

Registry بتسمح لـ Odoo يعرف implementation المرتبط بالـ key.

---

# 14.9 Client Action

XML:

```xml
<record id="maintenance_dashboard_action"
        model="ir.actions.client">
    <field name="name">Maintenance Dashboard</field>
    <field name="tag">
        asset_maintenance.dashboard
    </field>
</record>
```

JS:

```javascript
registry.category("actions").add(
    "asset_maintenance.dashboard",
    MaintenanceDashboard
);
```

---

# 14.10 XML Template

```xml
<templates xml:space="preserve">

    <t t-name="asset_maintenance.MaintenanceDashboard">
        <div class="maintenance-dashboard">
            <h1>Maintenance Dashboard</h1>

            <div class="cards">
                <div class="card">
                    <span>Total Requests</span>
                    <strong>
                        <t t-esc="state.requests.length"/>
                    </strong>
                </div>
            </div>
        </div>
    </t>

</templates>
```

---

# 14.11 CSS

```css
.maintenance-dashboard {
    padding: 24px;
}

.maintenance-dashboard .card {
    border-radius: 12px;
    padding: 20px;
}
```

---

# 14.12 Calling Backend

أفضل pattern:

```javascript
this.orm.call(
    "asset.maintenance.request",
    "action_get_dashboard_data",
    []
);
```

بدل ما تحط business logic داخل JS.

---

# 14.13 Reactive State

مثلاً:

```javascript
this.state = useState({
    requests: [],
    total: 0,
});
```

بعد load:

```javascript
this.state.requests = requests;
this.state.total = requests.length;
```

الـ UI يتحدث تلقائياً.

---

# 14.14 Updating UI

لو عايز تحدث table لما يكون فيه records جديدة، ما تعملش refresh عشوائي لكل حاجة.

فكر في:

```text
Where did data change?
 ↓
When should frontend fetch?
 ↓
Can we detect changes?
 ↓
Can we update only affected state?
```

في production، polling أو bus/realtime mechanisms ممكن تكون أنسب حسب use case.

---

# 14.15 Custom Dashboard

Dashboard بتاعة المشروع ممكن تعرض:

```text
┌─────────────────────────────────────┐
│ Maintenance Dashboard               │
├─────────┬─────────┬─────────┬───────┤
│ Total   │ Pending │ Active  │ Done  │
│ 120     │ 24      │ 18      │ 78    │
├─────────┴─────────┴─────────┴───────┤
│ Maintenance Cost                     │
│             Chart                    │
├─────────────────────────────────────┤
│ Recent Requests                      │
│ MR001 | Laptop | Broken | Ahmed      │
│ MR002 | Printer| Done   | Mohamed    │
└─────────────────────────────────────┘
```

---

# 14.16 OWL Errors

أشهر أسباب المشاكل:

- Template name mismatch
- JS asset not loaded
- Registry key mismatch
- Wrong service name
- Undefined state
- Lifecycle hook misuse
- Wrong component import
- XML syntax error
- Backend method doesn't exist
- Returned data shape different from frontend expectation

Debug flow:

```text
Browser Console
 ↓
Network
 ↓
JS Stack Trace
 ↓
Template
 ↓
Registry
 ↓
Backend method
 ↓
ORM
```

---

# 14.17 Task

اعمل:

**Maintenance Dashboard**

يعرض:

- Total Requests
- Draft
- Submitted
- Approved
- In Progress
- Done
- Cancelled
- Total Maintenance Cost
- Recent Requests

---

# 15. Performance

## 15.1 ليه Performance مهمة؟

Odoo application ممكن يكون فيه:

```text
10 users
100 users
1000 users
1000000 records
```

كود يشتغل كويس على 100 records ممكن يبقى سيئ جداً على مليون record.

---

# 15.2 Avoid N+1 Queries

Bad pattern:

```python
for request in requests:
    technician = request.technician_id
    print(technician.name)
```

مش كل access هنا بالضرورة يعمل query منفصل بسبب ORM prefetching، لكن pattern العام لازم يكون واعي للـ prefetching وquery count.

---

# 15.3 Batch Operations

بدل:

```python
for asset in assets:
    asset.write({'active': False})
```

غالباً:

```python
assets.write({
    'active': False,
})
```

أفضل.

---

# 15.4 `search_read`

مفيد لما محتاج data بسيطة مباشرة.

```python
records = model.search_read(
    domain,
    ['name', 'state'],
)
```

لكن مش لازم تستخدمه في كل مكان.

---

# 15.5 `read_group`

مهم جداً للـ analytics.

مثلاً عدد requests حسب state:

```python
model.read_group(
    [],
    ['state'],
    ['state'],
)
```

ده أفضل من تحميل كل records وعمل Python counting.

---

# 15.6 Database Indexes

```python
asset_code = fields.Char(
    index=True,
)
```

مفيد لما field يستخدم كثيراً في filtering/search.

لكن index له cost في:

- Storage
- INSERT
- UPDATE
- Maintenance

---

# 15.7 Efficient Domains

بدل:

```python
records = model.search([])
broken = records.filtered(
    lambda r: r.state == 'broken'
)
```

غالباً:

```python
broken = model.search([
    ('state', '=', 'broken')
])
```

لأن filter يحصل في database.

---

# 15.8 Computed Field Performance

Computed fields ممكن تكون expensive.

خصوصاً:

```text
Record
 ↓
100 lines
 ↓
each line has relations
 ↓
complex computation
```

راجع:

- dependencies
- store
- batching
- query count
- whether computation can be SQL/aggregation

---

# 15.9 Stored vs Non-stored

### Non-stored

```python
total_cost = fields.Float(
    compute='_compute_total_cost'
)
```

مناسب لما القيمة dynamic ومش محتاج search/group بسهولة.

### Stored

```python
total_cost = fields.Float(
    compute='_compute_total_cost',
    store=True,
)
```

مناسب لما محتاج:

- Search
- Group By
- Reporting
- Analytics

لكن recalculation لها cost.

---

# 15.10 `sudo()` Performance/Security

`sudo()` مش مجرد performance tool.

هو security decision.

استخدمه لما عندك business reason واضح.

---

# 15.11 Performance Debugging

اسأل:

```text
How many SQL queries?
How many records loaded?
Can this be batched?
Can domain move filtering to DB?
Can read_group aggregate?
Is computed field expensive?
Is index justified?
```

---

# 15.12 Task

خد Dashboard:

```text
Total requests by state
```

ونفذها بطريقتين:

1. `search()` + Python counting
2. `read_group()`

وقارن conceptually.

---

# 16. Testing

## 16.1 ليه Testing؟

بدل كل تغيير تعمل:

```text
Click
Click
Click
Click
```

tests تخليك تتأكد إن behavior ما اتكسرش.

---

# 16.2 أنواع Tests

- Unit tests
- Integration tests
- Security tests
- Business logic tests
- Controller tests

---

# 16.3 TestCase

Conceptually:

```python
from odoo.tests.common import TransactionCase


class TestAsset(TransactionCase):

    def test_create_asset(self):
        asset = self.env['asset.asset'].create({
            'name': 'Laptop',
            'asset_code': 'AST-001',
        })

        self.assertEqual(
            asset.name,
            'Laptop',
        )
```

---

# 16.4 Transactions

Odoo tests غالباً تعمل داخل transaction controlled by test framework.

ده بيساعد إن test data ما تلوثش database testing environment بنفس طريقة production data.

---

# 16.5 Testing Business Logic

مثلاً:

```text
Draft → Submitted
```

valid.

لكن:

```text
Done → Submitted
```

invalid.

Test:

```python
with self.assertRaises(UserError):
    request.action_submit()
```

---

# 16.6 Testing Constraints

```python
with self.assertRaises(ValidationError):
    self.env['asset.asset'].create({
        'name': 'Laptop',
        'purchase_cost': -100,
    })
```

---

# 16.7 Testing Security

لازم تختبر:

```text
User sees own requests
Supervisor sees team requests
Manager sees all requests
User cannot approve
Technician cannot retire asset
```

Security testing مش optional في system حساس.

---

# 16.8 Testing Controllers

اختبر:

```text
POST valid
POST invalid
GET pagination
GET filtering
401/403
404
validation errors
```

---

# 16.9 Task

اعمل tests لـ:

- Asset creation
- Negative purchase cost
- Request state transitions
- Permissions
- API create
- API invalid input

---

# 17. Professional Development

# 17.1 Clean Code

Bad:

```python
def x(self):
    ...
```

Better:

```python
def action_approve_maintenance_request(self):
    ...
```

الأسماء لازم توضح intent.

---

# 17.2 Reusable Code

لو عندك logic يتكرر:

```text
validate request
calculate total
send notification
```

ما تكرروش في 5 أماكن.

اعمل abstraction مناسبة.

لكن:

> Don't abstract too early.

---

# 17.3 Module Architecture

قسّم الـ code حسب responsibility:

```text
models
services/helpers where justified
controllers
views
security
reports
wizard
tests
```

ما تعملش abstraction لمجرد إن الكود شكله duplicate صغير.

---

# 17.4 Debugging

لما Error يحصل:

```text
Error message
   ↓
Read traceback from bottom/up
   ↓
Find your module frame
   ↓
Find first meaningful custom line
   ↓
Understand input/state
   ↓
Reproduce
   ↓
Fix root cause
   ↓
Add regression test
```

ما تعملش:

```text
Error
 ↓
Try random changes
```

---

# 17.5 Logging

استخدم logging:

```python
import logging

_logger = logging.getLogger(__name__)
```

وبعدين:

```python
_logger.info(
    "Maintenance request %s approved",
    request.seq,
)
```

ما تعملش:

```python
print(...)
```

في Production business logic.

---

# 17.6 Git

Git workflow:

```text
main
  ↓
feature/maintenance-request-workflow
  ↓
commit
  ↓
pull request
  ↓
review
  ↓
merge
```

Commit message واضح:

```text
feat: add maintenance request workflow
fix: prevent negative asset cost
refactor: optimize maintenance dashboard query
```

---

# 17.7 GitHub

Repository structure ممكن:

```text
asset-maintenance/
├── custom_addons/
│   └── asset_maintenance/
├── README.md
├── requirements.txt
├── .gitignore
└── docs/
```

ما ترفعش:

```text
.venv/
__pycache__/
*.pyc
database dumps
secrets
.env
```

---

# 17.8 Requirements

Production project لازم dependencies تكون واضحة.

مثلاً:

```text
requirements.txt
```

لكن لازم تفرق بين:

```text
Odoo Python dependencies
Project dependencies
System dependencies
```

---

# 17.9 Virtual Environment

مثلاً Windows:

```powershell
python -m venv .venv
```

Activate:

```powershell
.venv\Scripts\Activate.ps1
```

ثم:

```powershell
pip install -r requirements.txt
```

---

# 17.10 Odoo Configuration

Config ممكن يحتوي:

```ini
[options]

addons_path =
    C:\odoo\odoo\addons,
    C:\odoo\custom_addons

db_host = localhost
db_port = 5432
db_user = odoo
db_password = your_password

admin_passwd = your_master_password

http_port = 8069
```

في Production secrets لازم تكون managed بشكل آمن، وماتتحطش في Git.

---

# 17.11 Development Environment

Development:

```text
Windows/Linux
Python
Virtualenv
PyCharm/VS Code
PostgreSQL
Odoo source
Custom addons
Git
```

---

# 17.12 Production Environment

Typical:

```text
Internet
   ↓
Nginx
   ↓
Odoo
   ↓
PostgreSQL
```

ممكن تستخدم:

```text
Nginx
SSL/TLS
Odoo workers
PostgreSQL
Backups
Monitoring
Log management
```

---

# 17.13 Deployment

Basic production flow:

```text
Git
 ↓
Pull release
 ↓
Install dependencies
 ↓
Update module
 ↓
Restart Odoo
 ↓
Verify logs
 ↓
Smoke test
```

لا تعمل update على production بدون backup وخطة rollback مناسبة.

---

# 17.14 PostgreSQL

Odoo يعتمد على PostgreSQL.

مهم تفهم:

- Database
- Tables
- Indexes
- Transactions
- Locks
- Connections
- Backups
- Query performance

لكن business logic يفضل يمر عبر ORM.

---

# 17.15 Nginx

Nginx ممكن يكون reverse proxy:

```text
Client
 ↓
HTTPS
 ↓
Nginx
 ↓
Odoo
```

مسؤوليات ممكن تشمل:

- TLS termination
- Reverse proxy
- Static handling حسب setup
- Security headers
- Request limits

---

# 17.16 Backups

Backup strategy لازم تشمل:

```text
Database
Filestore
Configuration
Custom addons/source
```

مش database فقط.

---

# 17.17 Security

Production security:

- Strong master password
- HTTPS
- Least privilege
- Restricted database access
- Secure secrets
- Proper file permissions
- Regular updates
- Audit logs where needed
- Safe API authentication
- Avoid unnecessary sudo

---

# 17.18 Monitoring

راقب:

```text
CPU
RAM
Disk
PostgreSQL
Odoo workers
HTTP errors
Slow requests
Logs
Database size
Backup success
```

---

# 18. Production Checklist

قبل ما تعتبر Module Production-ready:

## Architecture

- [ ] Module structure واضحة
- [ ] Responsibilities separated
- [ ] No unnecessary core modifications
- [ ] Naming consistent

## Models

- [ ] Fields مناسبة
- [ ] Relations صحيحة
- [ ] Constraints موجودة
- [ ] Business rules server-side
- [ ] Computed fields reviewed

## ORM

- [ ] No unnecessary SQL
- [ ] Batch operations used
- [ ] No obvious N+1
- [ ] Domains efficient
- [ ] `sudo()` justified

## Views

- [ ] Form
- [ ] List
- [ ] Search
- [ ] Appropriate Kanban/Calendar/Graph/Pivot
- [ ] Buttons protected
- [ ] XML inheritance clean

## Security

- [ ] Groups
- [ ] ACL
- [ ] Record Rules
- [ ] Role-based design
- [ ] No security through UI only
- [ ] `sudo()` audited

## Reports

- [ ] QWeb works
- [ ] Correct report action
- [ ] Layout tested
- [ ] Large data considered

## API

- [ ] Authentication
- [ ] Authorization
- [ ] Validation
- [ ] Error handling
- [ ] Correct HTTP status codes
- [ ] Pagination
- [ ] Filtering
- [ ] No sensitive data leakage

## OWL

- [ ] Assets configured
- [ ] Registry keys correct
- [ ] State management clean
- [ ] Lifecycle handled
- [ ] Backend calls controlled
- [ ] UI updates efficiently

## Performance

- [ ] Query count reviewed
- [ ] `read_group` used where appropriate
- [ ] Batch operations
- [ ] Indexes justified
- [ ] Computed fields reviewed

## Testing

- [ ] Model tests
- [ ] Business rules
- [ ] Security
- [ ] API
- [ ] Regression tests

## Deployment

- [ ] Git
- [ ] Requirements
- [ ] Config
- [ ] PostgreSQL
- [ ] Nginx/HTTPS
- [ ] Backup
- [ ] Monitoring
- [ ] Rollback plan

---

# 19. Final Project Roadmap

إحنا مش هنبني المشروع كله مرة واحدة.

هنبنيه على مراحل.

## Phase 1 — Foundation

```text
Module
 ↓
Manifest
 ↓
Models
 ↓
Fields
```

Models:

```text
Asset
Asset Category
Technician
Spare Part
```

---

## Phase 2 — Relations

```text
Category
   ↓
Assets

Asset
   ↓
Maintenance Requests

Request
   ↓
Spare Part Lines
   ↓
Spare Parts
```

---

## Phase 3 — Business Logic

```text
State Machine
 ↓
Validation
 ↓
Computed Costs
 ↓
Transitions
```

---

## Phase 4 — UI

```text
Form
List
Search
Kanban
Calendar
Graph
Pivot
Buttons
Smart Buttons
```

---

## Phase 5 — Security

```text
Groups
 ↓
ACL
 ↓
Record Rules
 ↓
Business Authorization
```

---

## Phase 6 — Advanced Odoo

```text
Inheritance
 ↓
Mixins
 ↓
Chatter
 ↓
Activities
 ↓
Wizards
 ↓
Sequences
 ↓
Cron
 ↓
Email Templates
```

---

## Phase 7 — Reports

```text
QWeb
 ↓
Report Action
 ↓
PDF
 ↓
Maintenance History
```

---

## Phase 8 — API

```text
Controller
 ↓
Authentication
 ↓
Validation
 ↓
ORM
 ↓
JSON Response
 ↓
Pagination
 ↓
Filtering
```

---

## Phase 9 — OWL

```text
OWL Component
 ↓
State
 ↓
Services
 ↓
ORM Service
 ↓
Dashboard
 ↓
Reactive UI
```

---

## Phase 10 — Performance

```text
Query analysis
 ↓
Batching
 ↓
read_group
 ↓
Indexes
 ↓
Computed fields
```

---

## Phase 11 — Testing

```text
Unit
 ↓
Integration
 ↓
Security
 ↓
API
 ↓
Regression
```

---

## Phase 12 — Production

```text
Git
 ↓
Environment
 ↓
PostgreSQL
 ↓
Nginx
 ↓
Odoo Workers
 ↓
Backups
 ↓
Monitoring
```

---

# 🧠 Senior Developer Mindset

لما تشوف أي requirement في Odoo، ما تبدأش بالكود.

ابدأ بالأسئلة:

```text
1. What is the business entity?
2. What data do we need?
3. Who can access it?
4. Who can modify it?
5. What are the valid states?
6. What are the business rules?
7. What relations exist?
8. What UI is required?
9. Does it need automation?
10. Does it need reporting?
11. Does it need an API?
12. Does it need OWL?
13. How many records are expected?
14. How will we test it?
15. How will it behave in Production?
```

ده الفرق بين:

```text
Developer who writes Odoo code
```

و:

```text
Odoo Developer who designs Odoo systems
```

---

# 🚀 The Main Rule

> **Don't learn Odoo as syntax. Learn Odoo as a business framework and architecture.**

كل Feature جديدة في Asset Maintenance لازم تعدي على:

```text
Requirement
    ↓
Business Design
    ↓
Model
    ↓
Fields
    ↓
Relations
    ↓
Business Logic
    ↓
Security
    ↓
Views
    ↓
Automation
    ↓
Reports/API/OWL
    ↓
Testing
    ↓
Performance
    ↓
Production
```

وده هيكون المسار الكامل من Beginner إلى Professional Odoo Developer.
