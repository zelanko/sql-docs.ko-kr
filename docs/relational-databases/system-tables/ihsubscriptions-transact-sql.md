---
description: IHsubscriptions(Transact-SQL)
title: IHsubscriptions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHsubscriptions_TSQL
- IHsubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- IHsubscriptions system table
ms.assetid: 9ec21119-35f1-4e39-abaa-b2c790c485b1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b8dafdba96014fe7c60524a34d76d8bc36792762
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540939"
---
# <a name="ihsubscriptions-transact-sql"></a>IHsubscriptions(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **IHsubscriptions** 시스템 테이블은 현재 배포자를 사용 하 여 SQL Server 되지 않은 게시자의 게시에 대 한 각 구독에 대해 하나의 행을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
## <a name="definition"></a>정의  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|게시된 아티클을 고유하게 식별합니다.|  
|**srvid**|**smallint**|구독자의 서버 ID입니다.|  
|**dest_db**|**sysname**|대상 데이터베이스의 이름입니다.|  
|**login_name**|**sysname**|구독을 추가할 때 사용하는 로그인 이름입니다.|  
|**distribution_jobid**|**binary(16)**|배포 에이전트의 작업 ID입니다.|  
|**timestamp**|**timestamp**|구독을 만든 날짜와 시간입니다.|  
|**queued_reinit**|**bit**|아티클을 초기화 또는 다시 초기화하도록 표시할지 여부를 지정합니다. 값 **1** 은 구독 된 아티클이 초기화 또는 다시 초기화로 표시 되도록 지정 합니다.|  
|**status**|**tinyint**|구독 상태입니다.<br /><br /> **0** = 비활성<br /><br /> **1** = 구독 됨<br /><br /> **2** = 활성|  
|**sync_type**|**tinyint**|초기 동기화의 유형입니다.<br /><br /> **1** = 자동<br /><br /> **2** = 없음|  
|**subscription_type**|**int**|구독 유형은 다음과 같습니다.<br /><br /> **0** = 밀어넣기-배포 에이전트가 구독자에서 실행 됩니다.<br /><br /> **1** = 끌어오기-배포 에이전트가 배포자에서 실행 됩니다.|  
|**update_mode**|**tinyint**|업데이트 모드입니다.<br /><br /> **0** = 읽기 전용입니다.<br /><br /> **1** = 즉시 업데이트|  
|**loopback_detection**|**bit**|양방향 트랜잭션 복제 토폴로지에 속한 구독에 적용됩니다. 루프백 검색은 배포 에이전트가 구독자에서 발생한 트랜잭션을 다시 구독자로 보낼지 여부를 결정합니다.<br /><br /> **0** = 다시 보냅니다.<br /><br /> **1** = 다시 보내지 않습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;복제 뷰 ](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Transact-sql&#41;sp_addsubscription &#40;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [Transact-sql&#41;sp_helpsubscription &#40;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
