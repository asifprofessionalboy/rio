SELECT 
    W.VendorCode,
    W.VendorName,
    W.WorkOrderNo,
    W.PROC_MONTH,
    W.WorkManCategory,       -- Skill category (Skilled/Unskilled)
    COUNT(W.WorkManCategory) AS TotalWorkers, -- Count of workers in each category
    SUM(W.TotPaymentDays) AS TotalPaymentDays, -- Total payment days
    SUM(W.NetWagesAmt) AS TotalNetWages,       -- Total net wages
    SUM(P.PFAmt) AS TotalPFAmt,               -- Total PF amount
    SUM(P.ESIAmt) AS TotalESIAmt,             -- Total ESI amount
    SUM(P.GrossWages) AS TotalGrossWages      -- Total gross wages
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
    W.WorkManCategory
ORDER BY 
    W.PROC_MONTH;
