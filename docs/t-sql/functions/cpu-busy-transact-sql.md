---
title: '@@CPU_BUSY (Transact SQL) | Microsoft Docs'
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
- '@@CPU_BUSY_TSQL'
- '@@CPU_BUSY'
dev_langs:
- TSQL
helpviewer_keywords:
- CPU [SQL Server]
- status information [SQL Server], CPU
- ticks [SQL Server]
- time [SQL Server], CPU activity
- '@@CPU_BUSY function'
- statistical information [SQL Server], CPU
- CPU [SQL Server], activity
ms.assetid: 81ae0e64-79fa-4a74-9aa5-37045c4cd211
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 337682a73ae351536af64afca77959cbe6297d7f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40cpubusy-transact-sql"></a>&#x40;&#x40;CPU_BUSY (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 마지막으로 시작된 이후의 사용 시간을 반환합니다. 결과는 CPU 시간 증가값 또는 "틱"으로 표시되며 모든 CPU에 대해 누적됩니다. 따라서 실제 경과 시간을 초과할 수 있습니다. 곱한@TIMETICKS 을 마이크로초로 변환할 합니다.
  
> [!NOTE]  
>  반환 되는 시간@CPU_BUSY 또는 @@IO_BUSY 약 49 일의 누적 CPU 시간 초과, 산술 오버플로 경고를 수신 합니다. @ 값의 경우@CPU_BUSY, @@IO_BUSY 및 @@IDLE 변수 정확 하지 않습니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```
@@CPU_BUSY  
```  
  
## <a name="return-types"></a>반환 형식
**integer**
  
## <a name="remarks"></a>주의  
몇 가지를 포함 하는 보고서를 표시 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 CPU 활동을 포함 하 여 통계 [sp_monitor](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)합니다.
  
## <a name="examples"></a>예  
다음 예에서는 현재 날짜 및 시간의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPU 작업을 반환합니다. 값을 마이크로초로 변환할 때 산술 오버플로가 발생하지 않도록 값 중 하나를 `float` 데이터 형식으로 변환합니다.
  
```sql
SELECT @@CPU_BUSY * CAST(@@TIMETICKS AS float) AS 'CPU microseconds',   
   GETDATE() AS 'As of' ;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
CPU microseconds As of
---------------- -----------------------
18406250         2006-12-05 17:00:50.600
```
  
## <a name="see-also"></a>참고 항목
[sys.dm_os_sys_info &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)  
[@@IDLE&#40;Transact-SQL&#41;](../../t-sql/functions/idle-transact-sql.md)  
[@@IO_BUSY&#40;Transact-SQL&#41;](../../t-sql/functions/io-busy-transact-sql.md)  
[sp_monitor &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)  
[시스템 통계 함수 &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)
  
  
