---
title: sp_monitor (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5312413386dae9915b9ac6649b4210541d45b1db
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644431"
---
# <a name="spmonitor-transact-sql"></a>sp_monitor(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  에 대 한 통계를 표시 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_monitor  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|Description|  
|-----------------|-----------------|  
|**last_run**|시간 **sp_monitor** 을 마지막으로 실행 합니다.|  
|**current_run**|시간 **sp_monitor** 를 실행 합니다.|  
|**seconds**|이후 경과 된 초 수 **sp_monitor** 실행 되었습니다.|  
|**cpu_busy**|서버 컴퓨터의 CPU가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업을 수행한 시간(초)입니다.|  
|**io_busy**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 입력 및 출력 작업을 수행하는 데 걸린 시간(초)입니다.|  
|**유휴 상태**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 유휴 상태에 있던 시간(초)입니다.|  
|**packets_received**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 읽은 입력 패킷 수입니다.|  
|**packets_sent**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 쓰여진 출력 패킷 수입니다.|  
|**packet_errors**|패킷을 읽고 쓰면서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 발생한 오류 수입니다.|  
|**total_read**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이루어진 읽기 작업 수입니다.|  
|**total_write**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이루어진 쓰기 작업 수입니다.|  
|**total_errors**|읽고 쓰는 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 발생한 오류 수입니다.|  
|**연결**|로그인 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 시도한 로그인 수입니다.|  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 일련의 함수를 통해 수행한 작업량을 추적합니다. 실행 **sp_monitor** 이러한 함수로 반환 된 현재 값을 표시 하 고 프로시저를 실행 된 마지막 시간 이후 변경 된 정도 보여 줍니다.  
  
 형태로 각 열에 대 한 통계가 출력 됩니다 *수*(*번호*)-*번호*% 또는 *번호*(*수*). 첫 번째 *수* 시간 (초) 수를 나타냅니다 (에 대 한 **cpu_busy**하십시오 **io_busy**, 및 **유휴**) 또는 총 수 (에 대 한 다른 변수) 이므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다시 시작 되었습니다. *번호* 괄호로 초 또는 마지막 시간 이후 총 수를 의미 **sp_monitor** 실행 되었습니다. 백분율은 이후 시간 비율로 **sp_monitor** 을 마지막으로 실행 합니다. 예를 들어 보고서를 보여 줍니다 **cpu_busy** 으로 4250 (215)-68 %CPU 되었습니다 이후의 사용 중인 4250 초 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이후의 215 초를 마지막으로 시작한 **sp_monitor** 마지막 실행 및 68%를 총 시간 이후 **sp_monitor** 을 마지막으로 실행 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 얼마나 많이 사용되었는지에 대한 정보를 보고합니다.  
  
```  
USE master  
EXEC sp_monitor  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
||||  
|-|-|-|  
|**last_run**|**current_run**|**seconds**|  
|Mar 29 1998 11:55AM|Apr 4 1998 2:22 PM|561|  
  
||||  
|-|-|-|  
|**cpu_busy**|**io_busy**|**유휴 상태**|  
|190(0)-0%|187(0)-0%|148(556)-99%|  
  
||||  
|-|-|-|  
|**packets_received**|**packets_sent**|**packet_errors**|  
|16(1)|20(2)|0(0)|  
  
|||||  
|-|-|-|-|  
|**total_read**|**total_write**|**total_errors**|**연결**|  
|141(0)|54920(127)|0(0)|4(0)|  
  
## <a name="see-also"></a>관련 항목  
 [sp_who&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
