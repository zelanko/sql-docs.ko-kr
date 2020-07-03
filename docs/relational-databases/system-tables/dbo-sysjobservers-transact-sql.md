---
title: dbo.sysjobservers (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysjobservers
- sysjobservers_TSQL
- dbo.sysjobservers
- dbo.sysjobservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobservers system table
ms.assetid: 9abcc20f-a421-4591-affb-62674d04575e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3b02aa88951f7dd4e82ab26fcd54d715027b1ab7
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890457"
---
# <a name="dbosysjobservers-transact-sql"></a>dbo.sysjobservers(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

특정 작업과 하나 이상의 대상 서버와의 연관 또는 관계를 저장합니다. 이 테이블은 msdb 데이터베이스에 저장됩니다.
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|job_id|**uniqueidentifier**|작업 ID입니다.|  
|server_id|**int**|서버 ID입니다.|  
|last_run_outcome|**tinyint**|작업이 마지막으로 실행되었을 때의 결과입니다.<br /><br /> **0** = 실패<br /><br /> **1** = 성공<br /><br /> **2** = 다시 시도<br /><br /> **3** = 취소<br /><br /> **4** = 진행 중<br /><br /> **5** = 알 수 없음 (다음 설명 섹션 참조) |  
|last_outcome_ 메시지|**nvarchar(1024)**|last_run_outcome 열과 연관된 메시지(있는 경우)입니다.|  
|last_run_date|**int**|작업을 마지막으로 실행한 날짜입니다.|  
|last_run_time|**int**|작업을 마지막으로 실행한 시간입니다.|  
|last_run_duration|**int**|작업의 실행 시간(시, 분, 초)입니다. (*시간* \* 1만) + (*분* \* 100) + *초*수식을 사용 하 여 계산 됩니다.|  


## <a name="remarks"></a>설명

*4* 보다 높은 값은 SQL 에이전트가 해당 작업의 상태를 알 수 없음을 의미 합니다. 작업을 만들 때 처음에는 *last_run_outcome* *5* 로 설정 됩니다.


## <a name="see-also"></a>참고 항목

[Transact-sql&#41;&#40;테이블 SQL Server 에이전트](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
