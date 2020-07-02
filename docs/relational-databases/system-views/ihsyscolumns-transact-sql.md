---
title: IHsyscolumns (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHsyscolumns
- IHsyscolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHsyscolumns view
ms.assetid: 263452f1-9708-48f0-9536-402a89e7f5bf
author: stevestein
ms.author: sstein
ms.openlocfilehash: a965be50e45300aeca3ba158251c665e8204a6f2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85736673"
---
# <a name="ihsyscolumns-transact-sql"></a>IHsyscolumns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  **IHsyscolumns** 뷰는 SQL Server 되지 않은 게시자에서 게시 된 아티클에 대 한 열 정보를 제공 합니다. 이 보기는 distributiondatabase에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|열 또는 프로시저 매개 변수의 이름입니다.|  
|**id**|**int**|이 열이 속한 테이블의 개체 ID 또는 이 매개 변수와 연관된 저장 프로시저의 ID입니다.|  
|**xtype**|**tinyint**|[Transact-sql&#41;&#40;sys.sys형식의 ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)실제 저장소 유형입니다.|  
|**typestat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**tinyint**|확장 사용자 정의 데이터 형식의 ID입니다.|  
|**length**|**bigint**|[Transact-sql&#41;&#40;sys.sys형식 ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)에서의 최대 실제 저장소 길이입니다.|  
|**xprec**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xscale**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colid**|**int**|열 또는 매개 변수의 ID입니다.|  
|**xoffset**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**bitpos**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**쓰이는**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colstat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**cdefault**|**int**|이 열에 대한 기본값의 ID입니다.|  
|**도메인**|**int**|이 열에 대한 CHECK 제약 조건 또는 규칙의 ID입니다.|  
|**number**|**int**|프로시저가 그룹화 될 때의 하위 절차 번호입니다. 프로시저가 아닌 항목의 경우**0** 입니다.|  
|**colorder**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**autoval**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**offset**|**int**|이 열이 나타나는 행으로의 오프셋입니다.|  
|**collationid**|**int**|열의 데이터 정렬 ID입니다. 문자 기반이 아닌 열의 경우 NULL입니다.|  
|**language**|**int**|열에 대한 언어 식별자입니다.|  
|**status**|**int**|열 또는 매개 변수의 속성을 설명하는 데 사용하는 비트맵입니다.<br /><br /> **0x08** = 열에 null 값을 사용할 수 있습니다.<br /><br /> **0x10** = **varchar** 또는 **varbinary** 열이 추가 될 때 ANSI 안쪽 여백이 적용 되었습니다. **Varchar** 열에 대 한 후행 공백은 유지 되 고 뒤에 오는 0은 **varbinary** 열에 대해 유지 됩니다.<br /><br /> **0x40** = 매개 변수가 OUTPUT 매개 변수입니다.<br /><br /> **0x80** = 열이 id 열입니다.|  
|**type**|**int**|[Transact-sql&#41;&#40;sys.sys형식의 ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)실제 저장소 유형입니다.|  
|**usertype**|**tinyint**|[Transact-sql&#41;&#40;sys.sys형식 ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)에서 사용자 정의 데이터 형식의 ID입니다.|  
|**printfmt**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**int**|이 열의 전체 자릿수 수준입니다.|  
|**scale**|**int**|이 열의 소수 자릿수입니다.|  
|**iscomputed**|**int**|열이 계산되었는지 표시하는 플래그입니다.<br /><br /> **0** = 연결한 조합이.<br /><br /> **1** = 계산됨|  
|**isoutparam**|**int**|프로시저 매개 변수가 출력 매개 변수인지 여부를 나타냅니다.<br /><br /> **1** = True입니다.<br /><br /> **0** = False.|  
|**isnullable**|**int**|열에 Null 값이 허용되는지 여부를 나타냅니다.<br /><br /> **1** = True입니다.<br /><br /> **0** = False.|  
|**부씩**|**int**|열의 데이터 정렬 이름입니다. 문자 기반이 아닌 열의 경우 NULL입니다.|  
|**tdscollation**|**int**|TDS(tabular data stream)가 반환한 열의 데이터 정렬 이름입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;복제 뷰](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
