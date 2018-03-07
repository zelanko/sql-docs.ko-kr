---
title: '@@IO_BUSY (Transact SQL) | Microsoft Docs'
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
- '@@IO_BUSY'
- '@@IO_BUSY_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- ticks [SQL Server]
- I/O [SQL Server], time spent performing operations
- '@@IO_BUSY function'
- output operations [SQL Server]
- input operations [SQL Server]
- time [SQL Server], I/O operations
ms.assetid: 3c26770c-41ae-4e34-8c82-7bef920ffbca
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d42b1961a8e2c4b6feb43f415f43968fbf68fd8a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40iobusy-transact-sql"></a>&#x40;&#x40;IO_BUSY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 마지막으로 시작한 이후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 입력 및 출력 작업에 소요된 시간을 반환합니다. 결과는 CPU 시간 단위("틱")로 표시되며 모든 CPU에 대해 누적됩니다. 따라서 실제 경과 시간을 초과할 수 있습니다. 곱한@TIMETICKS 을 마이크로초로 변환할 합니다.  
  
> [!NOTE]  
>  반환 되는 시간@CPU_BUSY, 또는 @@IO_BUSY 약 49 일의 누적 CPU 시간 초과, 산술 오버플로 경고를 수신 합니다. @ 값의 경우@CPU_BUSY, @@IO_BUSY 및 @@IDLE 변수 정확 하지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@IO_BUSY  
```  
  
## <a name="return-types"></a>반환 형식  
 **integer**  
  
## <a name="remarks"></a>주의  
 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 통계를 포함한 보고서를 표시하려면 sp_monitor를 실행합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 시작 시간과 현재 시간 사이에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 입/출력 작업을 수행한 시간을 밀리초 단위로 반환합니다. 이 예제에서는 변환 하는 값 중 하나를 값을 마이크로초로 변환할 때 산술 오버플로 방지 하려면는 **float** 데이터 형식입니다.  
  
```  
SELECT @@IO_BUSY*@@TIMETICKS AS 'IO microseconds',   
   GETDATE() AS 'as of';  
```  
  
 일반적인 결과 집합은 다음과 같습니다.  
  
```  
  
IO microseconds as of                   
--------------- ----------------------  
4552312500      12/5/2006 10:23:00 AM   
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [@@CPU_BUSY&#40;Transact-SQL&#41;](../../t-sql/functions/cpu-busy-transact-sql.md)   
 [sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [시스템 통계 함수 &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  
