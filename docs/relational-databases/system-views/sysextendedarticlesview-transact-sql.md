---
title: sysextendedarticlesview (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysextendedarticlesview_TSQL
- sysextendedarticlesview
dev_langs:
- TSQL
helpviewer_keywords:
- sysextendedarticlesview view
ms.assetid: 8bdd22f7-c268-49b6-820c-3fe603feb128
author: stevestein
ms.author: sstein
ms.openlocfilehash: c273b33c0bdecd86eb9ef21f086860bbe3c569b5
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881258"
---
# <a name="sysextendedarticlesview-transact-sql"></a>sysextendedarticlesview(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Sysextendedarticlesview** 뷰는 게시 된 아티클에 대 한 정보를 제공 합니다. 이 뷰는 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|아티클에 대해 고유한 ID를 제공하는 ID 열입니다.|  
|**creation_script**|**nvarchar(255)**|아티클에 대한 스키마 생성 스크립트입니다.|  
|**del_cmd**|**nvarchar(255)**|DELETE 시 실행할 명령입니다. 그렇지 않으면 로그에서 만들어집니다.|  
|**한**|**nvarchar(255)**|아티클에 대한 설명 항목입니다.|  
|**dest_table**|**nvarchar(128)**|대상 테이블의 이름입니다.|  
|**필터가**|**int**|수평 분할에 사용하는 저장 프로시저의 개체 식별자입니다.|  
|**filter_clause**|**ntext**|행 필터링에 사용하는 아티클의 WHERE 절입니다.|  
|**ins_cmd**|**nvarchar(255)**|INSERT 시 실행할 명령입니다.|  
|**name**|**nvarchar(128)**|아티클과 관련된 이름이며 게시 내에서 고유합니다.|  
|**objid**|**int**|게시된 테이블 개체 ID입니다.|  
|**pubid**|**int**|아티클이 속한 게시의 ID입니다.|  
|**pre_creation_cmd**|**tinyint**|DROP TABLE, DELETE TABLE 또는 TRUNCATE에 대한 사전 생성 명령입니다.<br /><br /> **0** = 없음<br /><br /> **1** = 삭제<br /><br /> **2** = 삭제<br /><br /> **3** = 자름|  
|**status**|**int**|아티클 옵션 및 상태의 비트 마스크이며 다음 값 중 하나 이상에 대한 논리 비트 OR 연산의 결과일 수 있습니다.<br /><br /> **1** = 아티클이 활성 상태입니다.<br /><br /> **8** = INSERT 문에 열 이름을 포함 합니다.<br /><br /> **16** = 매개 변수가 있는 문을 사용 합니다.<br /><br /> **24** = INSERT 문에 열 이름을 포함 하 고 매개 변수가 있는 문을 사용 합니다.<br /><br /> 예를 들어 매개 변수가 있는 문을 사용하는 활성 아티클은 이 열의 값이 17이 되며 값 0은 아티클이 비활성 상태이고 추가 속성이 정의되지 않았음을 의미합니다.|  
|**sync_objid**|**int**|아티클 정의를 나타내는 테이블 또는 뷰의 ID입니다.|  
|**type**|**tinyint**|아티클의 유형입니다.<br /><br /> **1** = 로그 기반 아티클입니다.<br /><br /> **3** = 수동 필터가 있는 로그 기반 아티클입니다.<br /><br /> **5** = 수동 뷰가 있는 로그 기반 아티클입니다.<br /><br /> **7** = 수동 필터 및 수동 뷰가 있는 로그 기반 아티클입니다.|  
|**upd_cmd**|**nvarchar(255)**|UPDATE 시 실행할 명령입니다. 그렇지 않으면 로그에서 만들어집니다.|  
|**schema_option**|**binary**|스냅샷에 스크립팅할 게시된 개체의 속성을 나타냅니다. 지원 되는 스키마 옵션 목록은 [sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)를 참조 하세요.|  
|**dest_owner**|**nvarchar(128)**|대상 데이터베이스에 있는 테이블의 소유자입니다.|  
|**ins_scripting_proc**|**int**|INSERT 문이 복제될 때 실행되는 사용자 지정 저장 프로시저 또는 스크립트의 개체 식별자입니다.|  
|**del_scripting_proc**|**int**|DELETE 문이 복제될 때 실행되는 사용자 지정 저장 프로시저 또는 스크립트의 개체 식별자입니다.|  
|**upd_scripting_proc**|**int**|UPDATE 문이 복제될 때 실행되는 사용자 지정 저장 프로시저 또는 스크립트의 개체 식별자입니다.|  
|**custom_script**|**int**|DDD 트리거 완료 시 실행되는 사용자 지정 스크립트 또는 프로시저의 개체 식별자입니다.|  
|**fire_triggers_on_snapshot**|**int**|복제된 트리거가 스냅샷이 적용될 때 실행될지 여부를 나타냅니다. 다음 값 중 하나일 수 있습니다.<br /><br /> **0** = 트리거가 실행 되지 않습니다.<br /><br /> **1** = 트리거가 실행 됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;복제 뷰](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Transact-sql&#41;sp_addarticle &#40;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [Transact-sql&#41;sp_changearticle &#40;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [Transact-sql&#41;sp_helparticle &#40;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sysarticles &#40;Transact-sql&#41;](../../relational-databases/system-tables/sysarticles-transact-sql.md)  
  
  
