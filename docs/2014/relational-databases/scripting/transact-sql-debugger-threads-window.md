---
title: 스레드 창
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Threads Window [Transact-SQL]
ms.assetid: e153f619-0049-4162-9076-c24a454f3278
author: rothja
ms.author: jroth
ms.openlocfilehash: 6f3460c892c182996a753c2a16076418a6b2008f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063332"
---
# <a name="threads-window"></a>스레드 창
  **스레드** 창에서는 디버깅 중인 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 세션에서 사용하는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 스레드에 대한 정보를 표시합니다. 스레드 정보를 표시하려면 디버그 모드여야 합니다.  
  
## <a name="task-list"></a>작업 목록  
 **스레드 창에 액세스하려면**  
  
-   **디버그** 메뉴에서 **창**을 선택한 다음 **스레드**를 클릭합니다.  
  
## <a name="columns"></a>열  
 **ID**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거가 스레드에 할당하는 고유한 식별 번호입니다. sys.dm_os_threads 동적 관리 뷰에서 행을 선택하면 스레드에 대한 자세한 내용을 확인할 수 있습니다.  
  
 경량 풀링 모드로 실행 중이 아닌 경우 os_thread_id의 값이 **ID** 열 값과 일치하는 행을 선택합니다. 경량 풀링 모드로 실행 중인 경우 fiber_context_address의 값이 **ID** 열 값과 일치하는 행을 선택합니다.  
  
 **이름**  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 세션에 대한 정보를 **컴퓨터 이름/인스턴스 이름 [SPID]** 형식으로 표시합니다.  
  
 **컴퓨터 이름**  
 쿼리 편집기 세션이 연결된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 실행하는 컴퓨터의 이름입니다.  
  
 **InstanceName**  
 쿼리 편집기 세션이 연결된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스의 이름입니다.  
  
 **[SPID]**  
 이 세션을 고유하게 식별하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 세션 프로세스 ID입니다. spid 열과 값이 값은 sys.sysprocesses 뷰의 행을 선택하면 세션에 대한 자세한 내용을 확인할 수 있습니다.  
  
 **위치**  
 디버깅 중인 쿼리 편집기 세션에서 사용하는 스크립트 파일의 이름을 표시합니다.  
  
 **우선 순위**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거는 이 기능을 지원하지 않습니다.  
  
 **일시 중지됨**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거는 이 기능을 지원하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-SQL 디버거](transact-sql-debugger.md)   
 [Transact-SQL 디버거 정보](transact-sql-debugger-information.md)   
 [sys.dm_os_threads&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql)   
 [sys.sysprocesses&#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql)  
