---
title: Transact-SQL 스크립트 재생(SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: profiler
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- scripts [SQL Server], traces
- replaying traces
ms.assetid: 9c0eb222-e6e3-4bc1-a25f-a41e962d361b
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bfda646b7bd7211067bb146ff31d95bcd3662ccc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="replay-a-transact-sql-script-sql-server-profiler"></a>Transact-SQL 스크립트 재생(SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  성능 문제에 대해 가능한 해결 방법을 테스트하는 경우 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 재생하고 변경 전후의 성능을 비교합니다.  
  
### <a name="to-replay-a-transact-sql-script"></a>Transact-SQL 스크립트를 재생하려면  
  
1.  **파일** 메뉴에서 **열기**를 가리킨 다음 **스크립트 파일**을 클릭합니다.  
  
2.  열려는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 파일을 선택합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트가 재생에 필요한 이벤트를 포함하고 있어야 합니다. 자세한 내용은 [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)을 참조하세요.  
  
3.  **재생** 메뉴에서 **시작**을 클릭하고 스크립트를 재생하려는 서버에 연결합니다.  
  
4.  **재생 구성** 대화 상자에서 설정을 확인한 다음 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [추적 재생](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server 프로파일러](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
