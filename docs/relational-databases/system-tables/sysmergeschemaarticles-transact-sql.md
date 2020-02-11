---
title: sysmergeschemaarticles (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergeschemaarticles_TSQL
- sysmergeschemaarticles
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeschemaarticles system table
ms.assetid: b5085979-2f76-48e1-bf3b-765a84003dd9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9446d03db98d7fa5181fb0217814cdd86c55de1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68029816"
---
# <a name="sysmergeschemaarticles-transact-sql"></a>sysmergeschemaarticles(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 복제에 대한 스키마 전용 아티클을 추적합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|병합 게시에서 스키마 전용 아티클의 이름입니다.|  
|**type**|**tinyint**|스키마 전용 아티클의 유형을 나타내며 다음 중 하나일 수 있습니다.<br /><br /> **0x20** = 저장 프로시저 스키마 전용 아티클입니다.<br /><br /> **0x40** = 뷰 스키마 전용 아티클 또는 인덱싱된 뷰 스키마 전용 아티클입니다.|  
|**objid**|**int**|아티클 기준 개체의 개체 식별자입니다. 프로시저, 뷰, 인덱싱된 뷰, 사용자 정의 함수 등의 개체 식별자일 수 있습니다.|  
|**artid**|**uniqueidentifier**|아티클 ID입니다.|  
|**한**|**nvarchar(255)**|아티클 설명입니다.|  
|**pre_creation_command**|**tinyint**|아티클이 구독 데이터베이스에서 만들어질 때 수행되는 기본 동작입니다.<br /><br /> **0 =** None-구독자에 테이블이 이미 있는 경우 아무 동작도 수행 되지 않습니다.<br /><br /> **1** = Drop-테이블을 다시 만들기 전에 테이블을 삭제 합니다.<br /><br /> **2** = delete-하위 집합 필터의 where 절을 기반으로 삭제를 실행 합니다.<br /><br /> **3** = Truncate- **2**와 동일 하지만 행 대신 페이지를 삭제 합니다. 단, WHERE 절은 사용하지 않습니다.|  
|**pubid**|**uniqueidentifier**|게시의 고유 식별자입니다.|  
|**업무**|**tinyint**|스키마 전용 아티클의 상태를 나타내며 다음 중 하나일 수 있습니다.<br /><br /> **1** = 동기화 됨-다음에 스냅숏 에이전트 실행 될 때 테이블을 게시 하는 초기 처리 스크립트가 실행 됩니다.<br /><br /> **2** = 활성-테이블을 게시 하는 초기 처리 스크립트가 실행 되었습니다.<br /><br /> **5** = New_inactive를 추가 합니다.<br /><br /> **6** = New_active 추가할 수 있습니다.|  
|**creation_script**|**nvarchar(255)**|대상 테이블을 만드는 데 사용하는 선택적 아티클 스키마 사전 작성 스크립트의 경로 및 이름입니다.|  
|**schema_option**|**binary (8)**|주어진 스키마 전용 아티클에 대한 스키마 생성 옵션의 비트맵으로 다음 값 중 하나 이상의 비트 논리 OR 결과일 수 있습니다.<br /><br /> **0x00** = 스냅숏 에이전트에서 스크립팅을 사용 하지 않도록 설정 하 고 제공 된 CreationScript를 사용 합니다.<br /><br /> **0x01** = 개체 만들기 (CREATE TABLE, 프로시저 만들기 등)를 생성 합니다.<br /><br /> **0x10** = 해당 클러스터형 인덱스를 생성 합니다.<br /><br /> **0x20** = 사용자 정의 데이터 형식을 기본 데이터 형식으로 변환 합니다.<br /><br /> **0x40** = 해당 하는 비클러스터형 인덱스를 생성 합니다.<br /><br /> **0x80** = 기본 키에 대해 선언 된 참조 무결성을 포함 합니다.<br /><br /> **0x100** = 정의 된 경우 테이블 아티클의 사용자 트리거를 복제 합니다.<br /><br /> **0x200** = foreign key 제약 조건을 복제 합니다. 참조되는 테이블이 게시되지 않는 경우 게시된 테이블의 모든 FOREIGN KEY 제약 조건은 복제되지 않습니다.<br /><br /> **0x400** = check 제약 조건을 복제 합니다.<br /><br /> **0x800** = 기본값을 복제 합니다.<br /><br /> **0x1000** = 열 수준 데이터 정렬을 복제 합니다.<br /><br /> **0x2000** = 게시 된 아티클 원본 개체와 연결 된 확장 속성을 복제 합니다.<br /><br /> **0x4000** = 테이블 아티클에 정의 된 경우 고유 키를 복제 합니다.<br /><br /> **0x8000** = ALTER table 문을 사용 하 여 테이블 아티클의 기본 키 및 고유 키를 제약 조건으로 복제 합니다.<br /><br /> **Schema_option**의 가능한 값에 대 한 자세한 내용은 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 참조 하세요.|  
|**destination_object**|**sysname**|구독 데이터베이스 내 대상 개체의 이름입니다. 이 값은 저장 프로시저, 뷰 및 UDF와 같은 스키마 전용 아티클에만 적용합니다.|  
|**destination_owner**|**sysname**|**Dbo**가 아닌 경우 구독 데이터베이스에 있는 개체의 소유자입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
