
# Funciones


# Calculando el Stock
```
stock = sum(id.stock_quant_ids.mapped('qty'))
 ```   
# Valor por defecto desde una funcion

```
journal_imposiciones_id = fields.Many2one('account.journal', 'Diario Pago Imposiciones',
                                 default=lambda self: self._get_default_journal(), )
@api.model
def _get_default_journal(self):
  return self.env['ir.values'].get_defaults_dict('hr.payroll.config.settings').get('journal_id')
 ```                           
                            

# Onchange

```
@api.onchange('product_ids')
    def onchange_product_ids(self):
        product_ids = self.product_ids
        mayor = 0
        if product_ids:
            for line in self.product_ids:
                if line.cost_compra_fob > mayor:
                    print line.cost_compra_fob
                    mayor = line.cost_compra_fob
            self.cost_compra_fob = mayor
```

# GetName

```
@api.multi
    def name_get(self):
        res = super(ProcesoAdministracion, self).name_get()
        result = []
        for element in res:
            product_id = element[0]
            code = self.name
            if self.property_id:
                rol = self.property_id.street
            else:
                rol = '-'
            name = code and '[%s] %s' % (code, rol) or '%s' % rol
            result.append((product_id, name))
        return result
```


```
class ListDiscounts(models.Model):
    _name = 'list.discounts'
    _description = 'Lista de Descuentos'
    _rec_name = 'product_id'
```    

```
@api.model
    def name_search(self, name='', args=None, operator='ilike', limit=100):
        records = self.search((args or []) + [('desc', operator, name)])
        if records:
            return records.name_get()
        return super(HrHaberesydesc, self).name_search(name, args, operator, limit)
```

# Ejecutar Boton
```
@api.multi
def exe_stock(self):
    self.state = 'stock_disponible'
        
        
<button name="exe_next" string="Próximo" class="oe_highlight" type="object"
                          confirm="¿Estás seguro de adelantar el paso?"/>
```


# Secuencia
```
@api.model
    def create(self, vals):
        if vals.get('name', "New") == "New":
            vals['name'] = self.env['ir.sequence'].next_by_code('proceso.administracion') or "New"
        return super(ProcesoAdministracion, self).create(vals)
        
        
<?xml version="1.0" encoding="utf-8"?>
<odoo>
    <data noupdate="1">
        <record id="seq_real_proceso_administracion" model="ir.sequence">
            <field name="name">Proceso Administracion</field>
            <field name="code">proceso.administracion</field>
            <field name="prefix">ADM/%(range_year)s/</field>
            <field name="padding">5</field>
            <field name="company_id" eval="False"/>
        </record>
    </data>
</odoo>

```
