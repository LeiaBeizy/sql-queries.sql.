# sql-queries.sql

## 📊 Exemplo de Consulta SQL Analítica no Projeto

Para demonstrar a lógica de negócio aplicada, extraímos a taxa de aprovação de crédito segmentada por faixa etária com a seguinte query (disponível na pasta `sql/`):

```sql
SELECT 
    CASE 
        WHEN c.idade < 30 THEN '18-29 anos'
        WHEN c.idade BETWEEN 30 AND 50 THEN '30-50 anos'
        ELSE 'Mais de 50 anos'
    END AS faixa_etaria,
    COUNT(p.pedido_id) AS total_pedidos,
    SUM(CASE WHEN p.estado_pedido = 'Aprovado' THEN 1 ELSE 0 END) AS pedidos_aprovados,
    ROUND(SUM(CASE WHEN p.estado_pedido = 'Aprovado' THEN 1 ELSE 0 END) * 100.0 / COUNT(p.pedido_id), 2) AS taxa_aprovacao_percentual
FROM clientes c
JOIN pedidos_credito p ON c.cliente_id = p.cliente_id
GROUP BY 
    CASE 
        WHEN c.idade < 30 THEN '18-29 anos'
        WHEN c.idade BETWEEN 30 AND 50 THEN '30-50 anos'
        ELSE 'Mais de 50 anos'
    END;
```
