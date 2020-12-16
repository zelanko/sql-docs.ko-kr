---
description: EVENTDATA 함수 사용
title: EVENTDATA 함수 사용 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- EVENTDATA function
- DDL triggers, EVENTDATA function
ms.assetid: 675b8320-9c73-4526-bd2f-91ba42c1b604
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5b12fb3c0f29d4f9ef4137c277760593225b5e2e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97426426"
---
# <a name="use-the-eventdata-function"></a>EVENTDATA 함수 사용
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  DDL 트리거를 발생하는 이벤트에 대한 정보는 EVENTDATA 함수를 사용하여 캡처합니다. 이 함수는 **xml** 값을 반환합니다. XML 스키마에는 다음에 대한 정보가 포함됩니다.  
  
-   이벤트의 시간  
  
-   트리거 실행 시 연결의 SPID(시스템 프로세스 ID)  
  
-   트리거를 실행한 이벤트의 유형  
  
 이벤트 유형에 따라 스키마에는 이벤트가 발생한 데이터베이스, 이벤트가 발생한 개체 및 이벤트의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문과 같은 추가 정보가 포함됩니다. 자세한 내용은 [DDL Triggers](../../relational-databases/triggers/ddl-triggers.md)을(를) 참조하세요.  
  
 예를 들어 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스에서 다음 DDL 트리거가 생성된다고 가정해 보십시오.  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR CREATE_TABLE   
AS   
    PRINT 'CREATE TABLE Issued.'  
    SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
   RAISERROR ('New tables cannot be created in this database.', 16, 1)   
   ROLLBACK  
;  
```  
  
 그런 후에 다음 `CREATE TABLE` 문이 실행됩니다.  
  
 `CREATE TABLE NewTable (Column1 int);`  
  
 DDL 트리거의 `EVENTDATA()` 문은 허용되지 않는 `CREATE TABLE` 문의 텍스트를 캡처합니다. 이렇게 하려면 EVENTDATA로 생성된 **xml** 데이터에 대해 XQuery를 사용하여 \<CommandText> 요소를 검색합니다. 자세한 내용은 [XQuery 언어 참조&#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)를 참조하세요.  
  
> [!CAUTION]  
>  EVENTDATA는 CREATE_SCHEMA 이벤트의 데이터와 해당 CREATE SCHEMA 정의(있는 경우)의 <schema_element>를 캡처합니다. 또한 EVENTDATA는 <schema_element> 정의를 별개의 이벤트로 인식합니다. 따라서 CREATE SCHEMA 정의의 <schema_element>가 나타내는 이벤트와 CREATE_SCHEMA 이벤트 둘 다에서 생성된 DDL 트리거는 `TSQLCommand` 데이터 등의 동일한 이벤트 데이터를 두 번 반환할 수 있습니다. 예를 들어 CREATE_SCHEMA 및 CREATE_TABLE 이벤트 둘 다에서 생성된 DDL 트리거가 있으며 다음 일괄 처리가 실행된다고 가정해 보십시오.  
>   
>  `CREATE SCHEMA s`  
>   
>  `CREATE TABLE t1 (col1 int)`  
>   
>  애플리케이션에서 CREATE_TABLE 이벤트의 `TSQLCommand` 데이터를 검색하면 이 데이터는 CREATE_SCHEMA 이벤트가 발생할 때와 CREATE_TABLE 이벤트가 발생할 때 각각 한 번씩, 두 번 표시될 수 있습니다. CREATE_SCHEMA 이벤트 및 해당하는 CREATE SCHEMA 정의의 &lt;schema_element&gt; 텍스트 둘 다에서 DDL 트리거를 만드는 경우를 방지하거나 같은 이벤트가 두 번 처리되지 않도록 하는 논리를 애플리케이션에 구축합니다.  
  
## <a name="alter-table-and-alter-database-events"></a>ALTER TABLE 및 ALTER DATABASE 이벤트  
 ALTER_TABLE 및 ALTER_DATABASE 이벤트에 대한 이벤트 데이터에는 DDL 문의 영향을 받는 다른 개체의 이름 및 유형과 이러한 개체에서 수행되는 동작도 포함됩니다. ALTER_TABLE 이벤트 데이터에는 ALTER TABLE 문의 영향을 받는 열, 제약 조건 또는 트리거의 이름과 영향을 받는 개체에서 수행되는 동작(만들기, 변경, 삭제, 설정 또는 해제)이 포함됩니다. ALTER DATABASE 이벤트 데이터에는 ALTER DATABASE 문의 영향을 받는 파일 또는 파일 그룹의 이름과 영향을 받는 개체에서 수행되는 동작(만들기, 변경, 또는 삭제)이 포함됩니다.  
  
 예를 들어 AdventureWorks 예제 데이터베이스에서 다음 DDL 트리거를 만듭니다.  
  
```  
CREATE TRIGGER ColumnChanges  
ON DATABASE   
FOR ALTER_TABLE  
AS  
-- Detect whether a column was created/altered/dropped.  
SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]', 'nvarchar(max)')  
RAISERROR ('Table schema cannot be modified in this database.', 16, 1);  
ROLLBACK;  
```  
  
 그런 다음 제약 조건을 위반하는 다음 ALTER TABLE 문을 실행합니다.  
  
```  
ALTER TABLE Person.Address ALTER COLUMN ModifiedDate date;   
```  
  
 DDL 트리거의 EVENTDATA() 문은 허용되지 않는 `ALTER TABLE` 문의 텍스트를 캡처합니다.  
  
## <a name="example"></a>예제  
 EVENTDATA 함수를 사용하여 이벤트 로그를 만들 수 있습니다. 다음 예에서는 테이블을 만들어 이벤트 정보를 저장합니다. 그런 다음 데이터베이스 수준의 DDL 이벤트가 발생할 때마다 다음 정보로 테이블을 채우는 DDL 트리거가 현재 데이터베이스에 생성됩니다.  
  
-   이벤트의 시간(GETDATE 함수 사용)  
  
-   해당 세션에 이벤트가 발생한 데이터베이스 사용자(CURRENT_USER 함수 사용)  
  
-   이벤트 유형  
  
-   이벤트를 구성한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문  
  
 그런 다음 EVENTDATA로 생성된 **xml** 데이터에 대해 XQuery를 사용하여 마지막 두 항목도 캡처합니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE ddl_log (PostTime datetime, DB_User nvarchar(100), Event nvarchar(100), TSQL nvarchar(2000));  
GO  
CREATE TRIGGER log   
ON DATABASE   
FOR DDL_DATABASE_LEVEL_EVENTS   
AS  
DECLARE @data XML  
SET @data = EVENTDATA()  
INSERT ddl_log   
   (PostTime, DB_User, Event, TSQL)   
   VALUES   
   (GETDATE(),   
   CONVERT(nvarchar(100), CURRENT_USER),   
   @data.value('(/EVENT_INSTANCE/EventType)[1]', 'nvarchar(100)'),   
   @data.value('(/EVENT_INSTANCE/TSQLCommand)[1]', 'nvarchar(2000)') ) ;  
GO  
--Test the trigger  
CREATE TABLE TestTable (a int)  
DROP TABLE TestTable ;  
GO  
SELECT * FROM ddl_log ;  
GO  
```  
  
> [!NOTE]  
>  이벤트 데이터를 반환하려면 **query()** 메서드보다 XQuery의 **value()** 메서드를 사용하는 것이 좋습니다. **query()** 메서드는 XML 및 출력에서 앰퍼샌드로 이스케이프된 CR/LF(캐리지 리턴 및 줄 바꿈) 인스턴스를 반환하지만 **value()** 메서드는 출력에서는 볼 수 없는 CR/LF 인스턴스를 표시합니다.  
  
 이와 유사한 DDL 트리거 예가 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스와 함께 제공됩니다. 이 예를 사용하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 데이터베이스 트리거 폴더를 찾으십시오. 이 폴더는 **데이터베이스의** 프로그래밍 기능 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 폴더 아래에 있습니다. **ddlDatabaseTriggerLog** 를 마우스 오른쪽 단추로 클릭한 다음 **데이터베이스 트리거 스크립팅** 을 선택합니다. DDL 트리거 **ddlDatabaseTriggerLog** 는 기본적으로 해제되어 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [DDL 이벤트](../../relational-databases/triggers/ddl-events.md)   
 [DDL 이벤트 그룹](../../relational-databases/triggers/ddl-event-groups.md)  
  
  
