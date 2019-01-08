---
title: sysschemaarticles (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysschemaarticles_TSQL
- sysschemaarticles
dev_langs:
- TSQL
helpviewer_keywords:
- sysschemaarticles system table
ms.assetid: 67a1c039-c283-4a9c-bacc-b9b3973590c3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 39444e0eaf9a44f48fc86b5d7f4595d63d1e9823
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52822707"
---
# <a name="sysschemaarticles-transact-sql"></a>sysschemaarticles(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  트랜잭션 및 스냅숏 게시에 대한 스키마 전용 아티클을 추적합니다. 이 테이블은 게시 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|아티클 ID입니다.|  
|**creation_script**|**nvarchar(255)**|대상 테이블을 만드는 데 사용하는 아티클 스키마 스크립트의 경로 및 이름입니다.|  
|**description**|**nvarchar(255)**|아티클에 대한 설명 항목입니다.|  
|**dest_object**|**sysname**|아티클이 저장 프로시저, 뷰, UDF 등의 스키마 전용 아티클인 경우 구독 데이터베이스의 개체 이름입니다.|  
|**name**|**sysname**|게시 내 스키마 전용 아티클의 이름입니다.|  
|**objid**|**int**|아티클 기준 개체의 개체 식별자입니다. 프로시저, 뷰, 인덱싱된 뷰 UDF 등의 개체 식별자일 수 있습니다.|  
|**pubid**|**int**|게시의 ID입니다.|  
|**pre_creation_cmd**|**tinyint**|해당 아티클에 대한 스냅숏을 적용할 때 구독자에서 같은 이름의 기존 개체가 검색될 경우 시스템이 할 일을 지정합니다.<br /><br /> **0** = nothing입니다.<br /><br /> **1** = 대상 테이블을 삭제 합니다.<br /><br /> **2** = 대상 테이블을 삭제 합니다.<br /><br /> **3** = 대상 테이블을 잘라냅니다.|  
|**상태**|**int**|아티클의 상태를 표시하는 데 사용되는 비트맵입니다.|  
|**type**|**tinyint**|스키마 전용 아티클의 유형을 나타내는 값입니다.<br /><br /> **32** = 저장 프로시저입니다.<br /><br /> **64** = 뷰 또는 인덱싱된 뷰. <br /><br /> **96** = 집계 함수입니다.<br /><br /> **128** = 함수입니다.|  
|**schema_option**|**binary(8)**|지정한 아티클에 대한 스키마 생성 옵션의 비트 마스크입니다. 모든 CALL/MCALL/XCALL 구문에 대한 대상 데이터베이스 내의 저장 프로시저의 자동 생성을 지정합니다. 다음 값 중 하나 또는 둘 이상 값의 비트 논리 OR 결과입니다.<br /><br /> **0x00** = 스냅숏 에이전트를 사용 하 여 스크립팅을 *creation_script*합니다.<br /><br /> **0x01** = 개체 만들기 (CREATE TABLE, CREATE PROCEDURE 및 등)를 생성 합니다. 이 값은 저장 프로시저 아티클에 대한 기본값입니다.<br /><br /> **0x02** = 정의 된 경우 아티클 용 사용자 지정 저장된 프로시저를 생성 합니다.<br /><br /> **0x10** = 해당 클러스터형된 인덱스를 생성 합니다.<br /><br /> **0x20** = 사용자 정의 데이터 형식을 기본 데이터 형식으로 변환 합니다.<br /><br /> **0x40**= 해당 비클러스터형 인덱스 생성 합니다.<br /><br /> **0x80**= 기본 키에 대해 선언 된 참조 무결성 포함 합니다.<br /><br /> **0x73** = CREATE TABLE 문을 생성, 클러스터형 및 비클러스터형 인덱스를 생성, 사용자 정의 데이터 형식을 기본 데이터 형식 변환 및 구독자에 적용할 사용자 지정 저장된 프로시저 스크립트를 생성 합니다. 이 값은 저장 프로시저 아티클을 제외한 모든 아티클에 대한 기본값입니다.<br /><br /> **0x100**= 정의 된 경우 사용자 트리거를 테이블 아티클에서 복제 합니다.<br /><br /> **0x200**= 외래 키 제약 조건을 복제 합니다. 참조되는 테이블이 게시의 일부가 아니면 게시된 테이블의 모든 외래 키 제약 조건은 복제되지 않습니다.<br /><br /> **0x400**= check 제약 조건을 복제 합니다.<br /><br /> **0x800**= 기본값을 복제 합니다.<br /><br /> **0x1000**= 열 수준 데이터 정렬을 복제 합니다.<br /><br /> **0x2000**= 확장 된 게시 된 아티클 원본 개체와 연결 된 속성을 복제 합니다.<br /><br /> **0x4000**= 테이블 아티클에 대해 정의 된 경우 고유 키를 복제 합니다.<br /><br /> **0x8000**= ALTER TABLE 문을 사용 하 여 제약 조건으로 복제에 대 한 키 정보 및 테이블 아티클에 대 한 고유 키입니다.|  
|**dest_owner**|**sysname**|대상 데이터베이스에 있는 테이블의 소유자입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
