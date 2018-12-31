
# Funciones

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


# Ejecutar Boton
```
@api.multi
    def exe_stock(self):
        self.state = 'stock_disponible'
        
        
<button name="exe_next" string="Próximo" class="oe_highlight" type="object"
                          confirm="¿Estás seguro de adelantar el paso?"/>
```
