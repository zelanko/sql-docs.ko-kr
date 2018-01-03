---
title: "추적 (SQL Server Profiler)에서 스크립트 추출 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- scripts [SQL Server], traces
- extracting script from trace [SQL Server]
ms.assetid: 431126a6-ff91-4818-8763-4442152bd571
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4398f742c1805a264b1d76f79f8b771aa6d940ee
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="extract-a-script-from-a-trace-sql-server-profiler"></a>추적에서 스크립트 추출(SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]이 항목에서는 추출 하는 방법을 설명 [!INCLUDE[tsql](../../includes/tsql-md.md)] 이벤트를 추적 파일 또는 테이블을 저장 한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 를 사용 하 여 스크립트 파일 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]합니다.  
  
### <a name="to-extract-a-transact-sql-script-from-a-trace-file-or-table"></a>추적 파일이나 테이블에서 Transact-SQL 스크립트를 추출하려면  
  
1.  [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 파일로 저장할 [!INCLUDE[tsql](../../includes/tsql-md.md)] 이벤트를 포함하는 추적 파일이나 테이블을 엽니다. 자세한 내용은 [추적 파일 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) 또는 [추적 테이블 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)에서 제공되는 사전 정의된 튜닝 템플릿을 사용합니다.  
  
2.  **파일** 메뉴에서 **내보내기**, **SQL Server 이벤트 추출**을 차례로 가리킨 다음 **Transact-SQL 이벤트 추출**을 클릭합니다.  
  
3.  **다른 이름으로 저장** 대화 상자에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 파일의 이름을 입력한 다음 **저장**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 프로파일러](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
