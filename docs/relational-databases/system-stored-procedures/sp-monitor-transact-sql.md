---
description: sp_monitor(Transact-SQL)
title: sp_monitor (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_monitor_TSQL
- sp_monitor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_monitor
ms.assetid: cb628496-2f9b-40e4-b018-d0831c4cb018
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6722a59873dcf672fe2c1b953931f44da4515a8e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446995"
---
# <a name="sp_monitor-transact-sql"></a>sp_monitor(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  에 대 한 통계 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 표시 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_monitor  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|설명|  
|-----------------|-----------------|  
|**last_run**|**Sp_monitor** 마지막으로 실행 된 시간입니다.|  
|**current_run**|**Sp_monitor** 실행 되는 시간입니다.|  
|**까지의**|**Sp_monitor** 실행 된 이후 경과 된 시간 (초)입니다.|  
|**cpu_busy**|서버 컴퓨터의 CPU가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업을 수행한 시간(초)입니다.|  
|**io_busy**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 입력 및 출력 작업을 수행하는 데 걸린 시간(초)입니다.|  
|**유휴**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 유휴 상태에 있던 시간(초)입니다.|  
|**packets_received**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 읽은 입력 패킷 수입니다.|  
|**packets_sent**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 쓰여진 출력 패킷 수입니다.|  
|**packet_errors**|패킷을 읽고 쓰면서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 발생한 오류 수입니다.|  
|**total_read**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이루어진 읽기 작업 수입니다.|  
|**total_write**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이루어진 쓰기 작업 수입니다.|  
|**total_errors**|읽고 쓰는 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 발생한 오류 수입니다.|  
|**연결만**|로그인 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 시도한 로그인 수입니다.|  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 일련의 함수를 통해 수행한 작업량을 추적합니다. **Sp_monitor** 를 실행 하면 이러한 함수가 반환 하는 현재 값이 표시 되 고, 프로시저가 마지막으로 실행 된 이후 변경 된 값이 표시 됩니다.  
  
 각 열에 대해 *숫자*(*number*)-*number*% 또는 *number*(*number*) 형식으로 통계가 출력 됩니다. 첫 번째 *숫자* 는가 다시 시작 된 이후 경과 된 시간 (초) ( **cpu_busy**, **io_busy**및 **유휴**)의 수 또는 다른 변수에 대 한 총 수를 나타냅니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 괄호 안의 *숫자* 는 **sp_monitor** 가 마지막으로 실행 된 이후 경과 된 시간 (초) 또는 총 수를 나타냅니다. 백분율은 **sp_monitor** 마지막으로 실행 된 이후 경과 된 시간의 백분율입니다. 예를 들어 보고서가 4250 (215)-68%로 **cpu_busy** 표시 되는 경우, 마지막으로 시작 된 이후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 215 초, **sp_monitor** 마지막으로 실행 된 이후 초, cpu가 마지막으로 실행 된 이후 총 **sp_monitor** 시간에 대 한 68%가 시작 된 이후 cpu가 4250 사용 되는 것입니다.  
  
## <a name="permissions"></a>사용 권한  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 얼마나 많이 사용되었는지에 대한 정보를 보고합니다.  
  
```console
USE master  
EXEC sp_monitor  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

```console
last_run       current_run                   seconds
-----------    --------------------------    ---------
Mar 29 1998    11:55AM Apr 4 1998 2:22 PM    561

cpu_busy           io_busy     idle
---------------    ---------   --------------
190(0)-0%          187(0)-0%   148(556)-99%

packets_received       packets_sent    packet_errors
----------------       ------------    -------------
16(1)                  20(2)           0(0)

total_read     total_write   total_errors    connections
-----------    -----------   -------------   -----------
141(0)         54920(127)    0(0)            4(0)
```
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_who &#40;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
