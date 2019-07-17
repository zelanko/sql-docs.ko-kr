---
title: sysarticles (시스템 뷰) (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticles
- sysarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticles view
ms.assetid: 18f8c9b3-cab7-4e8f-8754-11ac38c3f789
author: stevestein
ms.author: sstein
ms.openlocfilehash: f0d1f6c1036d946088e2cc1aa91c08f620c3f597
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129544"
---
# <a name="sysarticles-system-view-transact-sql"></a>sysarticles(시스템 뷰)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **sysarticles** 뷰는 아티클 속성입니다. 이 뷰는 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|아티클에 대해 고유한 ID를 제공하는 ID 열입니다.|  
|**creation_script**|**nvarchar(255)**|아티클에 대한 스키마 스크립트입니다.|  
|**del_cmd**|**nvarchar(255)**|DELETE 시 실행할 명령입니다. 그렇지 않으면 로그에서 만들어집니다.|  
|**description**|**nvarchar(255)**|아티클에 대한 설명 항목입니다.|  
|**dest_table**|**sysname**|대상 테이블의 이름입니다.|  
|**filter**|**int**|수평 분할에 사용하는 저장 프로시저 ID입니다.|  
|**filter_clause**|**ntext**|행 필터링에 사용하는 아티클의 WHERE 절입니다.|  
|**ins_cmd**|**nvarchar(255)**|INSERT 시 실행할 명령입니다. 그렇지 않으면 로그에서 생성됩니다.|  
|**name**|**sysname**|아티클과 관련된 이름이며 게시 내에서 고유합니다.|  
|**objid**|**int**|게시된 테이블 개체 ID입니다.|  
|**pubid**|**int**|아티클이 속한 게시의 ID입니다.|  
|**pre_creation_cmd**|**tinyint**|DROP TABLE, DELETE TABLE 또는 TRUNCATE에 대한 사전 생성 명령입니다.<br /><br /> **0** = none입니다.<br /><br /> **1** = DROP.<br /><br /> **2** = DELETE.<br /><br /> **3** = TRUNCATE.|  
|**상태**|**tinyint**|아티클 옵션 및 상태의 비트 마스크이며 다음 값 중 하나 이상에 대한 논리 비트 OR 연산의 결과일 수 있습니다.<br /><br /> **1** = 아티클이 활성 상태입니다.<br /><br /> **8** = INSERT 문에 열 이름을 포함 합니다.<br /><br /> **16** = 문을 매개 변수화 사용 합니다.<br /><br /> **24** = INSERT 문에 열 이름을 포함 하 고 매개 변수가 있는 문을 사용 하 여 둘 다.<br /><br /> **64** = 변환 가능한 구독에 의해 정의 되는 아티클의 대 한 수평 분할 합니다.<br /><br /> 예를 들어 매개 변수가 있는 문을 사용 하는 활성 아티클은 값 미칠 **17** 이 열에 있습니다. 값이 **0** 는 아티클이 활성 상태입니다. 추가 속성 없이 정의 된 의미 합니다.|  
|**sync_objid**|**int**|아티클 정의를 나타내는 테이블 또는 뷰의 ID입니다.|  
|**type**|**tinyint**|아티클의 유형입니다.<br /><br /> **1** = 로그 기반 아티클입니다.<br /><br /> **3** = 수동 필터가 있는 로그 기반 아티클입니다.<br /><br /> **5** = 수동 뷰가 있는 로그 기반 아티클입니다.<br /><br /> **7** = 수동 필터 및 수동 뷰가 있는 로그 기반 아티클입니다.<br /><br /> **8** = 저장 프로시저 실행 합니다.<br /><br /> **24** = 직렬화 가능 프로시저 실행 합니다.<br /><br /> **32** = 저장 프로시저 (스키마 전용).<br /><br /> **64** = 뷰 (스키마 전용).<br /><br /> **128** = 함수 (스키마 전용).|  
|**upd_cmd**|**nvarchar(255)**|UPDATE 시 실행할 명령입니다. 그렇지 않으면 로그에서 만들어집니다.|  
|**schema_option**|**binary(8)**|아티클에 대한 스키마 생성 옵션의 비트 마스크입니다. 이 옵션은 구독자에게 전달하기 위해 스크립팅할 아티클 스키마 부분을 제어합니다. 스키마 옵션에 대한 자세한 내용은 [sp_addarticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)을 참조하세요.|  
|**dest_owner**|**sysname**|대상 데이터베이스에 있는 테이블의 소유자입니다.|  
|**ins_scripting_proc**|**int**|INSERT 문이 복제될 때 실행되는 등록된 사용자 지정 저장 프로시저 또는 스크립트입니다.|  
|**del_scripting_proc**|**int**|DELETE 문이 복제될 때 실행되는 등록된 사용자 지정 저장 프로시저 또는 스크립트입니다.|  
|**upd_scripting_proc**|**int**|UPDATE 문이 복제될 때 실행되는 등록된 사용자 지정 저장 프로시저 또는 스크립트입니다.|  
|**custom_script**|**nvarchar(2048)**|DDL 트리거 맨 끝에 실행되는 등록된 사용자 지정 저장 프로시저 또는 스크립트입니다.|  
|**fire_triggers_on_snapshot**|**bit**|복제된 트리거가 스냅샷이 적용될 때 실행될지 여부를 나타냅니다. 다음 값 중 하나일 수 있습니다.<br /><br /> **0** = 트리거가 실행 되지 않습니다.<br /><br /> **1** = 트리거가 실행 됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_helparticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sysarticles &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/sysarticles-transact-sql.md)  
  
  
