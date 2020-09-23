---
description: EVENTDATA(Transact-SQL)
title: EVENTDATA(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EVENTDATA
- fn_event_data
- EVENTDATA_TSQL
- fn_event_data_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server instance event data [SQL Server]
- event notifications [SQL Server], event status
- events [SQL Server], status information
- EVENTDATA function
- status information [SQL Server], events
- DDL triggers, returning event data
ms.assetid: 03a80e63-6f37-4b49-bf13-dc35cfe46c44
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e37bcd2decf37bffa96a726e4b964cc05bcaffa0
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91115534"
---
# <a name="eventdata-transact-sql"></a>EVENTDATA(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

이 함수는 서버 또는 데이터베이스 이벤트 정보를 반환합니다. 이벤트 알림이 실행되고 지정된 Service Broker가 결과를 수신하면 `EVENTDATA`가 호출됩니다. DDL 또는 로그온 트리거는 `EVENTDATA`의 내부 사용도 지원합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
EVENTDATA( )
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>설명  
`EVENTDATA`는 DDL 또는 로그온 트리거 내에 직접 참조되는 경우에만 데이터를 반환합니다. `EVENTDATA`는 DDL 또는 로그온 트리거가 해당 루틴을 호출하는 경우에도 다른 루틴이 이벤트를 호출하면 null을 반환합니다.
  
`EVENTDATA`에서 반환된 데이터는 다음 트랜잭션 이후에는 유효하지 않습니다.

+ `EVENTDATA`를 명시적으로 호출한 트랜잭션
+ `EVENTDATA`를 암시적으로 호출한 트랜잭션
+ 커밋된 트랜잭션
+ 롤백된 트랜잭션  
  
> [!CAUTION]  
>  `EVENTDATA`는 각 문자에 2바이트를 사용하는 유니코드로 클라이언트에 전송되는 XML 데이터를 반환합니다. `EVENTDATA`는 이러한 유니코드 코드 포인트를 나타낼 수 있는 XML을 반환합니다.  
>   
>  `0x0009`  
>   
>  `0x000A`  
>   
>  `0x000D`  
>   
>  `>= 0x0020 && <= 0xD7FF`  
>   
>  `>= 0xE000 && <= 0xFFFD`  
>   
>  XML은 표시할 수 없으며, [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자 및 데이터에 표시될 수 있는 일부 문자를 허용하지 않습니다. 이전 목록에 표시되지 않은 코드 포인트가 있는 문자 또는 데이터는 물음표(?)로 매핑됩니다.  
  
`CREATE LOGIN` 또는 `ALTER LOGIN` 문이 실행될 때 암호가 표시되지 않습니다. 이를 통해 로그인 보안을 보호합니다.  
  
## <a name="schemas-returned"></a>반환된 스키마  
EVENTDATA는 **xml** 데이터 형식 값을 반환합니다. 기본적으로 모든 이벤트의 스키마 정의는 [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools\Binn\schemas\sqlserver\2006\11\events\events.xsd 디렉터리에 설치됩니다.  
  
[Microsoft SQL Server XML 스키마](https://go.microsoft.com/fwlink/?LinkID=31850) 웹 페이지에도 이벤트 스키마가 있습니다.  
  
특정 이벤트에 대한 스키마를 추출하려면 복합 유형 `EVENT_INSTANCE_<event_type>`에 대한 스키마를 검색하세요. 예를 들어 `DROP_TABLE` 이벤트의 스키마를 추출하려면 `EVENT_INSTANCE_DROP_TABLE`의 스키마를 검색합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-querying-event-data-in-a-ddl-trigger"></a>A. DDL 트리거에서 이벤트 데이터 쿼리  
이 예제에서는 새 데이터베이스 테이블 만들기를 차단하는 DDL 트리거를 만듭니다. `EVENTDATA`에서 생성한 XML 데이터에 XQuery를 사용하면 트리거를 실행하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 캡처됩니다. 자세한 내용은 [XQuery 언어 참조&#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 **표 형태로 결과 표시**를 사용하여 `<TSQLCommand>` 요소를 쿼리하는 경우 명령 텍스트의 줄 바꿈이 표시되지 않습니다. 대신 **텍스트로 결과 표시**를 사용하세요.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER safety   
ON DATABASE   
FOR CREATE_TABLE   
AS   
    PRINT 'CREATE TABLE Issued.'  
    SELECT EVENTDATA().value  
        ('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
   RAISERROR ('New tables cannot be created in this database.', 16, 1)   
   ROLLBACK  
;  
GO  
--Test the trigger.  
CREATE TABLE NewTable (Column1 INT);  
GO  
--Drop the trigger.  
DROP TRIGGER safety  
ON DATABASE;  
GO  
```  
  
> [!NOTE]  
>  이벤트 데이터를 반환하려면 **query()** 메서드 대신 XQuery **value()** 메서드를 사용합니다. **query()** 메서드는 XML 및 출력에서 앰퍼샌드로 이스케이프된 CR/LF(캐리지 리턴 및 줄 바꿈) 인스턴스를 반환하지만 **value()** 메서드는 출력에서는 볼 수 없는 CR/LF 인스턴스를 표시합니다.  
  
### <a name="b-creating-a-log-table-with-event-data-in-a-ddl-trigger"></a>B. DDL 트리거에서 이벤트 데이터가 있는 로그 테이블 만들기  
이 예에서는 모든 데이터베이스 수준 이벤트 정보를 스토리지할 테이블을 만들고 DDL 트리거로 해당 테이블을 채웁니다. `EVENTDATA`에서 생성된 XML 데이터에 XQuery를 사용하면 이벤트 유형과 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 캡처됩니다.  
  
```sql 
USE AdventureWorks2012;  
GO  
CREATE TABLE ddl_log (PostTime DATETIME, DB_User NVARCHAR(100), Event NVARCHAR(100), TSQL NVARCHAR(2000));  
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
   CONVERT(NVARCHAR(100), CURRENT_USER),   
   @data.value('(/EVENT_INSTANCE/EventType)[1]', 'NVARCHAR(100)'),   
   @data.value('(/EVENT_INSTANCE/TSQLCommand)[1]', 'NVARCHAR(2000)') ) ;  
GO  
--Test the trigger.  
CREATE TABLE TestTable (a INT);  
DROP TABLE TestTable ;  
GO  
SELECT * FROM ddl_log ;  
GO  
--Drop the trigger.  
DROP TRIGGER log  
ON DATABASE;  
GO  
--Drop table ddl_log.  
DROP TABLE ddl_log;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [EVENTDATA 함수 사용 ](../../relational-databases/triggers/use-the-eventdata-function.md)   
 [DDL 트리거](../../relational-databases/triggers/ddl-triggers.md)   
 [이벤트 알림](../../relational-databases/service-broker/event-notifications.md)   
 [LOGON 트리거](../../relational-databases/triggers/logon-triggers.md)  
  
  
