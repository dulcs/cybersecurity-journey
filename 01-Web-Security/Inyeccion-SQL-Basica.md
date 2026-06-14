# 💉 Inyección SQL (SQLi) Básica

## 🧠 Mecanismo Técnico (El "Por Qué")
*   **Definición corta:** Ocurre cuando los datos del usuario se mezclan con la lógica de la consulta a la base de datos.
*   **Fallo de diseño:** La aplicación no sanitiza la entrada y el motor SQL interpreta los datos como comandos ejecutables.

## 🛠️ Vectores de Ataque Comunes
*   `' OR 1=1--` -> Rompe la lógica de autenticación (siempre es verdadero).
*   `' UNION SELECT NULL--` -> Permite extraer datos de otras tablas combinando resultados.

## 🧪 Laboratorios Resueltos (PortSwigger)
### Lab 1: []
*   **Objetivo:** 
*   **Metodología / Comandos usados:**
```sql
    
    ```
*   **Evidencia (Captura/Flag):** 

## 🛡️ Mitigación Defensiva (Código Seguro)
*   **Solución definitiva:** Uso estricto de **Consultas Preparadas (Parameterized Queries)**. Los datos se tratan estrictamente como cadenas de texto, nunca como código ejecutable.