---
title: 서버 이벤트용 WMI 공급자에 WQL 사용
description: 관리 응용 프로그램이 WQL(WMI Query Language) 문을 실행 하 여 서버 이벤트 용 WMI 공급자를 사용 하 여 SQL Server 이벤트에 액세스 하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- queries [WMI]
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Server Events, WQL
ms.assetid: 58b67426-1e66-4445-8e2c-03182e94c4be
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e6fae362d3a8d1fe387dd7561b1476bb37f0c255
ms.sourcegitcommit: bf5e9cb3a2caa25d0a37f401b3806b7baa5adea8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85295386"
---
# <a name="using-wql-with-the-wmi-provider-for-server-events"></a>서버 이벤트용 WMI 공급자에 WQL 사용
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  관리 애플리케이션은 서버 이벤트용 WMI 공급자를 통해 WQL(WMI Query Language) 문을 실행하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트에 액세스합니다. WQL은 몇 가지 WMI 관련 확장 기능이 포함된 SQL(구조적 쿼리 언어)의 단순화된 일부입니다. WQL을 사용할 경우 애플리케이션은 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스, 데이터베이스 또는 데이터베이스 개체(현재 지원되는 유일한 개체는 큐임)에 대해 이벤트 유형을 검색합니다. 서버 이벤트 용 WMI 공급자는 데이터베이스 범위 또는 개체 범위 이벤트 알림의 경우 대상 데이터베이스에 생성 되는 이벤트 알림이나 서버 범위 이벤트 알림의 경우 **master** 데이터베이스에 생성 되는 이벤트 알림으로 쿼리를 변환 합니다.  
  
 예를 들어 다음 WQL 쿼리를 살펴보십시오.  
  
```  
SELECT * FROM DDL_DATABASE_LEVEL_EVENTS WHERE DatabaseName = 'AdventureWorks'  
```  
  
 이 쿼리에서 WMI 공급자는 대상 서버에서 이벤트 알림과 동등한 항목을 생성합니다.  
  
```  
USE AdventureWorks ;  
GO  
  
CREATE EVENT NOTIFICATION SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9  
    ON DATABASE  
    WITH FAN_IN  
    FOR DDL_DATABASE_LEVEL_EVENTS  
    TO SERVICE   
        'SQL/Notifications/ProcessWMIEventProviderNotification/v1.0',  
        'A7E5521A-1CA6-4741-865D-826F804E5135';  
GO  
```  
  
 WQL 쿼리(`FROM`)의 `DDL_DATABASE_LEVEL_EVENTS` 절에 있는 인수는 이벤트 알림을 만들 수 있는 유효한 모든 이벤트일 수 있습니다. `SELECT` 및 `WHERE` 절의 인수는 이벤트 또는 해당 부모 이벤트와 연결된 이벤트 속성을 지정할 수 있습니다. 유효한 이벤트 및 이벤트 속성 목록은 [이벤트 알림 (데이터베이스 엔진)](https://technet.microsoft.com/library/ms182602.aspx)을 참조 하세요.  
  
 서버 이벤트용 WMI 공급자가 명시적으로 지원하는 WQL 구문은 다음과 같습니다. 추가 WQL 구문을 지정할 수도 있지만 해당 구문은 이 공급자와 관련이 없으며 대신 WMI 호스트 서비스에 의해 구문 분석됩니다. WMI 쿼리 언어에 대한 자세한 내용은 MSDN(Microsoft Developer Network)의 WQL 설명서를 참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```  
  
SELECT { event_property [ ,...n ] | * }  
FROM event_type   
WHERE where_condition   
```  
  
## <a name="arguments"></a>인수  
 *event_property*  
 이벤트의 속성입니다. 예를 들어 **Posttime**, **SPID**및 **LoginName**이 있습니다. [서버 이벤트 용 WMI 공급자 클래스 및 속성](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md) 에 나열 된 각 이벤트를 조회 하 여 보유 한 속성을 확인 합니다. 예를 들어 DDL_DATABASE_LEVEL_EVENTS 이벤트는 **DatabaseName** 및 **UserName** 속성을 보유 합니다. 또한 부모 이벤트에서 **SQLInstance**, **LoginName**, **Posttime**, **SPID**및 **ComputerName** 속성을 상속 합니다.  
  
 **,** *... n*  
 *Event_property* 를 쉼표로 구분 하 여 여러 번 쿼리할 수 있음을 나타냅니다.  
  
 \*  
 이벤트와 관련된 모든 속성이 쿼리되도록 지정합니다.  
  
 *event_type*  
 이벤트 알림을 만들 수 있는 모든 이벤트입니다. 사용 가능한 이벤트 목록은 [서버 이벤트 용 WMI 공급자 클래스 및 속성](https://technet.microsoft.com/library/ms186449.aspx)을 참조 하세요. 이벤트 *유형* 이름은 *event_type*  |  create event notification을 사용 하 여 수동으로 이벤트 알림을 만들 때 지정할 수 있는 동일한 event_type*event_group* 에 해당 합니다. *이벤트 유형의* 예로는 CREATE_TABLE, LOCK_DEADLOCK, DDL_USER_EVENTS 및 TRC_DATABASE가 있습니다.  
  
> [!NOTE]  
>  DDL과 같은 작업을 수행하는 특정 시스템 저장 프로시저에서 이벤트 알림이 발생할 수도 있습니다. 이벤트 알림을 테스트하여 실행된 시스템 저장 프로시저에 대한 응답을 확인합니다. 예를 들어 CREATE TYPE 문과 **sp_addtype** 저장 프로시저는 모두 CREATE_TYPE 이벤트에 대해 생성 되는 이벤트 알림을 발생 시킵니다. 그러나 **sp_rename** 저장 프로시저는 이벤트 알림을 발생 시 지 않습니다. 자세한 내용은[DDL Events](../../relational-databases/triggers/ddl-events.md)를 참조 하십시오.  
  
 *where_condition*  
 *Event_property* 이름 및 논리 and 비교 연산자로 구성 된 where 절 쿼리 조건자입니다. *Where_condition* 는 대상 데이터베이스에 해당 이벤트 알림이 등록 되는 범위를 결정 합니다. 또한 event_type 쿼리할 특정 스키마 또는 개체를 대상으로 하는 필터 역할을 할 수 있습니다 *.* 자세한 내용은 이 항목의 뒷부분에 나오는 주의 섹션을 참조하십시오.  
  
 피연산자만 `=` **DatabaseName**, **SchemaName**및 **ObjectName**과 함께 사용할 수 있습니다. 다른 식은 이러한 이벤트 속성과 함께 사용할 수 없습니다.  
  
## <a name="remarks"></a>설명  
 서버 이벤트 용 WMI 공급자 구문의 *where_condition* 은 다음을 결정 합니다.  
  
-   공급자가 지정 된 *event_type*를 검색 하려고 하는 범위입니다. 서버 수준, 데이터베이스 수준 또는 개체 수준 (현재 지원 되는 유일한 개체는 큐)입니다. 궁극적으로 이 범위는 대상 데이터베이스에 생성되는 이벤트 알림 유형을 결정합니다. 이 프로세스를 이벤트 알림 등록이라고 합니다.  
  
-   필요한 경우 등록이 수행되는 데이터베이스, 스키마 및 개체입니다.  
  
 서버 이벤트용 WMI 공급자는 아래에서 위로, 첫 번째 일치 알고리즘을 사용하여 기본 EVENT NOTIFICATION에 대한 가능한 가장 좁은 범위를 생성합니다. 이 알고리즘은 서버의 내부 활동과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 WMI 호스트 프로세스 인스턴스 간의 네트워크 트래픽을 최소화합니다. 공급자는 FROM 절에 지정 된 *event_type* 와 where 절의 조건을 검사 하 고 가능한 가장 좁은 범위를 사용 하 여 기본 이벤트 알림을 등록 하려고 합니다. 공급자는 가장 좁은 범위를 등록할 수 없는 경우 등록에 성공할 때까지 연속적으로 더 높은 범위에 등록을 시도합니다. 가장 높은 범위인 서버 수준에 도달했지만 실패하는 경우 소비자에게 오류를 반환합니다.  
  
 예를 들어 WHERE 절에 DatabaseName =**'** AdventureWorks **'** 를 지정 하면 공급자는 데이터베이스에 이벤트 알림을 등록 하려고 합니다 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스가 있고 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]에 이벤트 알림을 만드는 데 필요한 권한이 호출 클라이언트에 있으면 등록이 성공합니다. 그렇지 않으면 서버 수준에서 이벤트 알림이 등록됩니다. WMI 클라이언트에 필요한 사용 권한이 있으면 등록이 성공합니다. 하지만 이 시나리오에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 만들 때까지 이벤트가 클라이언트에 반환되지 않습니다.  
  
 또한 *where_condition* 는 필터 역할을 하 여 쿼리를 특정 데이터베이스, 스키마 또는 개체로 추가로 제한할 수 있습니다. 예를 들어 다음 WQL 쿼리를 살펴보십시오.  
  
```  
SELECT * FROM ALTER_TABLE   
WHERE DatabaseName = 'AdventureWorks' AND SchemaName = 'Sales'   
    AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'  
```  
  
 등록 프로세스의 결과에 따라 이 WOL 쿼리를 데이터베이스 또는 서버 수준에서 등록할 수 있습니다. 하지만 서버 수준에서 등록된 경우에도 공급자는 궁극적으로 `ALTER_TABLE` 테이블에 적용되지 않는 모든 `AdventureWorks.Sales.SalesOrderDetail` 이벤트를 필터링합니다. 즉, 공급자는 특정 테이블에서 발생하는 `ALTER_TABLE` 이벤트의 속성만 반환합니다.  
  
 `DatabaseName='AW1'` OR `DatabaseName='AW2'`와 같은 복합 식을 지정하면 두 개의 개별 이벤트 알림 대신 서버 범위에서 단일 이벤트 알림이 등록됩니다. 호출 클라이언트에 사용 권한이 있으면 등록이 성공합니다.  
  
 `SchemaName='X' AND ObjectType='Y' AND ObjectName='Z'`절에이 모두 지정 된 경우 `WHERE` 스키마의 개체에 직접 이벤트 알림을 등록 하려고 시도 합니다 `Z` `X` . 클라이언트에 사용 권한이 있으면 등록이 성공합니다. 현재 개체 수준 이벤트는 큐 에서만 지원 되 고 QUEUE_ACTIVATION *event_type*에 대해서만 지원 됩니다.  
  
 임의의 특정 범위에서 모든 이벤트를 쿼리할 수는 없습니다. 예를 들어 Lock_Deadlock과 같은 추적 이벤트나 TRC_LOCKS와 같은 추적 이벤트 그룹의 WQL 쿼리는 서버 수준에서만 등록할 수 있습니다. 이와 유사하게, CREATE_ENDPOINT 이벤트 및 DDL_ENDPOINT_EVENTS 이벤트 그룹도 서버 수준에서만 등록할 수 있습니다. 이벤트 등록에 적합 한 범위에 대 한 자세한 내용은 [이벤트 알림 디자인](https://technet.microsoft.com/library/ms175854\(v=sql.105\).aspx)을 참조 하세요. 서버 수준 에서만 *event_type* 등록 될 수 있는 WQL 쿼리를 등록 하려는 시도는 항상 서버 수준에서 수행 됩니다. WMI 클라이언트에 사용 권한이 있으면 등록이 성공합니다. 그렇지 않으면 오류가 클라이언트에 반환됩니다. 하지만 경우에 따라 이벤트에 해당하는 속성을 기반으로 WHERE 절을 서버 수준 이벤트의 필터로 사용할 수 있습니다. 예를 들어 많은 추적 이벤트에는 WHERE 절에서 필터로 사용할 수 있는 **DatabaseName** 속성이 있습니다.  
  
 서버 범위 이벤트 알림은 **master** 데이터베이스에 생성 되며, [server_event_notifications](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md) 카탈로그 뷰를 사용 하 여 메타 데이터에 대해 쿼리할 수 있습니다.  
  
 데이터베이스 범위 또는 개체 범위 이벤트 알림은 지정 된 데이터베이스에 생성 되며, [event_notifications](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md) 카탈로그 뷰를 사용 하 여 메타 데이터에 대해 쿼리할 수 있습니다. 카탈로그 뷰에 해당 데이터베이스 이름을 접두사로 추가해야 합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-querying-for-events-at-the-server-scope"></a>A. 서버 범위에서 이벤트 쿼리  
 다음 WQL 쿼리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 발생하는 `SERVER_MEMORY_CHANGE` 추적 이벤트의 모든 이벤트 속성을 검색합니다.  
  
```  
SELECT * FROM SERVER_MEMORY_CHANGE  
```  
  
### <a name="b-querying-for-events-at-the-database-scope"></a>B. 데이터베이스 범위에서 이벤트 쿼리  
 다음 WQL 쿼리는 `AdventureWorks` 데이터베이스에서 발생하고 `DDL_DATABASE_LEVEL_EVENTS` 이벤트 그룹에 속한 이벤트의 특정 이벤트 속성을 검색합니다.  
  
```  
SELECT SPID, SQLInstance, DatabaseName FROM DDL_DATABASE_LEVEL_EVENTS   
WHERE DatabaseName = 'AdventureWorks'   
```  
  
### <a name="c-querying-for-events-at-the-database-scope-filtering-by-schema-and-object"></a>C. 스키마 및 개체로 필터링하여 데이터베이스 범위에서 이벤트 쿼리  
 다음 쿼리는 `ALTER_TABLE` 테이블에서 발생하는 `AdventureWorks.Sales.SalesOrderDetail` 이벤트의 모든 이벤트 속성을 검색합니다.  
  
```  
SELECT * FROM ALTER_TABLE   
WHERE DatabaseName = 'AdventureWorks' AND SchemaName = 'Sales'   
    AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'  
```  
  
## <a name="see-also"></a>참고 항목  
 [서버 이벤트 용 WMI 공급자 개념](https://technet.microsoft.com/library/ms180560.aspx)   
 [이벤트 알림(데이터베이스 엔진)](https://technet.microsoft.com/library/ms182602.aspx)  
  
  
