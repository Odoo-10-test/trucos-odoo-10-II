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

# One2many

```
product_ids = fields.One2many('product.list', 'template_id', string='Listado Productos')

        
class ProductList(models.Model):
    _name = 'product.list'
    _description = 'Listado de Productos'
    parnert_id = fields.Many2one('res.partner', 'Proveedor')
    cost_compra_fob = fields.Float('Costo de Compra FOB')

    template_id = fields.Many2one('product.template', 'producto', ondelete='cascade')
    
<notebook>
        <page name="listado_materiales" string="Costo x Proveedores">
                    <field name="product_ids">
                        <tree editable="bottom">
                            <field name="parnert_id" required="1"/>
                            <field name="cost_compra_fob" required="1"/>
                        </tree>
                    </field>
         </page>
 </notebook>    
```


# Etiquetas

```
class ProcesoArriendoTag(models.Model):
    _name = 'proceso.arriendo.tag'
    _description = 'Compra y Venta Tag'

    active = fields.Boolean(default=True)
    color = fields.Integer(required=True, default=0)
    name = fields.Char(required=True)
    
tag_ids = fields.Many2many('proceso.arriendo.tag', string='Etiquetas')  

 <div class="oe_title">
   <h1><field name="name" readonly="1"/></h1>
   <field name="tag_ids" placeholder="Etiquetas" widget="many2many_tags"  options="{'no_create_edit': True}"/>
</div>
```

