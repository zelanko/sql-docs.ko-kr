---
title: sys.sysobjects (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sysobjects_TSQL
- sysobjects
- sysobjects_TSQL
- sys.sysobjects
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysobjects compatibility view
- sysobjects system table
ms.assetid: 44fdc387-67b0-4139-8bf5-ed26cf640cd1
caps.latest.revision: 41
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4b9013273782ff103d0cb254ed6bec4b80461443
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="syssysobjects-transact-sql"></a>sys.sysobjects(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  데이터베이스에서 만들어진 각 개체(제약 조건, 기본값, 로그, 규칙, 저장 프로시저)당 한 개의 행을 포함합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|name|**sysname**|개체 이름|  
|id|**int**|개체 ID|  
|xtype|**char(2)**|개체 유형입니다. 다음 개체 유형 중 하나일 수 있습니다.<br /><br /> AF = 집계 함수(CLR)<br /><br /> C = CHECK 제약 조건<br /><br /> D = 기본값 또는 DEFAULT 제약 조건<br /><br /> F = FOREIGN KEY 제약 조건<br /><br /> L = 로그<br /><br /> FN = 스칼라 함수<br /><br /> FS = 어셈블리(CLR) 스칼라 함수<br /><br /> FT = 어셈블리(CLR) 테이블 반환 함수<br /><br /> IF = 인라인 테이블 함수<br /><br /> IT = 내부 테이블<br /><br /> P = 저장 프로시저<br /><br /> PC = 어셈블리(CLR) 저장 프로시저<br /><br /> PK = PRIMARY KEY 제약 조건(K 유형)<br /><br /> RF = 복제 필터 저장 프로시저<br /><br /> S = 시스템 테이블<br /><br /> SN = 동의어<br /><br /> SQ = 서비스 큐<br /><br /> TA = 어셈블리(CLR) DML 트리거<br /><br /> TF = 테이블 함수<br /><br /> TR = SQL DML 트리거<br /><br /> TT = 테이블 유형<br /><br /> U = 사용자 테이블<br /><br /> UQ = UNIQUE 제약 조건(K 유형)<br /><br /> V = 뷰<br /><br /> X = 확장 저장 프로시저|  
|uid|**smallint**|개체 소유자의 스키마 ID입니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업그레이드한 데이터베이스의 경우 스키마 ID는 소유자의 사용자 ID와 동일합니다. 사용자 및 역할 수가 32,767을 초과하는 경우 오버플로되거나 NULL을 반환합니다.<br /><br /> **\*\* 중요 한 \* \***  다음 중 하나를 사용 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 해야 DDL 문는 [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 카탈로그 뷰 sys.sysobjects 대신 합니다.<br /><br /> 만들 &AMP;#124; ALTER &AMP;#124; 놓기 사용자<br /><br /> 만들 &AMP;#124; ALTER &AMP;#124; 놓기 역할<br /><br /> 만들 &AMP;#124; ALTER &AMP;#124; 놓기 응용 프로그램 역할<br /><br /> CREATE SCHEMA<br /><br /> ALTER AUTHORIZATION ON OBJECT|  
|정보|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|상태|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|base_schema_ver|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|replinfo|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|parent_obj|**int**|부모 개체의 개체 ID입니다. 예를 들어 트리거 또는 제약 조건인 경우 테이블의 ID입니다.|  
|crdate|**datetime**|개체를 만든 날짜입니다.|  
|ftcatid|**smallint**|전체 텍스트 인덱싱을 위해 등록된 모든 사용자 테이블의 경우 전체 텍스트 카탈로그 식별자이며, 등록되지 않은 모든 사용자 테이블의 경우 0입니다.|  
|schema_ver|**int**|테이블의 스키마가 변경될 때마다 증가하는 버전 번호입니다. 항상 0을 반환합니다.|  
|stats_schema_ver|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|유형|**char(2)**|개체 유형입니다. 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> AF = 집계 함수(CLR)<br /><br /> C = CHECK 제약 조건<br /><br /> D = 기본값 또는 DEFAULT 제약 조건<br /><br /> F = FOREIGN KEY 제약 조건<br /><br /> FN = 스칼라 함수<br /><br /> FS = 어셈블리(CLR) 스칼라 함수<br /><br /> FT = 어셈블리(CLR) 테이블 반환 함수 IF = 인라인 테이블 함수<br /><br /> IT = 내부 테이블<br /><br /> K = PRIMARY KEY 또는 UNIQUE 제약 조건<br /><br /> L = 로그<br /><br /> P = 저장 프로시저<br /><br /> PC = 어셈블리(CLR) 저장 프로시저<br /><br /> R = 규칙<br /><br /> RF = 복제 필터 저장 프로시저<br /><br /> S = 시스템 테이블<br /><br /> SN = 동의어<br /><br /> SQ = 서비스 큐<br /><br /> TA = 어셈블리(CLR) DML 트리거<br /><br /> TF = 테이블 함수<br /><br /> TR = SQL DML 트리거<br /><br /> TT = 테이블 유형<br /><br /> U = 사용자 테이블<br /><br /> V = 뷰<br /><br /> X = 확장 저장 프로시저|  
|userstat|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|sysstat|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|indexdel|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|refdate|**datetime**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|version|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|deltrig|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|instrig|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|updtrig|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|seltrig|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|category|**int**|게시, 제약 조건 및 ID에 사용됩니다.|  
|캐시|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
