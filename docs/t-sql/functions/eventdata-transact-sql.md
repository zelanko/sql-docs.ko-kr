---
title: EVENTDATA (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
- events [SQL Server], status infromation
- EVENTDATA function
- status information [SQL Server], events
- DDL triggers, returning event data
ms.assetid: 03a80e63-6f37-4b49-bf13-dc35cfe46c44
caps.latest.revision: 55
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3b385ee993ab576307b6609670761deae9a7a1f6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="eventdata-transact-sql"></a>EVENTDATA(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  서버 또는 데이터베이스 이벤트에 대한 정보를 반환합니다. EVENTDATA는 이벤트 알림이 발생할 때 호출되며 결과는 지정된 Service Broker에 반환됩니다. 또한 EVENTDATA는 DDL 또는 LOGON 트리거 본문 내에서 사용할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
EVENTDATA( )  
```  
  
## <a name="remarks"></a>주의  
 EVENTDATA는 DDL 또는 LOGON 트리거 내에 직접 참조되는 경우에만 데이터를 반환합니다. 다른 루틴에서 EVENTDATA를 호출한 경우 해당 루틴을 DDL 또는 로그온 트리거가 호출한 것이라 해도 EVENTDATA는 Null을 반환합니다.  
  
 EVENTDATA가 반환한 데이터는 EVENTDATA를 호출한 트랜잭션이 암시적으로나 명시적으로 커밋되거나 롤백된 이후에는 유효하지 않습니다.  
  
> [!CAUTION]  
>  EVENTDATA는 XML 데이터를 반환합니다. 이 데이터는 각 문자에 대해 2바이트를 사용하는 유니코드로 클라이언트에 전송됩니다. 다음 유니코드 코드 포인트는 EVENTDATA가 반환한 XML로 표시할 수 있습니다.  
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
>  [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자에 표시되는 일부 문자와 데이터는 XML로 표현되거나 허용되지 않습니다. 이전 목록에 표시되지 않은 코드 포인트가 있는 문자 또는 데이터는 물음표(?)로 매핑됩니다.  
  
 로그인의 보안을 보호하기 위해 CREATE LOGIN 또는 ALTER LOGIN 문이 실행될 때 암호가 표시되지 않습니다.  
  
## <a name="schemas-returned"></a>반환된 스키마  
 형식의 값을 반환 하는 EVENTDATA **xml**합니다. 기본적으로 모든 이벤트에 대한 스키마 정의는 [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools\Binn\schemas\sqlserver\2006\11\events\events.xsd 디렉터리에 설치됩니다.  
  
 에 이벤트 스키마를 게시 또는 [Microsoft SQL Server XML 스키마](http://go.microsoft.com/fwlink/?LinkID=31850) 웹 페이지입니다.  
  
 특정 이벤트에 대한 스키마를 추출하려면 복합 유형 `EVENT_INSTANCE_\<event_type>`에 대한 스키마를 검색하세요. 예를 들어 DROP_TABLE 이벤트에 대한 스키마를 추출하려면 `EVENT_INSTANCE_DROP_TABLE`에 대한 스키마를 검색하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-querying-event-data-in-a-ddl-trigger"></a>1. DDL 트리거에서 이벤트 데이터 쿼리  
 다음 예에서는 DDL 트리거를 만들어 데이터베이스에 새 테이블이 생성되는 것을 방지합니다. 트리거를 실행하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 EVENTDATA가 생성한 XML 데이터에 대해 XQuery를 사용하여 캡처합니다. 자세한 내용은 [XQuery 언어 참조&#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)를 참조하세요.  
  
> [!NOTE]  
>  쿼리할 때는 `\<TSQLCommand>` 요소를 사용 하 여 **표 형태로 결과** 에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 명령 텍스트에 줄 바꿈이 표시 되지 않습니다. 사용 하 여 **텍스트로 결과 표시** 대신 합니다.  
  
```  
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
CREATE TABLE NewTable (Column1 int);  
GO  
--Drop the trigger.  
DROP TRIGGER safety  
ON DATABASE;  
GO  
```  
  
> [!NOTE]  
>  이벤트 데이터를 반환 하려는 경우 XQuery를 사용 하는 것이 좋습니다 **value ()** 메서드 대신는 **query ()** 메서드. **query ()** 메서드 반환 XML 및 앰퍼샌드로 이스케이프 된 캐리지 반환 하 고 줄 출력에서 (CR/LF) 인스턴스를 바꿈 동안는 **value ()** 메서드 출력에 표시 되지 않도록 CR/LF 인스턴스 렌더링 합니다.  
  
### <a name="b-creating-a-log-table-with-event-data-in-a-ddl-trigger"></a>2. DDL 트리거에서 이벤트 데이터가 있는 로그 테이블 만들기  
 다음 예에서는 모든 데이터베이스 수준 이벤트에 대한 정보를 저장할 테이블을 만들고 DDL 트리거로 이 테이블을 채웁니다. 이벤트 유형 및 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 `EVENTDATA`가 생성한 XML 데이터에 대해 XQuery를 사용하여 캡처됩니다.  
  
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
--Test the trigger.  
CREATE TABLE TestTable (a int);  
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
  
## <a name="see-also"></a>관련 항목:  
 [EVENTDATA 함수 사용](../../relational-databases/triggers/use-the-eventdata-function.md)   
 [DDL 트리거](../../relational-databases/triggers/ddl-triggers.md)   
 [이벤트 알림](../../relational-databases/service-broker/event-notifications.md)   
 [LOGON 트리거](../../relational-databases/triggers/logon-triggers.md)  
  
  
