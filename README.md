# databases

### Code convention
- table name: `MyTable`
- table column: `MyColumn`
- table primary key: `TableId`
- foreign key constrain: `FK_MyTable_ForeignTableId`
- column check constraint: `CK_MyTable_MyColumn`
- view name: `VI_LogicalName`
- stored procedure: `usp_LogicalName`

**Code example:**
```T-SQL
SELECT
    t1.Value1  AS Val1
    , t1.Value2  AS Val2
    , t2.Value3  AS Val3
INNER JOIN dbo.Table3 AS t2
        ON t1.Value1 = t2.Value1
WHERE t1.Value1 > 1
    AND t2.Value2 >= 101
```

```T-SQL
DECLARE @myGoodVarchareVariable  varchar(50);
DECLARE @myGoodNVarchareVariable nvarchar(90);
DECLARE @myGoodCharVariable      char(7);
DECLARE @myGoodNCharVariable     nchar(10);
```

```T-SQL
CREATE PROCEDURE usp_FacilityFinesPerPeriod
    @FacilityId INT,
    @FromDate DATE,
    @ToDate DATE
AS
BEGIN
    SELECT
        F.Name AS FacilityName,
        SUM(ERV.Fine) AS FineSum
    FROM
        EnergyResourceViolations AS ERV
    INNER JOIN Facilities AS F
            ON ERV.FacilityId = F.Id
    WHERE F.Id = @FacilityId
        AND ERV.VisitDate BETWEEN @FromDate AND @ToDate
    GROUP BY F.Name
END;
```