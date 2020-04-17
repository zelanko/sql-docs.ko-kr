---
title: UDT 데이터 조작 | 마이크로 소프트 문서
description: 이 문서에서는 SQL Server 데이터베이스의 UDT 열에 데이터를 삽입, 선택 및 업데이트하는 방법에 대해 설명합니다.
ms.custom: ''
ms.date: 12/05/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- CAST function
- data deletions [CLR integration]
- data insertions [CLR integration]
- CONVERT function
- data updates [CLR integration]
- comparing data
- updating data [CLR integration]
- removing data
- IsByteOrdered property
- variables [CLR integration]
- data manipulation [CLR integration]
- user-defined types [CLR integration], data manipulation
- deleting data
- UDTs [CLR integration], data manipulation
- invoking UDT methods
- inserting data
ms.assetid: 51b1a5f2-7591-4e11-bfe2-d88e0836403f
author: rothja
ms.author: jroth
ms.openlocfilehash: 4ff4b620f2f06243b23b4c540f4c99b3c3cafa41
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486935"
---
# <a name="working-with-user-defined-types---manipulating-udt-data"></a>사용자 정의 형식 작업 - UDT 데이터 조작
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[tsql](../../includes/tsql-md.md)]에서는 UDT(사용자 정의 형식) 열의 데이터를 수정할 때 INSERT, UPDATE 또는 DELETE 문에 대한 특별한 구문을 제공하지 않습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST 또는 CONVERT 함수는 네이티브 데이터 형식을 UDT 형식으로 캐스트하는 데 사용됩니다.  
  
## <a name="inserting-data-in-a-udt-column"></a>UDT 열에 데이터 삽입  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 세 행의 샘플 데이터를 **포인트** 테이블에 삽입합니다. **점** 데이터 형식은 UDT의 속성으로 노출되는 X 및 Y 정수 값으로 구성됩니다. CAST 또는 CONVERT 함수를 사용하여 쉼표 구분 X 및 Y 값을 **포인트** 유형으로 캐스팅해야 합니다. 처음 두 문은 CONVERT 함수를 사용하여 문자열 값을 **Point** 유형으로 변환하고 세 번째 문은 CAST 함수를 사용합니다.  
  
```sql  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '3,4'));  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '1,5'));  
INSERT INTO dbo.Points (PointValue) VALUES (CAST ('1,99' AS Point));  
```  
  
## <a name="selecting-data"></a>데이터 선택  
 다음 SELECT 문은 UDT의 이진 값을 선택합니다.  
  
```sql  
SELECT ID, PointValue FROM dbo.Points  
```  
  
 읽을 수 있는 형식으로 표시되는 출력을 보려면 값을 문자열 표현으로 변환하는 **Point** UDT의 **ToString** 메서드를 호출합니다.  
  
```sql  
SELECT ID, PointValue.ToString() AS PointValue   
FROM dbo.Points;  
```  
  
 다음 결과가 생성됩니다.  
  
```  
ID PointValue  
-- ----------  
 1 3,4  
 2 1,5  
 3 1,99  
```  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST 및 CONVERT 함수를 사용하여 동일한 결과를 얻을 수도 있습니다.  
  
```sql  
SELECT ID, CAST(PointValue AS varchar)   
FROM dbo.Points;  
  
SELECT ID, CONVERT(varchar, PointValue)   
FROM dbo.Points;  
```  
  
 **점** UDT는 X 및 Y 좌표를 속성으로 노출하여 개별적으로 선택할 수 있습니다. 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 X 및 Y 좌표를 개별적으로 선택합니다.  
  
```sql  
SELECT ID, PointValue.X AS xVal, PointValue.Y AS yVal   
FROM dbo.Points;  
```  
  
 X 및 Y 속성은 결과 집합에 표시되는 정수 값을 반환합니다.  
  
```  
ID xVal yVal  
-- ---- ----  
 1    3    4  
 2    1    5  
 3    1   99  
```  
  
## <a name="working-with-variables"></a>변수 작업  
 DECLARE 문에 변수를 사용하여 UDT 형식에 변수를 할당할 수 있습니다. 다음 문은 [!INCLUDE[tsql](../../includes/tsql-md.md)] SET 문을 사용하여 값을 할당하고 변수에 UDT의 **ToString** 메서드를 호출하여 결과를 표시합니다.  
  
```sql  
DECLARE @PointValue Point;  
SET @PointValue = (SELECT PointValue FROM dbo.Points  
    WHERE ID = 2);  
SELECT @PointValue.ToString() AS PointValue;  
```  
  
 결과 집합에 변수 값이 표시됩니다.  
  
```  
PointValue  
----------  
-1,5  
```  
  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 변수 할당에 SET 대신 SELECT를 사용하여 동일한 결과를 얻습니다.  
  
```sql  
DECLARE @PointValue Point;  
SELECT @PointValue = PointValue FROM dbo.Points  
    WHERE ID = 2;  
SELECT @PointValue.ToString() AS PointValue;  
```  
  
 변수 할당에 SELECT 및 SET를 사용할 경우의 차이점은 SELECT를 사용하면 하나의 SELECT 문에서 여러 변수를 할당할 수 있는 반면 SET 구문에서는 각 변수 할당에 고유한 SET 문이 필요하다는 것입니다.  
  
## <a name="comparing-data"></a>데이터 비교  
 클래스를 정의할 때 **IsByteOrdered** 속성을 **true로** 설정한 경우 비교 연산자에서 UDT의 값을 비교할 수 있습니다. 자세한 내용은 [사용자 정의 유형 만들기](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)를 참조하십시오.  
  
```sql  
SELECT ID, PointValue.ToString() AS Points   
FROM dbo.Points  
WHERE PointValue > CONVERT(Point, '2,2');  
```  
  
 값 자체가 비교되는 경우 **IsByteOrdered** 설정에 관계없이 UDT의 내부 값을 비교할 수 있습니다. 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 X가 Y보다 큰 행을 선택합니다.  
  
```sql  
SELECT ID, PointValue.ToString() AS PointValue   
FROM dbo.Points  
WHERE PointValue.X < PointValue.Y;  
```  
  
 일치하는 PointValue를 검색하는 이 쿼리와 같이 변수에 비교 연산자를 사용할 수도 있습니다.  
  
```sql  
DECLARE @ComparePoint Point;  
SET @ComparePoint = CONVERT(Point, '3,4');  
SELECT ID, PointValue.ToString() AS MatchingPoint   
FROM dbo.Points  
WHERE PointValue = @ComparePoint;  
```  
  
## <a name="invoking-udt-methods"></a>UDT 메서드 호출  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 UDT에 정의된 메서드를 호출할 수도 있습니다. **포인트** 클래스에는 **거리,** **거리, 거리로부터의**세 가지 방법 및 **거리로부터XY가**포함되어 있습니다. 이러한 세 가지 방법을 정의하는 코드 목록은 [사용자 정의 형식 코딩을](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)참조하십시오.  
  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 **PointValue.Distance** 메서드를 호출합니다.  
  
```sql  
SELECT ID, PointValue.X AS [Point.X],   
    PointValue.Y AS [Point.Y],  
    PointValue.Distance() AS DistanceFromZero   
FROM dbo.Points;  
```  
  
 결과는 **거리** 열에 표시됩니다.  
  
```  
ID X  Y  Distance  
-- -- -- ----------------  
 1  3  4                5  
 2  1  5 5.09901951359278  
 3  1 99 99.0050503762308  
```  
  
 **DistanceFrom** 메서드는 **Point** 데이터 형식의 인수를 취하고 지정된 점에서 PointValue까지의 거리를 표시합니다.  
  
```sql  
SELECT ID, PointValue.ToString() AS Pnt,  
   PointValue.DistanceFrom(CONVERT(Point, '1,99')) AS DistanceFromPoint  
FROM dbo.Points;  
```  
  
 결과는 테이블의 각 행에 대한 **DistanceFrom** 메서드의 결과를 표시합니다.  
  
```  
ID Pnt DistanceFromPoint  
-- --- -----------------  
 1 3,4  95.0210502993942  
 2 1,5                94  
 3 1,9                90  
```  
  
 **DistanceFromXY** 메서드는 점을 개별적으로 인수로 사용합니다.  
  
```sql  
SELECT ID, PointValue.X as X, PointValue.Y as Y,   
PointValue.DistanceFromXY(1, 99) AS DistanceFromXY   
FROM dbo.Points  
```  
  
 결과 집합은 **DistanceFrom** 메서드와 동일합니다.  
  
## <a name="updating-data-in-a-udt-column"></a>UDT 열의 데이터 업데이트  
 UDT 열의 데이터를 업데이트하려면 [!INCLUDE[tsql](../../includes/tsql-md.md)] UPDATE 문을 사용합니다. UDT의 메서드를 사용하여 개체 상태를 업데이트할 수도 있습니다. 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 테이블의 행 하나를 업데이트합니다.  
  
```sql  
UPDATE dbo.Points  
SET PointValue = CAST('1,88' AS Point)  
WHERE ID = 3  
```  
  
 UDT 요소를 개별적으로 업데이트할 수도 있습니다. 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 Y 좌표만 업데이트합니다.  
  
```sql  
UPDATE dbo.Points  
SET PointValue.Y = 99  
WHERE ID = 3  
```  
  
 UDT가 **true로**설정된 바이트 순서로 정의된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 경우 WHERE 절에서 UDT 열을 평가할 수 있습니다.  
  
```sql  
UPDATE dbo.Points  
SET PointValue = '4,5'  
WHERE PointValue = '3,4';  
```  
  
### <a name="updating-limitations"></a>업데이트 제한  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 한 번에 여러 속성을 업데이트할 수는 없습니다. 예를 들어 한 UPDATE 문에서 동일한 열 이름을 두 번 사용할 수 없으므로 다음 UPDATE 문은 오류로 인해 실패합니다.  
  
```sql  
UPDATE dbo.Points  
SET PointValue.X = 5, PointValue.Y = 99  
WHERE ID = 3  
```  
  
 각 점을 개별적으로 업데이트하려면 Point UDT 어셈블리에 변경자(mutator) 메서드를 만들어야 합니다. 다음과 같이 변경자(mutator) 메서드를 호출하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] UPDATE 문에서 개체를 업데이트할 수 있습니다.  
  
```sql  
UPDATE dbo.Points  
SET PointValue.SetXY(5, 99)  
WHERE ID = 3  
```  
  
## <a name="deleting-data-in-a-udt-column"></a>UDT 열의 데이터 삭제  
 UDT의 데이터를 삭제하려면 [!INCLUDE[tsql](../../includes/tsql-md.md)] DELETE 문을 사용합니다. 다음 문은 WHERE 절에 지정된 조건과 일치하는 테이블의 모든 행을 삭제합니다. DELETE 문에서 WHERE 절을 생략하면 테이블의 모든 행이 삭제됩니다.  
  
```sql  
DELETE FROM dbo.Points  
WHERE PointValue = CAST('1,99' AS Point)  
```  
  
 다른 행 값은 그대로 두고 UDT 열의 값을 제거하려면 UPDATE 문을 사용합니다. 이 예에서는 PointValue를 null로 설정합니다.  
  
```sql  
UPDATE dbo.Points  
SET PointValue = null  
WHERE ID = 2  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL 서버의 사용자 정의 형식 작업](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)  
  
  
