# SQL-Join
SELECT
    C2.Name AS Data_Source_Name,
    C.Name AS Dependent_Item_Name,
    C.Path AS Dependent_Item_Path
FROM
   ReportServer.dbo.DataSource AS DS
INNER JOIN
   ReportServer.dbo.Catalog AS C
ON DS.ItemID = C.ItemID 
AND DS.Link IN (SELECT ItemID FROM ReportServer.dbo.Catalog
WHERE Type = 5) --Type 5 identifies data sources
FULL OUTER JOIN
ReportServer.dbo.Catalog C2
ON DS.Link = C2.ItemID
WHERE
  C2.Type = 5 
  and
  C2.Name = 'CCS_Quality'
ORDER BY
  C2.Name ASC,
  C.Name ASC;
