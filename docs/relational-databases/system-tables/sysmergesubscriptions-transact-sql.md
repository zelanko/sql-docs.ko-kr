---
description: sysmergesubscriptions(Transact-SQL)
title: sysmergesubscriptions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergesubscriptions_TSQL
- sysmergesubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergesubscriptions system table
ms.assetid: 6adc78da-991d-4c08-98c3-ecb4762e0e99
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ffb85633adfe9b8aceb05a5188e67e951d6be190
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473176"
---
# <a name="sysmergesubscriptions-transact-sql"></a>sysmergesubscriptions(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  알려진 각 구독자당 한 개의 행을 포함합니다. 게시자에서는 로컬 테이블에 해당합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|subscriber_server|**sysname**|서버의 ID입니다. 구독 데이터베이스의 사본을 다른 서버로 마이그레이션하는 경우 서버 지정 값에 srvid 필드를 매핑할 때 사용합니다.|  
|db_name|**sysname**|구독 데이터베이스의 이름입니다.|  
|pubid|**uniqueidentifier**|현재 구독을 만든 게시의 ID입니다.|  
|datasource_type|**int**|데이터 원본의 유형입니다.<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> **2** = Jet OLE DB.|  
|subid|**uniqueidentifier**|구독에 대한 고유한 ID입니다.|  
|replnickname|**binary**|복제의 압축된 애칭입니다.|  
|replicastate|**uniqueidentifier**|게시자의 값을 구독자의 값과 비교하여 이전 동기화가 성공했는지 확인하는 데 사용되는 고유한 식별자입니다.|  
|상태|**tinyint**|구독 상태입니다.<br /><br /> **0** = 비활성<br /><br /> **1** = 활성<br /><br /> **2** = 삭제 됨.|  
|subscriber_type|**int**|구독자의 유형입니다.<br /><br /> **1** = 전역<br /><br /> **2** = 로컬<br /><br /> **3** = 익명.|  
|subscription_type|**int**|구독 유형은 다음과 같습니다.<br /><br /> **0** = 푸시합니다.<br /><br /> **1** = 끌어오기<br /><br /> **2** = 익명.|  
|sync_type|**tinyint**|동기화 유형입니다.<br /><br /> **1** = 자동<br /><br /> **2** = 동기화 하지 않습니다.|  
|description|**nvarchar(255)**|구독에 대한 간단한 설명입니다.|  
|priority|**real**|구독 우선순위를 지정하고 우선순위를 기반으로 한 충돌 해결 구현을 허용합니다. 모든 로컬 또는 익명 구독에 대해 **0.00** 가 동일 합니다.|  
|recgen|**bigint**|마지막으로 받은 generation 번호입니다.|  
|recguid|**uniqueidentifier**|마지막으로 받은 generation의 고유한 ID입니다.|  
|sentgen|**bigint**|마지막으로 보낸 generation의 번호입니다.|  
|sentguid|**uniqueidentifier**|마지막으로 보낸 generation의 고유한 ID입니다.|  
|schemaversion|**int**|마지막으로 받은 스키마의 번호입니다.|  
|schemaguid|**uniqueidentifier**|마지막으로 받은 스키마의 고유한 ID입니다.|  
|last_validated|**datetime**|구독자 데이터에 대해 마지막으로 성공한 유효성 검사의 **날짜/시간** 입니다.|  
|attempted_validate|**datetime**|구독에서 유효성 검사를 시도한 마지막 **날짜/시간** 입니다.|  
|last_sync_date|**datetime**|동기화의 **날짜/시간** 입니다.|  
|last_sync_status|**int**|동기화 상태입니다.<br /><br /> **0** = 모든 작업이 시작 되기를 기다리고 있습니다.<br /><br /> **1** = 하나 이상의 작업이 시작 됩니다.<br /><br /> **2** = 모든 작업이 성공적으로 실행 되었습니다.<br /><br /> **3** = 하나 이상의 작업이 실행 중입니다.<br /><br /> **4** = 모든 작업이 예약 되 고 유휴 상태가 됩니다.<br /><br /> **5** = 이전 실패 후 하나 이상의 작업을 실행 하려고 합니다.<br /><br /> **6** = 하나 이상의 작업이 성공적으로 실행 되지 못했습니다.|  
|last_sync_summary|**sysname**|마지막 동기화 결과에 관한 설명입니다.|  
|metadatacleanuptime|**datetime**|만료 된 메타 데이터가 병합 복제 시스템 테이블에서 제거 된 마지막 **날짜/시간** 입니다.|  
|partition_id|**int**|구독이 속한 사전 계산 파티션을 식별합니다.|  
|cleanedup_unsent_changes|**bit**|보내지 않은 변경 사항에 대한 메타데이터가 구독자에서 정리되었음을 식별합니다.|  
|replica_version|**int**|구독이 속한 구독자의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 식별합니다. 다음 값 중 하나일 수 있습니다.<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|supportability_mode|**int**|내부적으로만 사용됩니다.|  
|application_name|**nvarchar(128)**|내부적으로만 사용됩니다.|  
|subscriber_number|**int**|내부적으로만 사용됩니다.|  
|last_makegeneration_datetime|**datetime**|Makegeneration 프로세스가 게시자에 대해 실행 한 마지막 **날짜/시간** 입니다. 자세한 내용은 [Replication 병합 에이전트](../../relational-databases/replication/agents/replication-merge-agent.md)의-MakeGenerationInterval 매개 변수를 참조 하세요.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
