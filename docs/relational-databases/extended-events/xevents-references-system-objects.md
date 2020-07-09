---
title: XEvent 관련 시스템 개체
description: 이 리소스는 시스템 개체에서 확장 이벤트를 지원하는 방법, SQL Server에서 확장 이벤트를 사용하는 방법, Azure SQL Database 관련 사항 등 확장 이벤트와 관련이 있습니다.
ms.date: 03/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: jukoesma
ms.technology: xevents
ms.topic: reference
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e61edcb1f8c1dd9844d887818d208cde1615d5ba
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756792"
---
# <a name="system-objects-that-support-extended-events"></a>확장 이벤트를 지원하는 시스템 개체

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

현재 문서에는 확장 이벤트와 관련된 다른 문서에 연결된 링크가 있습니다. 이러한 문서에서는 다음 내용에 관해 설명합니다.

- 확장 이벤트 기능을 지원하는 시스템 개체.
- 확장 이벤트를 사용하는 SQL Server 자체의 부분.
- 클라우드에서 Azure SQL Database에 특별히 해당하는 확장 이벤트의 측면.

이 목록 외의 내용도 있을 수 있습니다.

## <a name="system-tables"></a>시스템 테이블

- [확장 이벤트 테이블 - trace_xe_action_map](../system-tables/extended-events-tables-trace-xe-action-map.md)

- [확장 이벤트 테이블 - trace_xe_event_map](../system-tables/extended-events-tables-trace-xe-event-map.md)

## <a name="system-catalog-views"></a>시스템 카탈로그 뷰

- [확장 이벤트 카탈로그 뷰(Transact-SQL)](../system-catalog-views/extended-events-catalog-views-transact-sql.md)

- [sys.server_event_sessions(Transact-SQL)](../system-catalog-views/sys-server-event-sessions-transact-sql.md)

- [sys.server_event_session_actions(Transact-SQL)](../system-catalog-views/sys-server-event-session-actions-transact-sql.md)

- [sys.server_event_session_events(Transact-SQL)](../system-catalog-views/sys-server-event-session-events-transact-sql.md)

- [sys.server_event_session_fields(Transact-SQL)](../system-catalog-views/sys-server-event-session-fields-transact-sql.md)

- [sys.server_event_session_targets(Transact-SQL)](../system-catalog-views/sys-server-event-session-targets-transact-sql.md)

## <a name="other-system-objects"></a>기타 시스템 개체

- [확장 이벤트 동적 관리 뷰](../system-dynamic-management-views/extended-events-dynamic-management-views.md)

## <a name="uses-of-extended-events-by-sql-server-itself"></a>SQL Server 자체의 확장 이벤트 사용

이 목록 외의 내용도 있을 수 있습니다.

- [확장 이벤트 로그의 진단 정보 액세스](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)

- [Always On 가용성 그룹에 대한 확장 이벤트 구성](../../database-engine/availability-groups/windows/always-on-extended-events.md)

- [Stretch Database용 확장 이벤트](../../sql-server/stretch-database/extended-events-for-stretch-database.md)

## <a name="azure-sql-database-and-extended-events"></a>Azure SQL Database 및 확장 이벤트

- [Azure SQL Database의 확장 이벤트](/azure/sql-database/sql-database-xevent-db-diff-from-svr)

- [sys.database_event_session_targets(Azure SQL Database)](../system-catalog-views/sys-database-event-session-targets-azure-sql-database.md)

- [sys.database_event_session_fields(Azure SQL Database)](../system-catalog-views/sys-database-event-session-fields-azure-sql-database.md)

- [sys.database_event_session_events(Azure SQL Database)](../system-catalog-views/sys-database-event-session-events-azure-sql-database.md)

- [sys.database_event_session_actions(Azure SQL Database)](../system-catalog-views/sys-database-event-session-actions-azure-sql-database.md)
