Esta es una lista de queries que nos sirven para saber que todo está
bien.

El resultado de este query debe coincidir con la deuda pendiente del
análisis de vencimiento

    SELECT 
        SUM(CASE WHEN tipo_doc IN ('ADEL','AJNA','AJNM','N/CR') THEN -1 ELSE 1 END * saldo)
    FROM 
        docum_cc

Esta es la distribución del anterior número por tipo de documento

    SELECT 
        tipo_doc,
        SUM(CASE WHEN tipo_doc IN ('ADEL','AJNA','AJNM','N/CR') THEN -1 ELSE 1 END * saldo)
    FROM 
        docum_cc
    GROUP BY
        tipo_doc

Estas son las facturas donde no cuadra el saldo pendiente en la tabla de
documentos y en la tabla de facturas

    SELECT 
        D.co_cli AS codigoCliente,
        C.cli_des AS nombreCliente,
        D.tipo_doc AS tipo,
        D.nro_doc AS documento,
        D.fec_emis AS emision,
        D.saldo AS saldoDocumento,
        F.saldo AS saldoFactura
    FROM
        docum_cc D LEFT JOIN factura F ON D.nro_doc = F.fact_num
        LEFT JOIN clientes C ON D.co_cli = C.co_cli
    WHERE
        D.tipo_doc = 'FACT' AND D.nro_doc = F.fact_num AND D.saldo != F.saldo
    ORDER BY
        D.co_cli,
        D.nro_doc

Estas es el monto de diferencia entre la tabla de documento y la tabla
de facturas

    SELECT 
        SUM(D.saldo) AS saldoDocumento,
        SUM(F.saldo) AS saldoFactura,
        SUM(F.saldo) - SUM(D.saldo) AS saldoDiferencia
    FROM
        docum_cc D LEFT JOIN factura F ON D.nro_doc = F.fact_num
    WHERE
        D.tipo_doc = 'FACT' AND D.nro_doc  = f.fact_num AND D.saldo != F.saldo
