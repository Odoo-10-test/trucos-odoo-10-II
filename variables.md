# Variables

```
from odoo import fields, models, api, _
from datetime import datetime
from odoo.exceptions import UserError

name = fields.Char('Certificate name', size=128, required=True)

entry_date = fields.Datetime('Fecha de Entrada', default = lambda self: datetime.today())

doc_type = fields.Selection(
            [('D','RUT Chile'),
            ('N','Permiso de residencia Chile ')],
            'Tipo de Documento', size=1)
            
user_id = fields.Many2one('res.users', string='Responsable', track_visibility='onchange',
            default=lambda self: self.env.user)
  
company_id = fields.Many2one('res.company', string='Compañía', change_default=True, readonly=True,
            default=lambda self: self.env['res.company']._company_default_get('traveler.register'))
```
