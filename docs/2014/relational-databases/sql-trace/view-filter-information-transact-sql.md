---
title: 필터 정보 보기(Transact-SQL) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- displaying filter information
- filters [SQL Server], viewing
- filters [SQL Server], traces
- traces [SQL Server], filters
- viewing filter information
ms.assetid: b7e52c13-8c83-47c2-8cd0-af7a49eceb5c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: abeeac1dc2c6d06a0b1ce89f4dff35415f7189fc
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52749135"
---
# <a name="view-filter-information-transact-sql"></a>필터 정보 보기(Transact-SQL)
  이 항목에서는 기본 제공 함수를 사용하여 추적 필터 정보를 보는 방법에 대해 설명합니다.  
  
### <a name="to-view-filter-information"></a>필터 정보를 보려면  
  
1.  원하는 필터 정보에 대한 추적 ID를 지정하고 **fn_trace_getfilterinfo** 를 실행합니다. 이 함수는 필터, 필터가 적용된 열 및 필터가 적용된 값을 나열하는 테이블을 반환합니다.  
  
     다음과 같이 이 함수를 호출하십시오.  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getfilterinfo(trace_id)  
    ```  
  
## <a name="see-also"></a>관련 항목  
 [sys.fn_trace_getfilterinfo&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)   
 [SQL Server Profiler 저장 프로시저&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  
