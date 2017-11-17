---
title: '@@TOTAL_ERRORS (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@TOTAL_ERRORS'
- '@@TOTAL_ERRORS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@TOTAL_ERRORS function'
- total errors [SQL Server]
- errors [SQL Server], read/write
- number of disk read/write errors
- disks [SQL Server], errors
- write errors [SQL Server]
- read/write errors
ms.assetid: 09e62428-ee0e-4ef5-b969-da9d255f1199
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 65268d94ec7a12fd66587751ac9a93dc192be566
ms.contentlocale: ko-kr
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40totalerrors-transact-sql"></a>& #x 40; & #x 40; TOTAL_ERRORS (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 마지막으로 시작된 이후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 발생한 디스크 쓰기 오류 수를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@TOTAL_ERRORS  
```  
  
## <a name="return-types"></a>반환 형식  
 **integer**  
  
## <a name="remarks"></a>주의  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 발생한 모든 쓰기 오류가 반환되는 것은 아닙니다. 사소한 쓰기 오류는 서버 자체에서 처리되며 오류로 처리되지 않는 경우도 있습니다. 몇 가지를 포함 하는 보고서를 표시 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 오류의 총 수를 포함 하 여 통계 **sp_monitor**합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 날짜 및 시간에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 발생한 오류 수를 보여 줍니다.  
  
```  
SELECT @@TOTAL_ERRORS AS 'Errors', GETDATE() AS 'As of';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Errors      As of                   
----------- ----------------------  
0           3/28/2003 12:32:11 PM   
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_monitor &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [시스템 통계 함수 &#40; Transact SQL &#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  

