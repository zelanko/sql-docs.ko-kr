---
title: sysmergesubscriptions (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysmergesubscriptions_TSQL
- sysmergesubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergesubscriptions system table
ms.assetid: 6adc78da-991d-4c08-98c3-ecb4762e0e99
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 51640e20fe584cb8e8c89c3138920b830990fe1d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysmergesubscriptions-transact-sql"></a>sysmergesubscriptions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  알려진 각 구독자당 한 개의 행을 포함합니다. 게시자에서는 로컬 테이블에 해당합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|subscriber_server|**sysname**|서버의 ID입니다. 구독 데이터베이스의 사본을 다른 서버로 마이그레이션하는 경우 서버 지정 값에 srvid 필드를 매핑할 때 사용합니다.|  
|db_name|**sysname**|구독 데이터베이스의 이름입니다.|  
|pubid|**uniqueidentifier**|현재 구독을 만든 게시의 ID입니다.|  
|datasource_type|**int**|데이터 원본의 유형입니다.<br /><br /> **0** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> **2** = jet OLE DB입니다.|  
|subid|**uniqueidentifier**|구독에 대한 고유한 ID입니다.|  
|replnickname|**binary**|복제의 압축된 애칭입니다.|  
|replicastate|**uniqueidentifier**|게시자의 값을 구독자의 값과 비교하여 이전 동기화가 성공했는지 확인하는 데 사용되는 고유한 식별자입니다.|  
|상태|**tinyint**|구독 상태입니다.<br /><br /> **0** = 비활성입니다.<br /><br /> **1** = 활성 합니다.<br /><br /> **2** = 삭제 합니다.|  
|subscriber_type|**int**|구독자의 유형입니다.<br /><br /> **1** = 전역 합니다.<br /><br /> **2** = 로컬입니다.<br /><br /> **3** = 익명입니다.|  
|subscription_type|**int**|구독 유형은 다음과 같습니다.<br /><br /> **0** = 밀어넣기 합니다.<br /><br /> **1** = 끌어오기 합니다.<br /><br /> **2** = 익명입니다.|  
|sync_type|**tinyint**|동기화 유형입니다.<br /><br /> **1** = 자동입니다.<br /><br /> **2** = 동기화 없음.|  
|description|**nvarchar(255)**|구독에 대한 간단한 설명입니다.|  
|priority|**real**|구독 우선순위를 지정하고 우선순위를 기반으로 한 충돌 해결 구현을 허용합니다. Equals **0.00** 모든 로컬 또는 익명 구독에 대 한 합니다.|  
|recgen|**bigint**|마지막으로 받은 generation 번호입니다.|  
|recguid|**uniqueidentifier**|마지막으로 받은 generation의 고유한 ID입니다.|  
|sentgen|**bigint**|마지막으로 보낸 generation의 번호입니다.|  
|sentguid|**uniqueidentifier**|마지막으로 보낸 generation의 고유한 ID입니다.|  
|schemaversion|**int**|마지막으로 받은 스키마의 번호입니다.|  
|schemaguid|**uniqueidentifier**|마지막으로 받은 스키마의 고유한 ID입니다.|  
|last_validated|**datetime**|**datetime** 구독자 데이터의 마지막 성공한 유효성을 검사 합니다.|  
|attempted_validate|**datetime**|마지막 **datetime** 유효성 검사는 구독에 대해 시도 했습니다.|  
|last_sync_date|**datetime**|**datetime** 동기화 합니다.|  
|last_sync_status|**int**|동기화 상태입니다.<br /><br /> **0** = 모든 작업이 시작 되기를 기다리고 있습니다.<br /><br /> **1** = 하나 이상의 작업이 시작 됩니다.<br /><br /> **2** = 모든 작업이 성공적으로 실행 합니다.<br /><br /> **3** = 하나 이상의 작업이 실행 됩니다.<br /><br /> **4** = 모든 작업이 예약 되었으며 유휴 상태입니다.<br /><br /> **5** = 하나 이상의 작업 이전에 실패 한 후 실행 하려고 합니다.<br /><br /> **6** = 하나 이상의 작업이 성공적으로 실행에 실패 했습니다.|  
|last_sync_summary|**sysname**|마지막 동기화 결과에 관한 설명입니다.|  
|metadatacleanuptime|**datetime**|마지막 **datetime** 만료 된 메타 데이터를 병합 복제 시스템 테이블에서 제거 되었습니다.|  
|partition_id|**int**|구독이 속한 사전 계산 파티션을 식별합니다.|  
|cleanedup_unsent_changes|**bit**|보내지 않은 변경 사항에 대한 메타데이터가 구독자에서 정리되었음을 식별합니다.|  
|replica_version|**int**|구독이 속한 구독자의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 식별합니다. 다음 값 중 하나일 수 있습니다.<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|supportability_mode|**int**|내부적으로만 사용됩니다.|  
|application_name|**nvarchar(128)**|내부적으로만 사용됩니다.|  
|subscriber_number|**int**|내부적으로만 사용됩니다.|  
|last_makegeneration_datetime|**datetime**|마지막 **datetime** makegeneration 프로세스가 게시자에 대해 실행 된 합니다. 자세한 내용은의-MakeGenerationInterval 매개 변수를 참조 하십시오. [복제 병합 에이전트](../../relational-databases/replication/agents/replication-merge-agent.md)합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
