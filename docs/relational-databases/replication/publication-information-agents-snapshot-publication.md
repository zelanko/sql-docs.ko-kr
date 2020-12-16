---
title: 에이전트(스냅샷 - SSMS)
description: SSMS(SQL Server Management Studio)의 스냅샷 에이전트 페이지에 있는 '에이전트' 탭을 설명합니다.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.downlevelagents.snapshot.f1
ms.assetid: 599ff80b-392c-43aa-9db2-dc4ed33d4f6e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 74d09865e026e813d28f97c9e07f9fd27a16204d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97439854"
---
# <a name="publication-information-agents-snapshot-publication"></a>게시 정보, 에이전트(스냅샷 게시)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  **에이전트** 탭은 선택한 게시에 대한 스냅샷 에이전트의 요약 정보를 표시합니다.  
  
## <a name="options"></a>옵션  
 자세한 내용 및 스냅샷 에이전트와 관련된 태스크를 보려면 해당 에이전트에 대한 행을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 옵션을 클릭합니다. 표에서 데이터를 표시하는 방식을 변경하려면 표를 마우스 오른쪽 단추로 클릭한 후 다음 옵션 중 하나를 클릭합니다.  
  
-   **정렬**: **열 정렬** 대화 상자에서 한 개 이상의 열에 대해 정렬합니다.  
  
-   **표시할 열 선택**: **열 선택** 대화 상자에서 표시할 열 및 해당 열이 표시되는 순서를 선택합니다.  
  
-   **필터**: **필터 설정** 대화 상자의 열 값에 따라 표의 행을 필터링합니다.  
  
-   **필터 지우기**: 표에 대한 모든 필터 설정을 지웁니다.  
  
 필터 설정은 각 표에 대해 지정됩니다. 열 선택 및 정렬은 각 게시자에 대한 게시 표와 같이 동일한 유형의 모든 표에 적용됩니다.  
  
 **상태**  
 스냅샷 에이전트의 상태입니다. 다음 목록에서는 가능한 상태 값을 보여 줍니다.  
  
-   Error  
  
-   실패한 명령 다시 시도 중  
  
-   실행 중이 아님  
  
-   Completed  
  
 **에이전트**  
 스냅샷 에이전트 이 에이전트는 스냅샷 게시와 연결된 유일한 에이전트입니다. 배포 에이전트는 이 게시에 대한 구독과 연결됩니다. 자세한 내용은 [복제 모니터를 사용하여 정보 보기 및 태스크 수행](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)을 참조하세요.  
  
 **마지막 시작 시간**  
 마지막으로 에이전트가 시작된 시간입니다.  
  
 **Duration**  
 에이전트가 실행된 시간입니다. 에이전트가 현재 실행되고 있는 경우 이 시간은 경과된 시간을 나타내고 에이전트가 이전에 실행된 경우에는 총 시간을 나타냅니다.  
  
 **마지막 동작**  
 가장 최근의 에이전트 실행에서 수행된 마지막 동작입니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [복제 모니터를 사용하여 정보 보기 및 태스크 수행](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [복제 모니터링](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
