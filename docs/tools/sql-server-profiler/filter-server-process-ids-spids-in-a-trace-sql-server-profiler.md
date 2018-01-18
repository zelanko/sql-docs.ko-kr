---
title: "추적 (SQL Server Profiler)에 서버 프로세스 Id (Spid)를 필터링 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filters [SQL Server], traces
- filters [SQL Server], SPIDs
- traces [SQL Server], filters
ms.assetid: f5945c39-be6b-4632-91cb-92066c80e188
caps.latest.revision: "25"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 67926fa0506f797c4f39988061c4d1b7b731e5fa
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="filter-server-process-ids-spids-in-a-trace-sql-server-profiler"></a>추적의 SPID(서버 프로세스 ID) 필터링(SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]이 항목에서는 추적에서 서버 프로세스 id (Spid)를 사용 하 여 필터링 하는 방법을 설명 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]합니다.  
  
### <a name="to-filter-system-ids-in-a-trace"></a>추적에서 시스템 ID를 필터링하려면  
  
1.  **파일** 메뉴에서 **새 추적**을 클릭한 다음 SQL Server 인스턴스에 연결합니다.  
  
     **추적 속성** 대화 상자가 표시됩니다.  
  
    > [!NOTE]  
    >  경우 **연결한 후 즉시 추적 시작** 확인란이 **추적 속성** 대화 상자가 나타나지 않으며 대신 추적이 시작 됩니다. 에이 설정을 해제 하려면는 **도구** 메뉴를 클릭 하 여 **옵션**, 선택을 취소 하 고는 **연결한 후 즉시 추적 시작** 확인란 합니다.  
  
2.  **추적 이름** 입력란에 추적의 이름을 입력합니다.  
  
3.  에 **서식 파일을 사용 하 여** 이름 목록에서 추적 템플릿을 선택 합니다.  
  
4.  필요에 따라 추적 결과를 저장할 대상 파일이나 테이블을 지정합니다.  
  
5.  에 **이벤트 선택** 탭을 클릭는 **SPID** 열 머리글을는 **필터 편집** 대화 상자. 또는 열 머리글을 마우스 오른쪽 단추로 클릭하고 **열 필터 편집**을 클릭할 수도 있습니다. **SPID** 열이 표시되지 않는 경우에는 **모든 열 표시** 확인란을 선택합니다.  
  
6.  **필터 편집** 대화 상자에서 적절한 비교 연산자를 확장한 다음 비교할 값으로 SPID를 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 프로파일러](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
