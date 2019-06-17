# Ejemplo de algunas consultas SQL que hemos realizado:
Esquema lógico de ciclismo [aquí](https://github.com/santirn/BasesDeDatos-SQL/blob/master/Ciclismo.jpg). 


Obtener el dorsal y el nombre de los ciclistas que han ganado alguna etapa y todos los puertos que
están en ella. No se debe mostrar información sobre las etapas sin puertos de montaña. 

```SQL
-- SOLUCION CON EXISTS
SELECT  DISTINCT DORSAL, NOMBRE
FROM    CICLISTA, ETAPA, PUERTO
WHERE   CICLISTA.DORSAL=ETAPA.DORSAL AND
        ETAPA.NETAPA=PUERTO.NETAPA AND
        NOT EXISTS (SELECT  *
                    FROM    PUERTO
                    WHERE   PUERTO.NETAPA=ETAPA.NETAPA AND
                            PUERTO.DORSAL!=CICLISTA.DORSAL);   
     
                            
-- SOLUCIÓN CON ALL                             
SELECT  DISTINCT DORSAL, NOMBRE
FROM    CICLISTA, ETAPA, PUERTO
WHERE   CICLISTA.DORSAL=ETAPA.DORSAL AND
        ETAPA.NETAPA=PUERTO.NETAPA AND
        CICLISTA.DORSAL = ALL (SELECT DORSAL 
                              FROM    PUERTO
                              WHERE   PUERTO.NETAPA=ETAPA.NETAPA);
```  
