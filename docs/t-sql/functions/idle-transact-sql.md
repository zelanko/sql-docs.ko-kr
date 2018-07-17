---
title: '@@IDLE(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- '@@IDLE_TSQL'
- '@@IDLE'
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], idle
- ticks [SQL Server]
- '@@IDLE function'
- status information [SQL Server], idle time
- idle time [SQL Server]
ms.assetid: 8f49c62a-8da5-4afd-a5eb-4df8ef8be755
caps.latest.revision: 32
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c2eb99e1ab1d9f3aa36a3d1ec1c42c78c119f976
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37786104"
---
# <a name="x40x40idle-transact-sql"></a>&#x40;&#x40;IDLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 마지막으로 시작된 이후 유휴 상태인 시간을 반환합니다. 결과는 CPU 시간 단위("틱")로 표시되며 모든 CPU에 대해 누적됩니다. 따라서 실제 경과 시간을 초과할 수 있습니다. @@TIMETICKS를 곱하여 마이크로초로 변환합니다.  
  
> [!NOTE]  
>  @@CPU_BUSY 또는 @@IO_BUSY로 반환된 시간이 누적 CPU 시간의 약 49일을 초과할 경우 산술 오버플로 경고를 받게 됩니다. 이 경우 @@CPU_BUSY, @@IO_BUSY 및 @@IDLE 변수 값은 정확하지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@IDLE  
```  
  
## <a name="return-types"></a>반환 형식  
 **integer**  
  
## <a name="remarks"></a>Remarks  
 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 통계를 포함한 보고서를 표시하려면 **sp_monitor**를 실행합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 시작 시간과 현재 시간 사이에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 유휴 상태였던 시간을 밀리초 수로 보여 줍니다. 값을 마이크로초로 변환할 때 산술 오버플로가 발생하지 않도록 값 중 하나를 `float` 데이터 형식으로 변환합니다.  
  
```  
SELECT @@IDLE * CAST(@@TIMETICKS AS float) AS 'Idle microseconds',  
   GETDATE() AS 'as of';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
I  
Idle microseconds  as of                   
----------------- ----------------------  
8199934           12/5/2006 10:23:00 AM   
```  
  
## <a name="see-also"></a>참고 항목  
 [@@CPU_BUSY&#40;Transact-SQL&#41;](../../t-sql/functions/cpu-busy-transact-sql.md)   
 [sp_monitor&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [@@IO_BUSY&#40;Transact-SQL&#41;](../../t-sql/functions/io-busy-transact-sql.md)   
 [시스템 통계 함수&#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  
