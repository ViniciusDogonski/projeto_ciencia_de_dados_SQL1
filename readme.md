
### Modelo Lógico do Banco de Dados:

Tabelas:
- Cliente (cliente_id, nome, tipo)
- Pedido (pedido_id, cliente_id, valor_total)
- Produto (produto_id, nome, preco)
- Pedido_Item (pedido_id, produto_id, quantidade)
- Pagamento (pagamento_id, pedido_id, metodo)
- Fornecedor (fornecedor_id, nome)
- Estoque (produto_id, fornecedor_id, quantidade)
- Entrega (entrega_id, pedido_id, status, codigo_rastreio)

### Consultas SQL de Exemplo:

1. Recuperação simples de todos os produtos:
```sql
SELECT * FROM Produto;
```

2. Filtro para mostrar pedidos de um cliente específico:
```sql
SELECT * FROM Pedido WHERE cliente_id = 123;
```

3. Criação de uma coluna derivada que calcula o valor total de um pedido:
```sql
SELECT pedido_id, SUM(quantidade * preco) AS valor_total
FROM Pedido_Item
JOIN Produto ON Pedido_Item.produto_id = Produto.produto_id
GROUP BY pedido_id;
```

4. Ordenar produtos pelo preço em ordem decrescente:
```sql
SELECT * FROM Produto ORDER BY preco DESC;
```

5. Mostrar o número de pedidos feitos por cada cliente:
```sql
SELECT cliente_id, COUNT(*) AS num_pedidos
FROM Pedido
GROUP BY cliente_id;
```

6. Relação de produtos e seus fornecedores:
```sql
SELECT Produto.nome AS nome_produto, Fornecedor.nome AS nome_fornecedor
FROM Produto
JOIN Estoque ON Produto.produto_id = Estoque.produto_id
JOIN Fornecedor ON Estoque.fornecedor_id = Fornecedor.fornecedor_id;
```

7. Mostrar pedidos com status de entrega "Entregue" e seus detalhes:
```sql
SELECT Pedido.pedido_id, Cliente.nome AS nome_cliente, Entrega.status, Entrega.codigo_rastreio
FROM Pedido
JOIN Cliente ON Pedido.cliente_id = Cliente.cliente_id
JOIN Entrega ON Pedido.pedido_id = Entrega.pedido_id
WHERE Entrega.status = 'Entregue';
```

