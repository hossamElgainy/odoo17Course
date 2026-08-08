# Odoo 17 Development --- Asset Maintenance Management

> **Odoo Senior Developer / Mentor Roadmap**
>
> الهدف من الـ documentation دي إنك تتعلم Odoo 17 من الصفر لحد مستوى
> Professional، مع التركيز على الفهم الحقيقي للـ Architecture والـ ORM
> والـ Security والـ Backend والـ OWL Frontend، مش مجرد حفظ Syntax.

------------------------------------------------------------------------

## 🎯 الهدف من الـ Documentation

الـ Documentation دي مبنية على مشروع عملي اسمه:

**Asset Maintenance Management**

هنستخدم نفس المشروع في شرح وتطبيق كل Concept بدل ما نعمل أمثلة منفصلة
لكل موضوع.

الهدف النهائي:

-   بناء Odoo Modules حقيقية.
-   فهم Odoo Architecture.
-   فهم الـ ORM بشكل عميق.
-   كتابة Business Logic بطريقة صحيحة.
-   تصميم Security احترافية.
-   بناء Reports وAPIs.
-   تطوير OWL Frontend.
-   تحسين Performance.
-   كتابة Tests.
-   تجهيز Module للـ Production.

------------------------------------------------------------------------

# 🏗️ Project Architecture

المشروع بيحاكي نظام حقيقي لإدارة أصول الشركة والصيانة.

## Features

-   Assets
-   Asset Categories
-   Technicians
-   Maintenance Requests
-   Spare Parts
-   Asset Transfers
-   Maintenance Reports
-   Maintenance History

## Maintenance Request Workflow

``` text
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

مع إمكانية الانتقال إلى:

``` text
Cancelled
```

## Roles

``` text
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

------------------------------------------------------------------------

# 📚 Learning Roadmap

## 1. Module Fundamentals

-   Module Structure
-   `__manifest__.py`
-   `__init__.py`
-   Dependencies
-   Data Files
-   Assets

## 2. Models & Fields

-   Models
-   `_name`
-   `_description`
-   `_rec_name`
-   Char
-   Text
-   Integer
-   Float
-   Boolean
-   Date
-   Datetime
-   Selection
-   Binary
-   `required`
-   `readonly`
-   `default`
-   `copy`
-   `index`
-   `tracking`

## 3. ORM

-   `env`
-   Recordsets
-   `create()`
-   `write()`
-   `unlink()`
-   `search()`
-   `search_count()`
-   `browse()`
-   `read()`
-   `search_read()`
-   `mapped()`
-   `filtered()`
-   `sorted()`
-   `ensure_one()`
-   Domains
-   Context
-   `sudo()`

## 4. Relations

-   Many2one
-   One2many
-   Many2many
-   Related Fields
-   `ondelete`
-   Relation Tables
-   Command syntax for relational fields

## 5. Business Logic

-   Regular Methods
-   `@api.model`
-   `@api.depends`
-   `@api.constrains`
-   `@api.onchange`
-   Computed Fields
-   Stored Computed Fields
-   Inverse Methods
-   Business Rules
-   State Machines
-   State Transitions
-   `super()`
-   Override `create()`
-   Override `write()`
-   Override `unlink()`

## 6. Views

-   Form
-   List
-   Search
-   Kanban
-   Calendar
-   Graph
-   Pivot
-   Buttons
-   Statusbar
-   Smart Buttons
-   Domains in Views
-   Context in Views
-   XML Inheritance
-   XPath
-   View Priority

## 7. Actions & Menus

-   `ir.actions.act_window`
-   Client Actions
-   Server Actions
-   Window Actions
-   Menus
-   Menu hierarchy

## 8. Security

-   Users
-   Groups
-   `res.groups`
-   ACL
-   `ir.model.access.csv`
-   Record Rules
-   `domain_force`
-   `user.id`
-   `has_group()`
-   `sudo()`
-   Difference between ACL and Record Rules
-   Designing role-based security

## 9. Advanced Odoo

-   Model Inheritance
-   Extension Inheritance
-   Classical Inheritance
-   Delegation Inheritance
-   Abstract Models
-   Mixins
-   `mail.thread`
-   `mail.activity.mixin`
-   Chatter
-   Tracking
-   Activities
-   Wizards
-   `TransientModel`
-   Sequences
-   Cron / Scheduled Actions
-   Automated Actions
-   Email Templates

## 10. Reports

-   QWeb
-   QWeb Templates
-   Report Actions
-   PDF Reports
-   Dynamic Report Data
-   Report Layout
-   Headers / Footers

## 11. Controllers & APIs

-   Controllers
-   `@http.route`
-   GET
-   POST
-   PUT
-   DELETE
-   Authentication
-   CSRF
-   `request.env`
-   `sudo()`
-   JSON Responses
-   Error Handling
-   HTTP Status Codes
-   Pagination
-   Filtering
-   API Security
-   API Architecture

## 12. OWL / Frontend

-   OWL Architecture
-   Components
-   Templates
-   `setup()`
-   `useState`
-   Lifecycle Hooks
-   `onWillStart`
-   `onMounted`
-   `onWillUnmount`
-   Services
-   `useService`
-   ORM Service
-   Registry
-   Client Actions
-   JS Modules
-   XML Templates
-   Assets
-   CSS
-   Calling Backend from OWL
-   Reactive State
-   Updating UI
-   Custom Dashboards
-   Custom Views
-   OWL Errors

## 13. Performance

-   ORM Optimization
-   Avoiding N+1 Queries
-   `search_read`
-   `read_group`
-   Batch Operations
-   Database Indexes
-   Efficient Domains
-   Computed Field Performance
-   Stored vs Non-stored Fields
-   `sudo()` Performance/Security considerations

## 14. Testing

-   Odoo Testing Architecture
-   Unit Tests
-   Integration Tests
-   TestCase
-   Transactions
-   Testing Models
-   Testing Security
-   Testing Business Logic
-   Testing Controllers

## 15. Professional Development

-   Clean Code
-   Module Architecture
-   Reusable Code
-   Debugging
-   Logging
-   Git
-   GitHub
-   Requirements
-   Virtual Environment
-   Odoo Configuration
-   Development Environment
-   Production Environment
-   Deployment
-   PostgreSQL
-   Nginx
-   Backups
-   Security
-   Monitoring

------------------------------------------------------------------------

# 📖 Learning Methodology

كل Topic هيتشرح بنفس الـ structure:

1.  **يعني إيه؟**
2.  **المشكلة اللي بيحلها**
3.  **إمتى أستخدمه؟**
4.  **إمتى ماستخدموش؟**
5.  **Syntax الأساسي**
6.  **Example بسيط**
7.  **Example من Asset Maintenance**
8.  **شرح الكود بالتفصيل**
9.  **إيه اللي بيحصل داخل Odoo؟**
10. **Common Mistakes**
11. **Errors محتملة وحلها**
12. **Best Practices**
13. **Production Example**
14. **Task للتطبيق**

------------------------------------------------------------------------

# 🧩 Module Fundamentals

## 1. Module Structure

الـ Odoo Module هو Package بيضيف Feature أو Business Functionality جديدة
للنظام.

مثلاً:

``` text
Odoo
├── Sales
├── Purchase
├── Inventory
├── Accounting
└── Asset Maintenance
```

الـ Module مش مجرد Python files.

هو مجموعة أجزاء بتشتغل مع بعض:

``` text
Python
   ↓
Models / Business Logic
   ↓
ORM
   ↓
PostgreSQL

XML
   ↓
Views / Menus / Actions / Security / Data

JavaScript
   ↓
OWL / Frontend

CSS
   ↓
UI Styling

QWeb
   ↓
Reports
```

------------------------------------------------------------------------

# 📁 Production-like Module Structure

``` text
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
├── static/
│   └── src/
│       ├── js/
│       ├── xml/
│       └── css/
│
└── demo/
    └── demo.xml
```

> مش لازم كل الـ folders تكون موجودة من أول يوم. بنضيف كل جزء لما
> نحتاجه.

------------------------------------------------------------------------

# 📄 `__manifest__.py`

الـ `__manifest__.py` هو بطاقة تعريف الـ Module بالنسبة لـ Odoo.

``` python
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

## أهم الحقول

### `name`

الاسم اللي بيظهر للمستخدم:

``` python
'name': 'Asset Maintenance Management',
```

الـ technical name مختلف:

``` text
asset_maintenance
```

### `version`

إصدار الـ Module:

``` python
'version': '17.0.1.0.0',
```

### `depends`

الـ Odoo Modules اللي الـ Module بتاعنا بيعتمد عليها:

``` python
'depends': [
    'base',
    'mail',
],
```

هنحتاج `mail` عشان نستخدم:

``` python
mail.thread
mail.activity.mixin
```

> مهم: `depends` بتاعة Odoo مختلفة عن Python imports.

Python:

``` python
from odoo import models, fields
```

Odoo:

``` python
'depends': ['mail']
```

### `data`

الملفات اللي Odoo بيعملها Load:

``` python
'data': [
    'security/security.xml',
    'security/ir.model.access.csv',
    'data/sequence.xml',
    'views/asset_views.xml',
    'views/maintenance_request_views.xml',
    'views/menus.xml',
],
```

### `assets`

بتحدد ملفات الـ Frontend اللي Odoo يحملها:

``` python
'assets': {
    'web.assets_backend': [
        'asset_maintenance/static/src/js/**/*.js',
        'asset_maintenance/static/src/xml/**/*.xml',
        'asset_maintenance/static/src/css/**/*.css',
    ],
},
```

وده هنحتاجه لما نعمل OWL Dashboard أو Custom View.

### `installable`

``` python
'installable': True,
```

معناها إن الـ Module قابل للتثبيت.

### `application`

``` python
'application': True,
```

بتوضح إن الـ Module يعتبر Application رئيسي.

------------------------------------------------------------------------

# 📄 `__init__.py`

الـ root `__init__.py` بيعمل import للـ Python packages:

``` python
from . import models
```

وبعدين:

``` text
__init__.py
    ↓
models/__init__.py
    ↓
asset.py
```

------------------------------------------------------------------------

# 📄 `models/__init__.py`

مثلاً:

``` python
from . import asset
from . import technician
from . import maintenance_request
```

ده بيخلي ملفات الـ models يتم تحميلها.

لو نسيت:

``` python
from . import asset
```

ممكن يكون `asset.py` موجود فعلاً لكن الـ Model مش متسجل في Odoo.

------------------------------------------------------------------------

# 🧠 Module Loading Flow

بشكل مبسط:

``` text
Odoo
  ↓
Read __manifest__.py
  ↓
Check dependencies
  ↓
Load Python code
  ↓
Register Models
  ↓
Load Security
  ↓
Load Data
  ↓
Load Views
  ↓
Load Assets
```

------------------------------------------------------------------------

# 🏗️ أول Model في المشروع

``` text
asset_maintenance/
│
├── __init__.py
├── __manifest__.py
│
└── models/
    ├── __init__.py
    └── asset.py
```

`models/asset.py`:

``` python
from odoo import models, fields


class Asset(models.Model):
    _name = 'asset.asset'
    _description = 'Company Asset'

    name = fields.Char(
        string='Asset Name',
        required=True,
    )
```

العلاقة:

``` text
__manifest__.py
        ↓
__init__.py
        ↓
models/__init__.py
        ↓
asset.py
        ↓
Asset Model
```

------------------------------------------------------------------------

# 🔍 إيه اللي بيحصل داخل Odoo؟

لما Odoo يقرأ:

``` python
_name = 'asset.asset'
```

الـ ORM يسجل Model اسمه:

``` text
asset.asset
```

وبعد كده تقدر تتعامل معاه من خلال:

``` python
self.env['asset.asset']
```

ومن خلال الـ ORM تقدر تستخدم:

``` python
search()
create()
write()
unlink()
```

إحنا مش بنتعامل مع PostgreSQL بشكل مباشر في الـ business logic.

الـ ORM هو الطبقة اللي بتربط الـ Python Models بالـ Database.

------------------------------------------------------------------------

# ⚠️ Common Mistakes

## 1. نسيان import

الملف:

``` text
models/asset.py
```

موجود، لكن:

``` python
from . import asset
```

مش موجود في:

``` text
models/__init__.py
```

النتيجة: الـ Model مش بيتحمل.

## 2. Path غلط في manifest

لو كتبت:

``` python
'views/assets.xml'
```

لكن الملف اسمه:

``` text
views/asset_views.xml
```

هتحصل مشكلة أثناء loading لأن Odoo مش لاقي الملف.

## 3. نسيان إضافة XML إلى `data`

لو عندك:

``` text
views/asset_views.xml
```

لكن نسيت:

``` python
'data': [
    'views/asset_views.xml',
]
```

فالـ XML مش هيتحمل.

------------------------------------------------------------------------

# 🛠️ Best Practices

من البداية افصل المسؤوليات:

``` text
models/
    Business Logic

views/
    UI

security/
    Access Control

data/
    Configuration / Initial Data

wizard/
    Temporary User Operations

reports/
    Reporting

static/
    Frontend
```

## ما تعدلش Odoo Core

بدل ما تعدل ملفات Odoo نفسها، اعمل Custom Module.

مثلاً لو عايز تعدل `sale.order`:

``` python
class SaleOrder(models.Model):
    _inherit = 'sale.order'
```

وده هنشرحه بالتفصيل في Model Inheritance.

------------------------------------------------------------------------

# 🏢 Production Example

لو الشركة قالت:

> عايزين نظام لإدارة أصول الشركة والصيانة.

ممكن architecture تكون:

``` text
asset_maintenance/
│
├── models/
│   ├── asset.py
│   ├── asset_category.py
│   ├── technician.py
│   ├── maintenance_request.py
│   ├── maintenance_request_line.py
│   ├── spare_part.py
│   └── asset_transfer.py
│
├── security/
│   ├── security.xml
│   └── ir.model.access.csv
│
├── views/
│   ├── asset_views.xml
│   ├── maintenance_request_views.xml
│   ├── technician_views.xml
│   └── menus.xml
│
├── data/
│   ├── sequence.xml
│   ├── cron.xml
│   └── mail_template.xml
│
├── wizard/
│   └── asset_transfer_wizard.py
│
├── reports/
│   ├── maintenance_report.xml
│   └── maintenance_report_templates.xml
│
└── static/
    └── src/
        ├── js/
        ├── xml/
        └── css/
```

الهدف مش إن كل Module يبقى بنفس الشكل.

القاعدة الأهم:

> **Organize by responsibility.**

------------------------------------------------------------------------

# 📝 First Task

اعمل أول Version من:

``` text
asset_maintenance
```

بحيث تحتوي على:

``` text
asset_maintenance/
│
├── __init__.py
├── __manifest__.py
│
└── models/
    ├── __init__.py
    └── asset.py
```

والـ Model:

``` python
class Asset(models.Model):
    _name = 'asset.asset'
    _description = 'Company Asset'

    name = fields.Char(required=True)
```

والـ manifest يعتمد على:

``` python
'depends': ['base']
```

بعد كده جرّب تثبت الـ Module.

لو ظهر Error، ابعته زي ما هو.

هنعمل عليه:

``` text
Error
  ↓
Root Cause
  ↓
How to Debug
  ↓
Fix
  ↓
Best Practice
  ↓
Refactoring
```

------------------------------------------------------------------------

# 🚀 Next Topic

بعد Module Structure هنكمل:

``` text
Module Fundamentals
        ↓
__manifest__.py Deep Dive
        ↓
Dependencies
        ↓
Data Files
        ↓
Assets
        ↓
Models
        ↓
Fields
        ↓
ORM
```

وبعدها هنبدأ نبني الـ Asset Maintenance System فعليًا خطوة بخطوة.

------------------------------------------------------------------------

# 🎯 End Goal

في نهاية الـ roadmap المفروض تكون قادر تعمل:

``` text
Production-ready Odoo Module
│
├── Backend
│   ├── Models
│   ├── ORM
│   ├── Business Logic
│   └── APIs
│
├── Security
│   ├── ACL
│   ├── Groups
│   └── Record Rules
│
├── UI
│   ├── XML Views
│   └── OWL
│
├── Reports
│   └── QWeb PDF
│
├── Automation
│   ├── Cron
│   └── Automated Actions
│
├── Testing
│
└── Production
    ├── PostgreSQL
    ├── Nginx
    ├── Backups
    ├── Monitoring
    └── Deployment
```

> **المبدأ الأساسي:** متتعلمش Odoo كـ Syntax. اتعلمه كـ Framework +
> Architecture + Business Platform.
