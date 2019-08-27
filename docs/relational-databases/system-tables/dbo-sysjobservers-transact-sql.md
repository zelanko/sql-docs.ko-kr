---
title: dbo. sysjobservers (Transact-sql) | Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 03a4457cb5dd087639a439e9e9bb883eaf924366
ms.sourcegitcommit: 8c1c6232a4f592f6bf81910a49375f7488f069c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/26/2019
ms.locfileid: "70026202"
---
# <a name="dbosysjobservers-transact-sql"></a>dbo.sysjobservers(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

특정 작업과 하나 이상의 대상 서버와의 연관 또는 관계를 저장합니다. 이 테이블은 msdb 데이터베이스에 저장 됩니다.
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|job_id|**uniqueidentifier**|작업 ID입니다.|  
|server_id|**int**|서버 ID입니다.|  
|last_run_outcome|**tinyint**|작업이 마지막으로 실행되었을 때의 결과입니다.<br /><br /> **0** = 실패<br /><br /> **1** = 성공<br /><br /> **2** = 다시 시도<br /><br /> **3** = 취소<br /><br /> **4** = 진행 중<br /><br /> **5** = 알 수 없음 (다음 설명 섹션 참조) |  
|last_outcome_ 메시지|**nvarchar(1024)**|last_run_outcome 열과 연관된 메시지(있는 경우)입니다.|  
|last_run_date|**int**|작업을 마지막으로 실행한 날짜입니다.|  
|last_run_time|**int**|작업을 마지막으로 실행한 시간입니다.|  
|last_run_duration|**int**|작업의 실행 시간(시, 분, 초)입니다. (*시간*\*1만) + (*분*\*100) + *초*수식을 사용 하 여 계산 됩니다.|  


## <a name="remarks"></a>설명

*4* 보다 높은 값은 SQL 에이전트가 해당 작업의 상태를 알 수 없음을 의미 합니다. *Last_run_outcome* 는 작업을 만들 때 처음에 *5* 로 설정 됩니다.


## <a name="see-also"></a>관련 항목

[SQL Server 에이전트 테이블 &#40;transact-sql&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
