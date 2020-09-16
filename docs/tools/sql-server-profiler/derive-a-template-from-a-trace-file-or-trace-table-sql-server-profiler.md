---
title: 추적 파일 또는 추적 테이블에서 템플릿 파생
titleSuffix: SQL Server Profiler
description: SQL Server Profiler를 사용하여 기존 추적 파일에서 또는 데이터베이스에 저장된 추적 테이블에서 추적 템플릿을 만드는 방법을 알아봅니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 305817b7-4d23-49fb-9e6c-4d34359877bf
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 02af487c0d7301ce7d5d71ff046b90fb25efc8ab
ms.sourcegitcommit: a9f16d7819ed0e2b7ad8f4a7d4d2397437b2bbb2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88713711"
---
# <a name="derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler"></a>추적 파일 또는 추적 테이블에서 템플릿 파생(SQL Server Profiler)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 기존 추적 파일이나 테이블에서 추적 템플릿을 만드는 방법에 대해 설명합니다.  
  
### <a name="to-derive-a-template-from-a-trace-file-or-trace-table"></a>추적 파일 또는 추적 테이블에서 템플릿을 파생시키려면  
  
1.  템플릿의 기반이 될 추적 파일이나 추적 테이블을 엽니다. 자세한 내용은 [추적 파일 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) 또는 [추적 테이블 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)에서 제공되는 사전 정의된 튜닝 템플릿을 사용합니다.  
  
2.  **파일** 메뉴에서 **다른 이름으로 저장**을 가리킨 다음 **추적 템플릿**을 클릭합니다.  
  
3.  이름을 입력하거나 목록에서 이름을 선택합니다. **확인**을 클릭합니다.  
  
> [!NOTE]  
>  기존 템플릿 파일을 선택하면 파일을 덮어쓸 것인지를 묻는 메시지가 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [추적 템플릿 만들기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)   
 [추적 템플릿 수정&#40;SQL Server Profiler&#41;](./modify-trace-templates.md?view=sql-server-ver15)   
 [실행 중인 추적으로부터 템플릿 파생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
