---
title: 파일에 추적 결과 저장 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 74f80667-62f3-4e14-bb1a-f0c2b6ef3402
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 46963a4c25acd99fba902d84bd5102f8563dd968
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48213773"
---
# <a name="save-trace-results-to-a-file"></a>파일에 추적 결과 저장
  추적 결과를 파일에 저장할 수 있습니다. 추적 파일은 추적 결과가 기록된 파일입니다. 추적 파일은 로컬 디렉터리(예: C:\\*foldername*\\*filename.trc*) 또는 네트워크 디렉터리(예: \\\computername\sharename\filename.trc)에서 찾을 수 있습니다.  
  
 추적 파일을 사용하여 다음 작업을 할 수 있습니다.  
  
-   추적 재생  
  
-   감사 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   성능 분석 관리  
  
-   추적 이벤트와 성능 카운터의 상관 관계 지정으로 문제 감지 기능 향상  
  
-   데이터베이스 엔진 튜닝 관리자 분석 수행  
  
-   쿼리 최적화 수행  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 **@tracefile** 저장 프로시저의 **@tracefile**인수에 경로 및 파일 이름이 지정되면 추적 결과를 이 파일에 저장합니다.  
  
> [!NOTE]  
>  추적 파일을 저장하기 위한 경로가 **sp_trace_create** 저장 프로시저에 지정되는 경우 서버에서 해당 디렉터리에 액세스할 수 있어야 합니다. 또한 로컬 디렉터리가 **sp_trace_create**에 지정되는 경우 이는 서버 컴퓨터의 로컬 디렉터리라는 점을 유의하세요.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하면 추적 결과를 파일 또는 테이블에 저장할 수 있습니다. 추적 결과를 테이블에 저장하면 파일에 저장할 때와 똑같이 액세스할 수 있을 뿐 아니라 테이블을 쿼리하여 특정 이벤트를 검색할 수 있습니다.  
  
 추적 결과를 저장하는 방법은 [테이블에 추적 결과 저장&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md) 및 [파일에 추적 결과 저장&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [sp_trace_create&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)   
 [추적 만들기&#40;Transact-SQL&#41;](../sql-trace/create-a-trace-transact-sql.md)   
 [추적 만들기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
  
