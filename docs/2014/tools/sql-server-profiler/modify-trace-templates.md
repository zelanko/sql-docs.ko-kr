---
title: 추적 템플릿 수정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- templates [SQL Server], SQL Server Profiler
- Profiler [SQL Server Profiler], templates
- trace templates [SQL Server]
- modifying trace templates
- SQL Server Profiler, templates
ms.assetid: 75b62a54-8d16-4599-bd2d-c42cfcc209f4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ebe8924f46de15a3a34c0f49304c87a904919bdb
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52757655"
---
# <a name="modify-trace-templates"></a>추적 템플릿 수정
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 가 실행 중인 로컬 컴퓨터에서 파일에 저장된 템플릿을 수정할 수 있습니다. 이런 파일에서 파생된 템플릿도 수정할 수 있습니다. 기존 템플릿을 수정할 때 **추적 속성** 대화 상자의 **이벤트 선택** 탭에서 속성이 원래 설정된 순서와 동일한 순서대로 이벤트 클래스나 데이터 열 같은 템플릿 속성을 편집합니다. 이벤트 클래스 및 데이터 열을 추가 또는 제거할 수도 있고 필터도 같은 방법으로 변경할 수 있습니다. 템플릿을 수정하면 사용자 특정 템플릿이 만들어지고 원래 시스템 템플릿은 그대로 남습니다. 자세한 내용은 [추적 및 추적 템플릿 저장](save-traces-and-trace-templates.md)을 참조하세요.  
  
 추적을 만들 때 사용한 원래 템플릿을 기억할 수 없거나 나중에 같은 추적을 실행하려는 경우 기존 추적 파일에서 템플릿을 파생해야 합니다. 기존의 추적으로 작업하면 속성을 볼 수는 있지만 수정할 수는 없습니다. 속성을 수정하려면 추적을 시작하거나 일시 중지하십시오. 자세한 내용은 [추적 파일 또는 추적 테이블에서 템플릿 파생&#40;SQL Server Profiler&#41;](sql-server-profiler.md) 및 [실행 중인 추적으로부터 템플릿 파생&#40;SQL Server Profiler&#41;](derive-a-template-from-a-running-trace-sql-server-profiler.md)을 참조하세요.  
  
 **추적 템플릿을 만들려면**  
  
 [추적 템플릿 만들기&#40;SQL Server Profiler&#41;](create-a-trace-template-sql-server-profiler.md)  
  
 **추적 템플릿에서 추적을 실행하려면**  
  
 [추적 만들기&#40;SQL Server Profiler&#41;](create-a-trace-sql-server-profiler.md)  
  
 **추적 템플릿을 수정하려면**  
  
 [SQL Server Profiler 사용](../../database-engine/modify-a-trace-template-sql-server-profiler.md)  
  
 [Transact-SQL 사용](../../relational-databases/sql-trace/modify-an-existing-trace-transact-sql.md)  
  
 **추적 템플릿 또는 추적 파일에서 이벤트를 추가하거나 제거하려면**  
  
 [SQL Server Profiler 사용](specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
 [Transact-SQL 사용](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
## <a name="see-also"></a>관련 항목  
 [추적 시작](start-a-trace.md)  
  
  
