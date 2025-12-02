# SQL Injection Basics - PortSwigger Academy

## Lab 1: Retrieval of hidden data.
**Objetivo:** Obtener productos no publicados.
**Metodologia:**
Detecte que el filtro de categoria se reflejaba en la URL.
Use el payload `' OR 1=1--` para hacer la consulta verdadera.
**Resultado:**
La aplicacion mostro todo los productos.

