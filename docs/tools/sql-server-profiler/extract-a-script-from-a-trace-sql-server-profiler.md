---
title: 추적에서 스크립트 추출
titleSuffix: SQL Server Profiler
description: SQL Server Profiler에서 추적 파일 또는 테이블로부터 Transact-SQL 이벤트를 추출하여 Transact-SQL 스크립트 파일로 저장하는 방법을 알아봅니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 431126a6-ff91-4818-8763-4442152bd571
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 2495eb7c020e6fb64fb894d4d6bb7614707f84bc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774859"
---
# <a name="extract-a-script-from-a-trace-sql-server-profiler"></a>추적에서 스크립트 추출(SQL Server Profiler)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

이 항목에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 를 사용하여 추적 파일이나 테이블에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 이벤트를 추출하고 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]스크립트 파일로 저장하는 방법에 대해 설명합니다.  
  
### <a name="to-extract-a-transact-sql-script-from-a-trace-file-or-table"></a>추적 파일이나 테이블에서 Transact-SQL 스크립트를 추출하려면  
  
1.  [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 파일로 저장할 [!INCLUDE[tsql](../../includes/tsql-md.md)] 이벤트를 포함하는 추적 파일이나 테이블을 엽니다. 자세한 내용은 [추적 파일 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) 또는 [추적 테이블 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)에서 제공되는 사전 정의된 튜닝 템플릿을 사용합니다.  
  
2.  **파일** 메뉴에서 **내보내기**, **SQL Server 이벤트 추출**을 차례로 가리킨 다음 **Transact-SQL 이벤트 추출**을 클릭합니다.  
  
3.  **다른 이름으로 저장** 대화 상자에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 파일의 이름을 입력한 다음 **저장**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
