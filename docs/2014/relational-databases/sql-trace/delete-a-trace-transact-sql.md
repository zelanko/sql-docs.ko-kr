---
title: 추적 삭제(Transact-SQL) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], deleting
- removing traces
- deleting traces
ms.assetid: a5502814-b281-42dd-b885-5c9368025ae6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 57d80824ab0dde301a0b96239636cf0f79ca032c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62714741"
---
# <a name="delete-a-trace-transact-sql"></a>추적 삭제(Transact-SQL)
  이 항목에서는 저장 프로시저를 사용하여 추적을 삭제하는 방법에 대해 설명합니다.  
  
 추적 저장 프로시저 사용에 대한 예는 [추적 만들기&#40;Transact-SQL&#41;](create-a-trace-transact-sql.md)를 참조하세요.  
  
### <a name="to-delete-a-trace"></a>추적을 삭제하려면  
  
1.  **@status = 0**을 지정해서 **sp_trace_setstatus**를 실행하여 추적을 중지합니다.  
  
2.  **@status = 2**를 지정해서 **sp_trace_setstatus**를 실행하여 추적을 닫고 서버에서 추적 정보를 삭제합니다.  
  
> [!NOTE]  
>  추적은 먼저 중지한 후 닫아야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_trace_setstatus&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)   
 [SQL Server Profiler 저장 프로시저&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  
