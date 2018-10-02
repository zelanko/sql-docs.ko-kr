---
title: 확장 이벤트 도구 | Microsoft 문서
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], using
- extended events [SQL Server], options for using
ms.assetid: d312a9ff-50ba-4721-baef-50bfd3169d38
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 46a154647b09f0a785773ff1fc85ba13aea12e09
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792931"
---
# <a name="extended-events-tools"></a>확장 이벤트 도구
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  다음 도구를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 확장 이벤트 세션을 만들고 관리할 수 있습니다.  
  
-   DDL(데이터 정의 언어) 문: 확장 이벤트 세션을 만들고 수정할 수 있습니다.  
  
-   동적 관리 뷰, 카탈로그 뷰 및 시스템 테이블: [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 세션 데이터 및 메타데이터를 가져올 수 있습니다. 시스템 테이블은 SQL 추적 이벤트 클래스 및 열에 해당하는 기존 확장 이벤트 항목을 확인하는 데 유용합니다.  
  
-   개체 탐색기의 **확장 이벤트** 노드: 세션을 시작, 중지 또는 삭제하거나 세션 템플릿을 가져오고 내보낼 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 공급자: 확장 이벤트 세션을 생성, 변경 및 관리하는 데 사용할 수 있는 강력한 도구입니다. 자세한 내용은 [확장 이벤트에 PowerShell 공급자 사용](../../relational-databases/extended-events/use-the-powershell-provider-for-extended-events.md)을 참조하세요.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]을 참조하세요. 확장 이벤트 항목에 제공된 코드 예제를 만들고 실행할 수 있습니다. 자세한 내용은 [개체 탐색기](../../ssms/object/object-explorer.md)를 참조하세요.  
  
 서버에는 사용자가 만드는 세션 외에도 기본 시스템 상태 세션이 있습니다. 이 세션은 성능 문제를 해결하는 데 사용할 수 있는 시스템 데이터를 수집합니다. 자세한 내용은 [system_health 세션 사용](../../relational-databases/extended-events/use-the-system-health-session.md)을 참조하세요.  
  
## <a name="ddl-statements"></a>DDL 문  
 다음 DDL 문을 사용하여 확장 이벤트 세션을 생성, 변경 및 삭제할 수 있습니다.  
  
|속성|설명|  
|----------|-----------------|  
|[CREATE EVENT SESSION&#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)|이벤트 원본, 이벤트 세션 대상 및 이벤트 세션 매개 변수를 식별하는 확장 이벤트 세션 개체를 만듭니다.|  
|[ALTER EVENT SESSION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)|이벤트 세션을 시작 또는 중지하거나 이벤트 세션 구성을 변경합니다.|  
|[DROP EVENT SESSION&#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)|이벤트 세션을 삭제합니다.|  
  
## <a name="catalog-views"></a>카탈로그 뷰  
 다음 카탈로그 뷰를 사용하여 이벤트 세션을 만들 때 함께 생성된 메타데이터를 가져올 수 있습니다.  
  
|속성|설명|  
|----------|-----------------|  
|[sys.server_event_sessions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)|이벤트 세션 정의를 모두 나열합니다.|  
|[sys.server_event_session_actions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-actions-transact-sql.md)|이벤트 세션의 각 이벤트의 동작에 대해 한 행을 반환합니다.|  
|[sys.server_event_session_events&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-events-transact-sql.md)|이벤트 세션의 각 이벤트에 대해 한 행을 반환합니다.|  
|[sys.server_event_session_fields&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-fields-transact-sql.md)|이벤트 및 대상에 명시적으로 설정된 각 사용자 지정 가능 열에 대해 한 행을 반환합니다.|  
|[sys.server_event_session_targets&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-targets-transact-sql.md)|이벤트 세션의 각 이벤트 대상에 대해 한 행을 반환합니다.|  
  
## <a name="dynamic-management-views"></a>동적 관리 뷰  
 다음 동적 관리 뷰를 사용하여 세션 메타데이터 및 세션 데이터를 가져올 수 있습니다. 메타데이터는 카탈로그 뷰를 통해 얻을 수 있습니다. 세션 데이터는 이벤트 세션을 시작하고 실행할 때 생성됩니다.  
  
> [!NOTE]  
>  세션이 시작되기 전에는 이러한 뷰에 세션 데이터가 포함되지 않습니다.  
  
|속성|설명|  
|----------|-----------------|  
|[sys.dm_os_dispatcher_pools&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-dispatcher-pools-transact-sql.md)|세션 발송자 풀에 대한 정보를 반환합니다.|  
|[sys.dm_xe_objects&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql.md)|이벤트 패키지에 의해 표시되는 각 개체에 대해 한 행을 반환합니다.|  
|[sys.dm_xe_object_columns&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql.md)|모든 개체에 대한 스키마 정보를 반환합니다.|  
|[sys.dm_xe_packages&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql.md)|확장 이벤트 엔진에 등록된 패키지를 모두 나열합니다.|  
|[sys.dm_xe_sessions&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql.md)|활성 확장 이벤트 세션에 대한 정보를 반환합니다.|  
|[sys.dm_xe_session_targets&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql.md)|세션 대상에 대한 정보를 반환합니다.|  
|[sys.dm_xe_session_events&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-events-transact-sql.md)|세션 이벤트에 대한 정보를 반환합니다.|  
|[sys.dm_xe_session_event_actions&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-event-actions-transact-sql.md)|이벤트 세션 동작에 대한 정보를 반환합니다.|  
|[sys.dm_xe_map_values&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-map-values-transact-sql.md)|내부 숫자 키를 사람이 이해할 수 있는 텍스트 형식으로 매핑합니다.|  
|[sys.dm_xe_session_object_columns&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-object-columns-transact-sql.md)|세션에 바인딩된 개체의 구성 값을 표시합니다.|  
  
## <a name="system-tables"></a>시스템 테이블  
 다음 시스템 테이블을 사용하여 SQL 추적 이벤트 클래스 및 열에 해당하는 확장 이벤트 항목에 대한 정보를 가져올 수 있습니다.  
  
|속성|설명|  
|----------|-----------------|  
|[trace_xe_event_map&#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-event-map.md)|SQL 추적 이벤트 클래스에 매핑된 Extended Events 이벤트마다 하나의 행을 포함합니다.|  
|[trace_xe_action_map&#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-action-map.md)|SQL 추적 열 ID에 매핑된 Extended Events 동작마다 하나의 행을 포함합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 확장 이벤트 테이블&#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/6d52ff03-f5aa-4f0f-8c98-9b49dc76f94e)   
 [system_health 세션 사용](../../relational-databases/extended-events/use-the-system-health-session.md)   
 [확장 이벤트에 PowerShell 공급자 사용](../../relational-databases/extended-events/use-the-powershell-provider-for-extended-events.md)  
  
  
