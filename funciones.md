
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
