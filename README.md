SELECT 
    W.VendorCode,
    W.VendorName,
    W.WorkOrderNo,
    W.PROC_MONTH,
    SUM(W.TotPaymentDays) AS Tot,
    COUNT(W.WorkManCategory) AS WorkManCategoryCount,
    W.NetWagesAmt,
    P.PFAmt,
    P.ESIAmt,
    P.GrossWages
FROM 
    App_Online_Wages_Details W
INNER JOIN 
    App_PF_ESI_Details P
ON  
    P.WorkOrderNo = W.WorkOrderNo
WHERE 
    W.VendorCode = '16293' 
    AND W.WorkOrderNo = '4700022667'
GROUP BY 
    W.VendorCode, 
    W.VendorName, 
    W.WorkOrderNo, 
    W.PROC_MONTH, 
    W.NetWagesAmt, 
    P.PFAmt, 
    P.ESIAmt, 
    P.GrossWages
ORDER BY 
    W.PROC_MONTH;
