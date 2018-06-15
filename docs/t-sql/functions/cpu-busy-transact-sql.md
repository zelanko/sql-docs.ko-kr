---
title: '@@CPU_BUSY(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 27eb30bf1a8b176024610affa368a8db1c6607e1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33052800"
---
# <a name="x40x40cpubusy-transact-sql"></a>&#x40;&#x40;CPU_BUSY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

이 함수는 최신 시작 이후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 활성 작업에서 소비한 시간을 반환합니다. `@@CPU_BUSY`는 CPU 시간 증가값 또는 "틱"에서 측정된 결과를 반환합니다. 이 값은 모든 CPU에 대해 누적됩니다. 따라서 실제 경과 시간을 초과할 수 있습니다. 마이크로초로 변환하려면 [@@TIMETICKS](./timeticks-transact-sql.md)를 곱합니다.
  
> [!NOTE]  
>  @@CPU_BUSY 또는 @@IO_BUSY에서 반환된 시간이 누적 CPU 시간의 약 49일을 초과할 경우 산술 오버플로 경고를 수신할 수 있습니다. 이 경우에 `@@CPU_BUSY`, `@@IO_BUSY` 및 `@@IDLE` 변수 값은 정확하지 않습니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```
@@CPU_BUSY  
```  
  
## <a name="return-types"></a>반환 형식
**integer**
  
## <a name="remarks"></a>Remarks  
CPU 활동을 포함하여 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 통계를 포함하는 보고서를 확인하려면 [sp_monitor](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)를 실행합니다.
  
## <a name="examples"></a>예  
이 예제에서는 현재 날짜 및 시간으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPU 작업을 반환합니다. 이 예제에서는 값 중 하나를 `float` 데이터 형식으로 변환합니다. 그러면 마이크로초 단위로 값을 계산할 때 산술 오버플로 문제를 방지합니다.
  
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
  
## <a name="see-also"></a>관련 항목:
[sys.dm_os_sys_info&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)  
[@@IDLE&#40;Transact-SQL&#41;](../../t-sql/functions/idle-transact-sql.md)  
[@@IO_BUSY&#40;Transact-SQL&#41;](../../t-sql/functions/io-busy-transact-sql.md)  
[sp_monitor&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)  
[시스템 통계 함수&#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)
  
  
