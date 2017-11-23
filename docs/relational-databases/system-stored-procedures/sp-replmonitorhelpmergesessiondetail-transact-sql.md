---
title: sp_replmonitorhelpmergesessiondetail (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_replmonitorhelpmergesessiondetail
- sp_replmonitorhelpmergesessiondetail_TSQL
helpviewer_keywords: sp_replmonitorhelpmergesessiondetail
ms.assetid: 805c92fc-3169-410c-984d-f37e063b791d
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 85338afafa7ca61b6cea5388c7a5f362edf35caa
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spreplmonitorhelpmergesessiondetail-transact-sql"></a>sp_replmonitorhelpmergesessiondetail(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 복제를 모니터링하는 데 사용되는 특정 복제 병합 에이전트 세션에 대한 자세한 아티클 수준 정보를 반환합니다. 결과 집합에는 세션 중에 동기화된 각 아티클에 대한 정보 행이 포함됩니다. 또한 세션 초기화를 나타내는 행과 세션의 업로드 및 다운로드 단계를 요약하는 행도 포함됩니다. 이 저장 프로시저는 배포 데이터베이스의 배포자 또는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replmonitorhelpmergesessiondetail [ @session_id = ] session_id  
```  
  
## <a name="arguments"></a>인수  
 [  **@session_id**  =] *session_id*  
 에이전트 세션을 지정합니다. *session_id* 은 **int** 이며 기본값은 없습니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**PhaseID**|**int**|동기화 세션의 단계를 나타내며 다음 중 하나일 수 있습니다.<br /><br /> **0** = 초기화 또는 요약 행<br /><br /> **1** = 업로드<br /><br /> **2** = 다운로드|  
|**ArticleName**|**sysname**|동기화 중인 아티클의 이름입니다. **ArticleName** 아티클 정보를 나타내지 않는 결과 집합의 행에 대 한 요약 정보도 포함 합니다.|  
|**PercentComplete**|**decimal**|현재 실행 중이거나 실패한 세션에 대해 지정한 아티클 정보 행에 적용된 전체 변경 내용의 비율을 나타냅니다.|  
|**RelativeCost**|**decimal**|아티클을 동기화하는 데 소요된 시간을 세션의 전체 동기화 시간에 대한 비율로 나타냅니다.|  
|**기간**|**int**|에이전트 세션의 길이입니다.|  
|**Inserts**|**int**|세션의 삽입 수입니다.|  
|**Updates**|**int**|세션의 업데이트 수입니다.|  
|**Deletes**|**int**|세션의 삭제 수입니다.|  
|**충돌**|**int**|세션에서 발생한 충돌 수입니다.|  
|**오류 Id**|**int**|세션 오류의 ID입니다.|  
|**SeqNo**|**int**|결과 집합의 세션 순서입니다.|  
|**RowType**|**int**|결과 집합에서 각 행이 나타내는 정보의 유형을 나타냅니다.<br /><br /> **0** = 초기화<br /><br /> **1** = 업로드 요약<br /><br /> **2** = 아티클 업로드 정보<br /><br /> **3** = 다운로드 요약<br /><br /> **4** = 아티클 다운로드 정보|  
|**SchemaChanges**|**int**|세션의 스키마 변경 수입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_replmonitorhelpmergesessiondetail** 병합 복제를 모니터링 하는 데 사용 됩니다.  
  
 구독자에서 실행 될 때 **sp_replmonitorhelpmergesessiondetail** 만 마지막 5 개 병합 에이전트 세션에 대 한 자세한 정보를 반환 합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **db_owner** 또는 **replmonitor** 고정된 데이터베이스 역할 또는 구독자에서 구독 데이터베이스 배포자에서 배포 데이터베이스에서 실행할 수 있습니다 **sp_ replmonitorhelpmergesessiondetail**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [프로그래밍 방식으로 복제 모니터링](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
