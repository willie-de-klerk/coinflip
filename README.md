# coinflip
I flipped a coin ten thousand times using SQL. 

```
CREATE TABLE coinflip_tbl(id INT PRIMARY KEY IDENTITY(1,1) , result BIT);

CREATE PROCEDURE sp_coinflip
AS
BEGIN
	INSERT INTO coinflip_tbl(result) values ((SELECT ROUND(RAND(),0)));	
END
GO
DELETE FROM coinflip_tbl;
DECLARE @flips INT;
SET @flips = 10000;
DECLARE @currentflip INT;
SET @currentflip = 0;
WHILE @currentflip < @flips
	BEGIN
		SET @currentflip = @currentflip +1;
		EXEC sp_coinflip
	END
GO

SELECT  ((SELECT count(result) from coinflip_tbl where result = 1)/10000. * 100.0) as "Heads", ((SELECT count(result) from coinflip_tbl where result = 0)/10000. * 100.0) as "Tails";
```
