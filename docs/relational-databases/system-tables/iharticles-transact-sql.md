---
title: IHarticles (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
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
- IHarticles
- IHarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHarticles system table
ms.assetid: 773ef9b7-c993-4629-9516-70c47b9dcf65
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 53542af40c2d5c477b9fbd2ff21467ffd6af69e7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33003220"
---
# <a name="iharticles-transact-sql"></a>IHarticles(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHarticles** 시스템 테이블에서-SQL Server 이외 게시자는 현재 배포자를 사용 하 여 복제 되는 각 아티클당 하나의 행을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
## <a name="definition"></a>정의  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|아티클에 대해 고유한 ID를 제공하는 ID 열입니다.|  
|**name**|**sysname**|아티클과 관련된 이름이며 게시 내에서 고유합니다.|  
|**publication_id**|**smallint**|아티클이 속한 게시의 ID입니다.|  
|**table_id**|**int**|게시 되는 테이블의 ID [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md)합니다.|  
|**publisher_id**|**smallint**|비 SQL Server 게시자의 ID입니다.|  
|**creation_script**|**nvarchar(255)**|아티클에 대한 스키마 스크립트입니다.|  
|**del_cmd**|**nvarchar(255)**|삭제를 복제할 때 테이블 아티클에서 사용되는 복제 명령 유형입니다. 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.|  
|**filter**|**int**|이 열은 사용 되지 않으며 하려는 경우에 포함 되어는 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) 볼 수는 **IHarticles** 테이블와 호환 되는 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) SQL Server 기사 (에 사용 되는 보기 [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**filter_clause**|**ntext**|아티클의 WHERE 절로서 행 필터링에 사용되며 SQL 게시자가 아닌 게시자가 해석할 수 있는 표준 Transact-SQL로 작성됩니다. |  
|**ins_cmd**|**nvarchar(255)**|삽입을 복제할 때 테이블 아티클에서 사용되는 복제 명령 유형입니다. 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.|  
|**pre_creation_cmd**|**tinyint**|같은 이름을 가진 개체가 이미 구독자에 존재하는 경우 초기 스냅숏을 적용하기 전에 실행하는 명령입니다.<br /><br /> **0** = none-명령을 실행 되지 않습니다.<br /><br /> **1** = DROP-대상 테이블을 삭제 합니다.<br /><br /> **2** = DELETE-대상 테이블에서 데이터를 삭제 합니다.<br /><br /> **3** = TRUNCATE-대상 테이블을 자릅니다.|  
|**상태**|**tinyint**|아티클 옵션 및 상태의 비트 마스크이며 다음 값 중 하나 이상에 대한 논리 비트 OR 연산의 결과일 수 있습니다.<br /><br /> **0** = 추가 속성이 없습니다.<br /><br /> **1** = 활성 합니다.<br /><br /> **8** = INSERT 문에 열 이름을 포함 합니다.<br /><br /> **16** = 문을 매개 변수화 사용 합니다.<br /><br /> 예를 들어 매개 변수가 있는 문을 사용하는 활성 아티클은 이 열의 값이 17이 되며 값 0은 아티클이 비활성 상태이고 추가 속성이 정의되지 않았음을 의미합니다.|  
|**type**|**tinyint**|아티클의 유형입니다.<br /><br /> **1** = 로그 기반 아티클입니다.|  
|**upd_cmd**|**nvarchar(255)**|업데이트를 복제할 때 테이블 아티클에서 사용되는 복제 명령 유형입니다. 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.|  
|**schema_option**|**binary(8)**|지정된 아티클에 대한 스키마 생성 옵션의 비트맵으로 다음 값 중 하나 이상의 비트 논리 OR 결과일 수 있습니다.<br /><br /> **0x00** = 스냅숏 에이전트에서 한 스크립팅을 비활성화 하 고 제공 된 creationscript 합니다.<br /><br /> **0x01** = 개체 만들기 (CREATE TABLE, CREATE PROCEDURE 등)를 생성 합니다.<br /><br /> **0x10** = 해당 클러스터형된 인덱스를 생성 합니다.<br /><br /> **0x40** = 해당 비클러스터형 인덱스를 생성 합니다.<br /><br /> **0x80** = 선언 된 참조 무결성 기본 키에 포함 합니다.<br /><br /> **0x1000** = 열 수준 데이터 정렬을 복제 합니다. 참고:이 옵션은 대/소문자 구분 비교를 사용 하려면 Oracle 게시자에 대해 기본적으로 설정 됩니다.<br /><br /> **0x4000** = 테이블 아티클에 대해 정의 된 경우 고유 키를 복제 합니다.<br /><br /> **0x8000** = 기본 키 및 테이블에 고유 키 문서 ALTER TABLE 문을 사용 하 여 제약 조건으로 복제 합니다.|  
|**dest_owner**|**sysname**|대상 데이터베이스에 있는 테이블의 소유자입니다.|  
|**dest_table**|**sysname**|대상 테이블의 이름입니다.|  
|**tablespace_name**|**nvarchar(255)**|아티클에 대한 로깅 테이블에서 사용하는 테이블스페이스를 식별합니다.|  
|**objid**|**int**|이 열은 사용 되지 않으며 하려는 경우에 포함 되어는 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) 볼 수는 **IHarticles** 테이블와 호환 되는 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) SQL Server 기사 (에 사용 되는 보기 [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**sync_objid**|**int**|이 열은 사용 되지 않으며 하려는 경우에 포함 되어는 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) 볼 수는 **IHarticles** 테이블와 호환 되는 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) SQL Server 기사 (에 사용 되는 보기 [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**설명**|**nvarchar(255)**|아티클에 대한 설명 항목입니다.|  
|**publisher_status**|**int**|게시 된 아티클을 정의 하는 뷰를 호출 하 여 정의한 경우를 나타내는 데 [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)합니다.<br /><br /> **0** = [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 가 호출 되었습니다.<br /><br /> **1** = [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 호출 되지 않았습니다.|  
|**article_view_owner**|**nvarchar(255)**|로그 판독기 에이전트에서 사용하는 게시자에 있는 동기화 개체의 소유자입니다.|  
|**article_view**|**nvarchar(255)**|로그 판독기 에이전트에서 사용하는 게시자에 있는 동기화 개체입니다.|  
|**ins_scripting_proc**|**int**|이 열은 사용 되지 않으며 하려는 경우에 포함 되어는 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) 볼 수는 **IHarticles** 테이블와 호환 되는 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) SQL Server 기사 (에 사용 되는 보기 [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**del_scripting_proc**|**int**|이 열은 사용 되지 않으며 하려는 경우에 포함 되어는 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) 볼 수는 **IHarticles** 테이블와 호환 되는 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) SQL Server 기사 (에 사용 되는 보기 [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**upd_scripting_proc**|**int**|이 열은 사용 되지 않으며 하려는 경우에 포함 되어는 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) 볼 수는 **IHarticles** 테이블와 호환 되는 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) SQL Server 기사 (에 사용 되는 보기 [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**custom_script**|**int**|이 열은 사용 되지 않으며 하려는 경우에 포함 되어는 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) 볼 수는 **IHarticles** 테이블와 호환 되는 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) SQL Server 기사 (에 사용 되는 보기 [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**fire_triggers_on_snapshot**|**bit**|이 열은 사용 되지 않으며 하려는 경우에 포함 되어는 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) 볼 수는 **IHarticles** 테이블와 호환 되는 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) SQL Server 기사 (에 사용 되는 보기 [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**instance_id**|**int**|게시된 테이블에 대한 아티클 로그의 현재 인스턴스를 식별합니다.|  
|**use_default_datatypes**|**bit**|문서 기본 데이터 형식 매핑을;를 사용 하는지 여부를 나타냅니다. 값이 **1** 기본 데이터 형식 매핑을 사용 됨을 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)  
  
  
