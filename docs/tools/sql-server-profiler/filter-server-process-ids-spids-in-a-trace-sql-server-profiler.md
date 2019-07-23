---
title: 추적의 SPID(서버 프로세스 ID) 필터링(SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], traces
- filters [SQL Server], SPIDs
- traces [SQL Server], filters
ms.assetid: f5945c39-be6b-4632-91cb-92066c80e188
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 172ba4b6cb2ed5bee84d920f8b7e0c73de3b8e90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075010"
---
# <a name="filter-server-process-ids-spids-in-a-trace-sql-server-profiler"></a>추적의 SPID(서버 프로세스 ID) 필터링(SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목은 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 추적에서 SPID(서버 프로세스 식별자)를 필터링하는 방법을 설명합니다.  
  
### <a name="to-filter-system-ids-in-a-trace"></a>추적에서 시스템 ID를 필터링하려면  
  
1.  **파일** 메뉴에서 **새 추적**을 클릭한 다음 SQL Server 인스턴스에 연결합니다.  
  
     **추적 속성** 대화 상자가 나타납니다.  
  
    > [!NOTE]  
    >  **연결한 후 즉시 추적 시작**을 선택한 경우에는 **추적 속성** 대화 상자가 나타나지 않고 추적이 시작됩니다. 이 설정을 해제하려면 **도구**메뉴에서 **옵션**을 클릭한 다음, **연결한 후 즉시 추적 시작** 확인란의 선택을 취소합니다.  
  
2.  **추적 이름** 입력란에 추적의 이름을 입력합니다.  
  
3.  **템플릿 사용** 이름 목록에서 추적 템플릿을 선택합니다.  
  
4.  필요에 따라 추적 결과를 저장할 대상 파일이나 테이블을 지정합니다.  
  
5.  **이벤트 선택**탭에서 **SPID** 열 머리글을 클릭하여 **필터 편집** 대화 상자를 엽니다. 또는 열 머리글을 마우스 오른쪽 단추로 클릭하고 **열 필터 편집**을 클릭할 수도 있습니다. **SPID** 열이 표시되지 않는 경우에는 **모든 열 표시** 확인란을 선택합니다.  
  
6.  **필터 편집** 대화 상자에서 적절한 비교 연산자를 확장한 다음 비교할 값으로 SPID를 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 프로파일러](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
