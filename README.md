select count(distinct ah.Hdate)
from App_HolidayMaster ah
where DATEPART(month, ah.Hdate) = '10'
  and DATEPART(year, ah.Hdate) = '2024'
  and ah.Location = 'KTP'
  and (
    exists (
      select 1
      from App_AttendanceDetails
      where dates = ah.Hdate - 1
        and AadharNo = AttDtl.AadharNo
        and WorkOrderNo = AttDtl.WorkOrderNo
        and CAST(present AS INT) >= 1
    ) or exists (
      select 1
      from App_AttendanceDetails
      where dates = ah.Hdate + 1
        and AadharNo = AttDtl.AadharNo
        and WorkOrderNo = AttDtl.WorkOrderNo
        and CAST(present AS INT) >= 1
    )
  )
