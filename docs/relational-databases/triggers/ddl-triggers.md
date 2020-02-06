---
title: DDL 트리거 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- DDL triggers, about DDL triggers
ms.assetid: 1a4a6564-9820-4a14-9305-2c0e9ea37454
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b4647814765225a2c1deeedd05f77bed80d7e992
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68056148"
---
# <a name="ddl-triggers"></a>DDL 트리거
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  DDL 트리거는 다양한 DDL(데이터 정의 언어) 이벤트에 대한 응답으로 실행됩니다. 이러한 이벤트는 주로 CREATE, ALTER, DROP, GRANT, DENY, REVOKE 또는 UPDATE STATISTICS 키워드로 시작하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 해당합니다. DDL과 같은 작업을 수행하는 특정 시스템 저장 프로시저에서 DDL 트리거가 발생할 수도 있습니다.  
  
 다음과 같은 경우 DDL 트리거를 사용합니다.  
  
-   데이터베이스 스키마에 대한 특정 변경 작업을 방지하려는 경우  
  
-   데이터 스키마가 변경될 때 데이터베이스에서 특정 작업이 수행되게 하려는 경우  
  
-   데이터베이스 스키마의 변경 내용이나 이벤트를 기록하려는 경우  
  
> [!IMPORTANT]  
>  DDL 트리거를 테스트하여 실행된 시스템 저장 프로시저에 대한 응답을 확인합니다. 예를 들어 CREATE TYPE 문과 **sp_addtype** 저장 프로시저는 모두 CREATE_TYPE 이벤트에서 생성되는 DDL 트리거를 발생시킵니다.  
  
## <a name="types-of-ddl-triggers"></a>DDL 트리거 유형  
 ### <a name="transact-sql-ddl-trigger"></a>Transact-SQL DDL 트리거  
 서버 범위 또는 데이터베이스 범위 이벤트에 대한 응답으로 하나 이상의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하는 특수 유형의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저입니다. 예를 들어 ALTER SERVER CONFIGURATION과 같은 문을 실행하거나 DROP TABLE을 사용하여 테이블을 삭제하면 DDL 트리거가 실행될 수 있습니다.  
  
 ### <a name="clr-ddl-trigger"></a>CLR DDL 트리거  
 CLR 트리거는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 실행하는 대신 .NET Framework에서 생성되고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업로드되는 어셈블리 멤버인 관리 코드로 작성된 하나 이상의 메서드를 실행합니다.  
  
 DDL 트리거를 시작하는 DDL 문이 실행된 후에만 DDL 트리거가 시작됩니다. DDL 트리거는 INSTEAD OF 트리거로 사용될 수 없습니다. DDL 트리거는 로컬 또는 전역 임시 테이블과 저장 프로시저에 영향을 주는 이벤트에 대한 응답으로 실행되지 않습니다.  
  
 DDL 트리거는 특수 **inserted** 및 **deleted** 테이블을 만들 수 없습니다.  
  
 DDL 트리거를 실행하는 이벤트에 대한 정보 및 트리거로 변경되는 내용은 EVENTDATA 함수를 사용하여 확인할 수 있습니다.  
  
 각 DDL 이벤트에 대해 만들 다중 트리거입니다.  
  
 DDL 트리거는 DML 트리거와 달리 스키마로 범위가 한정되지 않습니다. DDL 트리거에 대한 메타데이터를 쿼리하는 데 OBJECT_ID, OBJECT_NAME, OBJECTPROPERTY 및 OBJECTPROPERTYEX와 같은 함수는 사용할 수 없습니다. 대신 카탈로그 뷰를 사용하세요.  
  
 서버 범위 DDL 트리거는 SQL Server Management Studio 개체 탐색기의 **트리거** 폴더에 나타납니다. 이 폴더는 **서버 개체** 폴더 아래에 있습니다. 데이터베이스 범위 DDL 트리거는 **데이터베이스 트리거** 폴더에 나타납니다. 이 폴더는 해당 데이터베이스의 **프로그래밍 기능** 폴더 아래에 있습니다.  
  
> [!IMPORTANT]  
>  사용 권한 수준을 높이고 트리거를 실행하더라도 트리거 내의 악성 코드가 실행될 수 있습니다. 이 위협을 완화하는 방법은 [트리거 보안 관리](../../relational-databases/triggers/manage-trigger-security.md)를 참조하세요.  
  
## <a name="ddl-trigger-scope"></a>DDL 트리거 범위  
 DDL 트리거는 현재 데이터베이스나 서버에서 처리되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 이벤트에 응답하여 시작될 수 있습니다. 트리거의 범위는 이벤트에 따라 달라집니다. 예를 들어 CREATE_TABLE 이벤트에 대한 응답으로 시작되도록 만들어진 DDL 트리거는 데이터베이스 또는 서버 인스턴스에서 CREATE_TABLE 이벤트가 발생할 때마다 시작될 수 있습니다. CREATE_LOGIN 이벤트에 대한 응답으로 시작되도록 만들어진 DDL 트리거는 서버 인스턴스에서 CREATE_LOGIN 이벤트가 발생할 경우에만 시작될 수 있습니다.  
  
 다음 예에서는 데이터베이스에서 `safety` 또는 `DROP_TABLE` 이벤트가 발생할 때마다 DDL 트리거 `ALTER_TABLE` 가 시작됩니다.  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_TABLE, ALTER_TABLE   
AS   
   PRINT 'You must disable Trigger "safety" to drop or alter tables!'   
   ROLLBACK;  
```  
  
 다음 예에서는 현재 서버 인스턴스에서 `CREATE_DATABASE` 이벤트가 발생할 경우 DLL 트리거가 메시지를 출력합니다. 또한 `EVENTDATA` 함수를 사용하여 해당 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 텍스트를 검색합니다. DDL 트리거와 함께 EVENTDATA를 사용하는 방법은 [EVENTDATA 함수 사용](../../relational-databases/triggers/use-the-eventdata-function.md)을 참조하세요.  
  
```  
IF EXISTS (SELECT * FROM sys.server_triggers  
    WHERE name = 'ddl_trig_database')  
DROP TRIGGER ddl_trig_database  
ON ALL SERVER;  
GO  
CREATE TRIGGER ddl_trig_database   
ON ALL SERVER   
FOR CREATE_DATABASE   
AS   
    PRINT 'Database Created.'  
    SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
GO  
DROP TRIGGER ddl_trig_database  
ON ALL SERVER;  
GO  
  
```  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 지정 가능한 범위에 매핑하는 목록은 이 항목의 뒷부분에 나오는 "DDL 트리거를 시작하기 위한 특정 DDL 문 선택" 섹션에 제공된 링크를 통해 볼 수 있습니다.  
  
 데이터베이스 범위 DDL 트리거는 해당 트리거를 만든 데이터베이스에 개체로 저장됩니다. **master** 데이터베이스에서 DDL 트리거를 만들 수 있으며 이러한 DDL 트리거는 사용자가 디자인한 데이터베이스에서 만든 DDL 트리거와 똑같이 동작합니다. DDL 트리거에 대한 정보는 **sys.triggers** 카탈로그 뷰를 쿼리하여 얻을 수 있습니다. **sys.triggers** 는 트리거가 만들어진 데이터베이스 컨텍스트 내에서 또는 **master.sys.triggers**와 같이 데이터베이스 이름을 식별자로 지정하여 쿼리할 수 있습니다.  
  
 서버 범위 DDL 트리거는 **master** 데이터베이스에 개체로 저장됩니다. 그러나 서버 범위 DDL 트리거에 대한 정보는 임의의 데이터베이스 컨텍스트에서 **sys.server_triggers** 카탈로그 뷰를 쿼리하여 얻을 수 있습니다.  
  
## <a name="specifying-a-transact-sql-statement-or-group-of-statements"></a>Transact-SQL 문 또는 문 그룹 지정  
  
### <a name="selecting-a-particular-ddl-statement-to-fire-a-ddl-trigger"></a>DDL 트리거를 시작하기 위한 특정 DDL 문 선택  
 하나 이상의 특정 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 실행된 이후에 DDL 트리거가 시작되도록 만들 수 있습니다. 이전 예에서 `safety` 트리거는 `DROP_TABLE` 또는 `ALTER_TABLE` 이벤트가 발생한 이후에 시작됩니다. DDL 트리거를 시작하도록 지정할 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 목록과 트리거 시작 범위는 [DDL 이벤트](../../relational-databases/triggers/ddl-events.md)를 참조하세요.  
  
### <a name="selecting-a-predefined-group-of-ddl-statements-to-fire-a-ddl-trigger"></a>DDL 트리거를 시작하기 위한 미리 정의된 DDL 문 그룹 선택  
 DDL 트리거는 미리 정의된 유사 이벤트 그룹에 속한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 이벤트가 실행된 이후에 시작될 수 있습니다. 예를 들어 CREATE TABLE, ALTER TABLE 또는 DROP TABLE 문이 실행된 이후에 DDL 트리거가 시작되도록 하려면 CREATE TRIGGER 문에 FOR DDL_TABLE_EVENTS를 지정하면 됩니다. CREATE TRIGGER가 실행되면 이벤트 그룹에 속하는 이벤트가 **sys.trigger_events** 카탈로그 뷰에 추가됩니다.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 트리거가 이벤트 그룹에 만들어지는 경우 **sys.trigger_events** 에는 이벤트 그룹에 대한 정보가 포함되지 않고 **sys.trigger_events** 에는 이벤트 그룹에 속한 개별 이벤트에 대한 정보만 포함됩니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서 **sys.trigger_events** 는 트리거가 만들어진 이벤트 그룹에 대한 메타데이터와 이벤트 그룹에 속한 개별 이벤트에 대한 메타데이터를 보존합니다. 따라서 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전의 이벤트 그룹에 속한 이벤트에 대한 변경 사항은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]의 이벤트 그룹에 만들어진 DDL 트리거에 적용되지 않습니다.  
  
 DDL 트리거에 사용할 수 있는 미리 정의된 DDL 문 그룹 목록, 이벤트 그룹에 포함된 특정 문 및 이러한 이벤트 그룹을 프로그래밍할 수 있는 범위는 [DDL Event Groups](../../relational-databases/triggers/ddl-event-groups.md)을 참조하십시오.  
  
## <a name="related-tasks"></a>관련 작업  
  
|Task|항목|  
|----------|-----------|  
|DDL 트리거 생성, 수정 또는 삭제하거나 사용하지 않도록 설정하는 방법에 대해 설명합니다.|[DDL 트리거 구현](../../relational-databases/triggers/implement-ddl-triggers.md)|  
|CLR DDL 트리거를 만드는 방법에 대해 설명합니다.|[CLR 트리거 만들기](../../relational-databases/triggers/create-clr-triggers.md)|  
|DDL 트리거에 대한 정보를 반환하는 방법에 대해 설명합니다.|[DDL 트리거에 대한 정보 가져오기](../../relational-databases/triggers/get-information-about-ddl-triggers.md)|  
|EVENTDATA 함수를 사용하여 DDL 트리거를 발생하는 이벤트에 대한 정보를 반환하는 방법에 대해 설명합니다.|[EVENTDATA 함수 사용](../../relational-databases/triggers/use-the-eventdata-function.md)|  
|트리거 보안을 관리하는 방법에 대해 설명합니다.|[트리거 보안 관리](../../relational-databases/triggers/manage-trigger-security.md)|  
  
## <a name="see-also"></a>참고 항목  
 [DML 트리거](../../relational-databases/triggers/dml-triggers.md)   
 [LOGON 트리거](../../relational-databases/triggers/logon-triggers.md)   
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
  
