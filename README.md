
select W.VendorCode,W.VendorName,W.WorkOrderNo,W.PROC_MONTH, sum(W.TotPaymentDays) as Tot ,count (W.WorkManCategory),W.NetWagesAmt,
P.PFAmt,p.ESIAmt,P.GrossWages
from App_Online_Wages_Details W
inner join App_PF_ESI_Details P
On  P.WorkOrderNo  = W.WorkOrderNo 
where VendorCode='16293' and W.WorkOrderNo='4700022667' group by WorkManCategory order by PROC_MONTH
