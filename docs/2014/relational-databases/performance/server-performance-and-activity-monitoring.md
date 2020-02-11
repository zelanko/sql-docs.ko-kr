---
title: 서버 성능 및 작업 모니터링 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- activity monitoring [SQL Server]
- traces [SQL Server], how-to topics
- monitoring server performance [SQL Server], activity monitoring
- stored procedures [SQL Server], traces
- performance [SQL Server], servers
- servers [SQL Server], performance
- SQL Server Profiler, how-to topics
- SQL Server Management Studio [SQL Server], monitoring system
- Profiler [SQL Server Profiler], how-to topics
ms.assetid: f9abe48d-d6e9-4c38-a355-fc5eb5a95a25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7289c18fac421bbdb5ccc0e00a3bea60b7a22d9e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63150611"
---
# <a name="server-performance-and-activity-monitoring"></a>서버 성능 및 작업 모니터링
  데이터베이스 모니터링의 목표는 서버의 성능을 평가하는 것입니다. 효과적인 모니터링을 위해서는 현재 성능에 대한 스냅샷을 정기적으로 만들어 문제를 일으키는 프로세스를 격리하고 데이터를 지속적으로 수집하여 성능 경향을 추적해야 합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)] 운영 체제에서는 데이터베이스의 현재 상태를 보고 상태 변화에 따라 성능을 추적할 수 있는 유틸리티를 제공 합니다.  
  
 다음 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 Windows의 성능 및 작업 모니터링 도구 사용 방법을 설명합니다. 다음 항목이 포함됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 **Windows 도구를 사용 하 여 모니터링 작업을 수행 하려면**  
  
-   [Windows&#41;&#40;시스템 모니터를 시작 합니다.](start-system-monitor-windows.md)  
  
-   [Windows 애플리케이션 로그 보기&#40;Windows&#41;](view-the-windows-application-log-windows-10.md)  
  
 **Windows 도구를 사용 하 여 SQL Server 데이터베이스 경고를 만들려면**  
  
-   [Windows&#41;&#40;SQL Server 데이터베이스 경고 설정](set-up-a-sql-server-database-alert-windows.md)  
  
 **SQL Server Management Studio를 사용 하 여 모니터링 작업을 수행 하려면**  
  
-   [SQL Server 오류 로그 &#40;SQL Server Management Studio 확인&#41;](../../ssms/sql-server-management-studio-ssms.md)  
  
-   [작업 모니터 열기&#40;SQL Server Management Studio&#41;](../performance-monitor/open-activity-monitor-sql-server-management-studio.md)  
  
 **Transact-sql 저장 프로시저를 사용 하 여 SQL 추적으로 모니터링 태스크를 수행 하려면**  
  
-   [추적 만들기&#40;Transact-SQL&#41;](../sql-trace/create-a-trace-transact-sql.md)  
  
-   [Transact-sql&#41;&#40;추적 필터 설정](../../ssms/agent/set-sql-server-alias-for-sql-server-agent-service-ssms.md)  
  
-   [Transact-sql&#41;&#40;기존 추적 수정](../sql-trace/modify-an-existing-trace-transact-sql.md)  
  
-   [Transact-sql&#41;&#40;저장 된 추적 보기](../sql-trace/view-a-saved-trace-transact-sql.md)  
  
-   [Transact-sql&#41;&#40;필터 정보 보기](../sql-trace/view-filter-information-transact-sql.md)  
  
-   [Transact-sql&#41;&#40;추적 삭제](../sql-trace/delete-a-trace-transact-sql.md)  
  
 **SQL Server Profiler를 사용 하 여 추적을 만들고 수정 하려면**  
  
-   [추적 만들기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
-   [전역 추적 옵션 설정 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-global-trace-options-sql-server-profiler.md)  
  
-   [추적 파일 &#40;SQL Server Profiler&#41;에 대 한 이벤트 및 데이터 열을 지정 합니다.](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
-   [추적 &#40;SQL Server Profiler를 실행 하는 Transact-sql 스크립트를 만듭니다&#41;](../../tools/sql-server-profiler/create-a-transact-sql-script-for-running-a-trace-sql-server-profiler.md)  
  
-   [SQL Server Profiler &#40;파일에 추적 결과 저장&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)  
  
-   [추적 파일에 최대 파일 크기 설정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-file-size-for-a-trace-file-sql-server-profiler.md)  
  
-   [추적 결과를 테이블 &#40;SQL Server Profiler에 저장&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)  
  
-   [추적 테이블에 최대 테이블 크기 설정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-table-size-for-a-trace-table-sql-server-profiler.md)  
  
-   [추적에서의 이벤트 필터링&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)  
  
-   [SQL Server Profiler&#41;&#40;필터 정보 보기](../../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)  
  
-   [필터 &#40;SQL Server Profiler를 수정&#41;](../../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)  
  
-   [이벤트 시작 시간을 기준으로 이벤트를 필터링 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-start-time-sql-server-profiler.md)  
  
-   [이벤트 종료 시간 기반의 이벤트 필터링&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
-   [추적 &#40;SQL Server Profiler&#41; Spid &#40;서버 프로세스 Id를 필터링&#41;](../../tools/sql-server-profiler/filter-server-process-ids-spids-in-a-trace-sql-server-profiler.md)  
  
-   [추적 &#40;SQL Server Profiler에 표시 되는 열 구성&#41;](../../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)  
  
 **SQL Server Profiler를 사용 하 여 추적을 시작, 일시 중지 및 중지 하려면**  
  
-   [서버 연결 후 자동으로 추적 시작&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)  
  
-   [추적 일시 중지&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/pause-a-trace-sql-server-profiler.md)  
  
-   [추적 중지&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/stop-a-trace-sql-server-profiler.md)  
  
-   [일시 중지 또는 중지 후 추적 실행&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
 **SQL Server Profiler를 사용 하 여 추적을 열고 추적을 표시 하는 방법을 구성 하려면**  
  
-   [추적 파일 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)  
  
-   [추적 테이블 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)  
  
-   [추적 창 지우기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/clear-a-trace-window-sql-server-profiler.md)  
  
-   [SQL Server Profiler &#40;추적 창을 닫습니다&#41;](../../tools/sql-server-profiler/close-a-trace-window-sql-server-profiler.md)  
  
-   [추적 정의 기본값 설정 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)  
  
-   [추적 표시 기본값 설정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
 **SQL Server Profiler를 사용 하 여 추적을 재생 하려면**  
  
-   [SQL Server Profiler &#40;추적 파일 재생&#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)  
  
-   [SQL Server Profiler &#40;추적 테이블 재생&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)  
  
-   [SQL Server Profiler &#40;한 번에 단일 이벤트 재생&#41;](../../tools/sql-server-profiler/replay-a-single-event-at-a-time-sql-server-profiler.md)  
  
-   [중단점까지 재생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-breakpoint-sql-server-profiler.md)  
  
-   [커서까지 재생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-cursor-sql-server-profiler.md)  
  
-   [Transact-sql 스크립트 &#40;SQL Server Profiler 재생&#41;](../../tools/sql-server-profiler/replay-a-transact-sql-script-sql-server-profiler.md)  
  
 **SQL Server Profiler를 사용 하 여 추적 템플릿을 만들고 수정 하 고 사용 하려면**  
  
-   [추적 템플릿 만들기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)  
  
-   [추적 템플릿 수정&#40;SQL Server Profiler&#41;](../../database-engine/modify-a-trace-template-sql-server-profiler.md)  
  
-   [실행 중인 추적으로부터 템플릿 파생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)  
  
-   [추적 파일 또는 추적 테이블에서 템플릿 파생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)  
  
-   [추적 템플릿 내보내기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/export-a-trace-template-sql-server-profiler.md)  
  
-   [SQL Server Profiler&#41;&#40;추적 템플릿을 가져옵니다.](../../tools/sql-server-profiler/import-a-trace-template-sql-server-profiler.md)  
  
 **SQL Server Profiler 추적을 사용 하 여 서버 성능을 수집 하 고 모니터링 하려면**  
  
-   [&#40;SQL Server Profiler 추적 하는 동안 값 또는 데이터 열을 찾습니다&#41;](../../tools/sql-server-profiler/find-a-value-or-data-column-while-tracing-sql-server-profiler.md)  
  
-   [SQL Server Profiler &#40;교착 상태 그래프를 저장&#41;](save-deadlock-graphs-sql-server-profiler.md)  
  
-   [실행 계획 XML 이벤트를 SQL Server Profiler &#40;별도로 저장&#41;](save-showplan-xml-events-separately-sql-server-profiler.md)  
  
-   [실행 계획 XML 통계 프로필 이벤트를 SQL Server Profiler &#40;별도로 저장&#41;](save-showplan-xml-statistics-profile-events-separately-sql-server-profiler.md)  
  
-   [추적 &#40;SQL Server Profiler에서 스크립트를 추출&#41;](../../tools/sql-server-profiler/extract-a-script-from-a-trace-sql-server-profiler.md)  
  
-   [추적과 Windows 성능 로그 데이터의 상관 관계를 &#40;SQL Server Profiler&#41;](../../database-engine/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  
