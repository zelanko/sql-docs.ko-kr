---
title: "테이블 (SQL Server Profiler)에 추적 결과 저장 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
ms.assetid: edbecf74-683b-4e43-a1ef-7a3d5f5e27f6
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 47c21a4e8505dedbb6f9b811aba09302aeaf019b
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="save-trace-results-to-a-table-sql-server-profiler"></a>테이블에 추적 결과 저장(SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]이 항목에서는 사용 하 여 데이터베이스 테이블에 추적 결과 저장 하는 방법을 설명 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]합니다.  
  
### <a name="to-save-trace-results-to-a-table"></a>추적 결과를 테이블에 저장하려면  
  
1.  **파일** 메뉴에서 **새 추적**을 클릭한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결합니다.  
  
     **추적 속성**대화 상자가 표시됩니다.  
  
    > [!NOTE]  
    >  **연결한 후 즉시 추적 시작**을 선택한 경우에는 **추적 속성**대화 상자가 나타나지 않고 추적이 시작됩니다. 이 설정을 해제하려면 **도구**메뉴에서 **옵션**을 클릭한 다음 **연결한 후 즉시 추적 시작** 확인란의 선택을 취소합니다.  
  
2.  **추적 이름** 입력란에 추적 이름을 입력한 다음 **테이블에 저장**을 클릭합니다.  
  
3.  **서버에 연결** 대화 상자에서 추적 테이블을 포함할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결합니다.  
  
4.  **대상 테이블** 대화 상자의 **데이터베이스**목록에서 데이터베이스를 선택합니다.  
  
5.  **소유자** 목록에서 추적의 소유자를 선택합니다.  
  
6.  **테이블** 목록에서 추적 결과에 대한 테이블 이름을 입력하거나 선택합니다. **확인.**  
  
7.  **추적 속성** 대화 상자에서 **최대 행 수 설정(천 단위)**확인란을 선택하여 저장할 최대 행 수를 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 프로파일러](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
