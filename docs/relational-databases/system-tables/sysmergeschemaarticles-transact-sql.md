---
title: sysmergeschemaarticles (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysmergeschemaarticles_TSQL
- sysmergeschemaarticles
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeschemaarticles system table
ms.assetid: b5085979-2f76-48e1-bf3b-765a84003dd9
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 13a3104b8f457cf4c9d223630739e3cf6eb76ee8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sysmergeschemaarticles-transact-sql"></a>sysmergeschemaarticles(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 복제에 대한 스키마 전용 아티클을 추적합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|병합 게시에서 스키마 전용 아티클의 이름입니다.|  
|**유형**|**tinyint**|스키마 전용 아티클의 유형을 나타내며 다음 중 하나일 수 있습니다.<br /><br /> **0x20** = 저장 프로시저 스키마 전용 아티클입니다.<br /><br /> **0x40** = 뷰 스키마 전용 아티클 또는 인덱싱된 뷰 스키마 전용 아티클입니다.|  
|**objid**|**int**|아티클 기준 개체의 개체 식별자입니다. 프로시저, 뷰, 인덱싱된 뷰, 사용자 정의 함수 등의 개체 식별자일 수 있습니다.|  
|**artid**|**uniqueidentifier**|아티클 ID입니다.|  
|**설명**|**nvarchar(255)**|아티클에 대한 설명입니다.|  
|**pre_creation_command**|**tinyint**|아티클이 구독 데이터베이스에서 만들어질 때 수행되는 기본 동작입니다.<br /><br /> **0 =** none-구독자에서 테이블이 이미 있는 경우 아무 작업도 수행 합니다.<br /><br /> **1** = drop-테이블을 다시 만들기 전에 삭제 합니다.<br /><br /> **2** = delete-하위 집합 필터의 WHERE 절을 기반으로 하 여 삭제를 실행 합니다.<br /><br /> **3** = Truncate-동일 **2**, 하지만 행 대신 페이지를 삭제 합니다. 단, WHERE 절은 사용하지 않습니다.|  
|**pubid**|**uniqueidentifier**|게시의 고유 식별자입니다.|  
|**상태**|**tinyint**|스키마 전용 아티클의 상태를 나타내며 다음 중 하나일 수 있습니다.<br /><br /> **1** = Unsynced-다음에 스냅숏 에이전트가 실행 되는 테이블 실행을 게시 하는 초기 처리 스크립트가 있습니다.<br /><br /> **2** = active-테이블을 게시 하는 초기 처리 스크립트가 실행 되었습니다.<br /><br /> **5** = New_inactive-추가 될 합니다.<br /><br /> **6** = New_active-추가 될 합니다.|  
|**creation_script**|**nvarchar(255)**|대상 테이블을 만드는 데 사용하는 선택적 아티클 스키마 사전 작성 스크립트의 경로 및 이름입니다.|  
|**schema_option**|**binary (8)**|주어진 스키마 전용 아티클에 대한 스키마 생성 옵션의 비트맵으로 다음 값 중 하나 이상의 비트 논리 OR 결과일 수 있습니다.<br /><br /> **0x00** = 스냅숏 에이전트에서 한 스크립팅을 비활성화 하 고 제공 된 creationscript 합니다.<br /><br /> **0x01** = 개체 만들기 (CREATE TABLE, CREATE PROCEDURE 등)를 생성 합니다.<br /><br /> **0x10** = 해당 클러스터형된 인덱스를 생성 합니다.<br /><br /> **0x20** = 사용자 정의 데이터 형식을 기본 데이터 형식으로 변환 합니다.<br /><br /> **0x40** = 해당 비클러스터형 인덱스 생성 또는 인덱스입니다.<br /><br /> **0x80** = 선언 된 참조 무결성 기본 키에 포함 합니다.<br /><br /> **0x100** 복제 사용자 트리거를 테이블 아티클에서 = 정의 된 경우.<br /><br /> **0x200** = foreign key 제약 조건을 복제 합니다. 참조되는 테이블이 게시되지 않는 경우 게시된 테이블의 모든 FOREIGN KEY 제약 조건은 복제되지 않습니다.<br /><br /> **0x400** = check 제약 조건을 복제 합니다.<br /><br /> **0x800** = 기본값을 복제 합니다.<br /><br /> **0x1000** = 열 수준 데이터 정렬을 복제 합니다.<br /><br /> **0x2000** = 게시 된 아티클 원본 개체와 연관 된 확장 속성 복제 합니다.<br /><br /> **0x4000** = 테이블 아티클에 대해 정의 된 경우 고유 키를 복제 합니다.<br /><br /> **0x8000** = 기본 키 및 테이블에 고유 키 문서 ALTER TABLE 문을 사용 하 여 제약 조건으로 복제 합니다.<br /><br /> 가능한 값에 대 한 자세한 내용은 **schema_option**, 참조 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)합니다.|  
|**destination_object**|**sysname**|구독 데이터베이스 내 대상 개체의 이름입니다. 이 값은 저장 프로시저, 뷰 및 UDF와 같은 스키마 전용 아티클에만 적용합니다.|  
|**destination_owner**|**sysname**|없는 경우 구독 데이터베이스에서 개체의 소유자 **dbo**합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40; Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
