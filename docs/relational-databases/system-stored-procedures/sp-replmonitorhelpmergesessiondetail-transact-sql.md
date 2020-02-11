---
title: sp_replmonitorhelpmergesessiondetail (T-sql)
description: 특정 복제 병합 에이전트 세션에 대 한 자세한 아티클 수준 정보를 반환 하는 sp_replmonitorhelpmergesessiondetail 저장 프로시저에 대해 설명 합니다.
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelpmergesessiondetail
- sp_replmonitorhelpmergesessiondetail_TSQL
helpviewer_keywords:
- sp_replmonitorhelpmergesessiondetail
ms.assetid: 805c92fc-3169-410c-984d-f37e063b791d
author: stevestein
ms.author: sstein
ms.openlocfilehash: b5e29916d4dc8419311c9639cc5321b1cf391940
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75321625"
---
# <a name="sp_replmonitorhelpmergesessiondetail-transact-sql"></a>sp_replmonitorhelpmergesessiondetail(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  병합 복제를 모니터링하는 데 사용되는 특정 복제 병합 에이전트 세션에 대한 자세한 아티클 수준 정보를 반환합니다. 결과 집합에는 세션 중에 동기화된 각 아티클에 대한 정보 행이 포함됩니다. 또한 세션 초기화를 나타내는 행과 세션의 업로드 및 다운로드 단계를 요약하는 행도 포함됩니다. 이 저장 프로시저는 배포 데이터베이스의 배포자 또는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replmonitorhelpmergesessiondetail [ @session_id = ] session_id  
```  
  
## <a name="arguments"></a>인수  
`[ @session_id = ] session_id`에이전트 세션을 지정 합니다. *session_id* 은 **int** 이며 기본값은 없습니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**PhaseID**|**int**|동기화 세션의 단계를 나타내며 다음 중 하나일 수 있습니다.<br /><br /> **0** = 초기화 또는 요약 행<br /><br /> **1** = 업로드<br /><br /> **2** = 다운로드|  
|**ArticleName**|**sysname**|동기화 중인 아티클의 이름입니다. 또한 **m e** 에는 아티클 정보를 나타내지 않는 결과 집합의 행에 대 한 요약 정보가 포함 되어 있습니다.|  
|**PercentComplete**|**진수가**|현재 실행 중이거나 실패한 세션에 대해 지정한 아티클 정보 행에 적용된 전체 변경 내용의 비율을 나타냅니다.|  
|**RelativeCost**|**진수가**|아티클을 동기화하는 데 소요된 시간을 세션의 전체 동기화 시간에 대한 비율로 나타냅니다.|  
|**Duration**|**int**|에이전트 세션의 길이입니다.|  
|**클립보드**|**int**|세션의 삽입 수입니다.|  
|**업데이트**|**int**|세션의 업데이트 수입니다.|  
|**되며**|**int**|세션의 삭제 수입니다.|  
|**충돌**|**int**|세션에서 발생한 충돌 수입니다.|  
|**ErrorID**|**int**|세션 오류의 ID입니다.|  
|**SeqNo**|**int**|결과 집합의 세션 순서입니다.|  
|**RowType**|**int**|결과 집합에서 각 행이 나타내는 정보의 유형을 나타냅니다.<br /><br /> **0** = 초기화<br /><br /> **1** = 업로드 요약<br /><br /> **2** = 아티클 업로드 정보<br /><br /> **3** = 다운로드 요약<br /><br /> **4** = 아티클 다운로드 정보|  
|**SchemaChanges**|**int**|세션의 스키마 변경 수입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_replmonitorhelpmergesessiondetail** 는 병합 복제를 모니터링 하는 데 사용 됩니다.  
  
 구독자에서 실행 되는 경우 **sp_replmonitorhelpmergesessiondetail** 는 지난 5 병합 에이전트 세션에 대 한 자세한 정보만 반환 합니다.  
  
## <a name="permissions"></a>사용 권한  
 배포자의 배포 데이터베이스 또는 구독자의 구독 데이터베이스에 대 한 **db_owner** 또는 **replmonitor** 고정 데이터베이스 역할의 멤버만 **sp_replmonitorhelpmergesessiondetail**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [프로그래밍 방식으로 복제 모니터링](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
