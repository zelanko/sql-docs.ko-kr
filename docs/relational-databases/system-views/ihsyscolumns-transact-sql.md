---
title: IHsyscolumns (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 74116af7883c4b9a3f27c2afed88d16c993198ce
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52747888"
---
# <a name="ihsyscolumns-transact-sql"></a>IHsyscolumns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **IHsyscolumns** 뷰는에서-SQL Server 이외 게시자의 게시 된 아티클에 대 한 열 정보를 표시 합니다. 이 보기는 distributiondatabase에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|열 또는 프로시저 매개 변수의 이름입니다.|  
|**id**|**int**|이 열이 속한 테이블의 개체 ID 또는 이 매개 변수와 연관된 저장 프로시저의 ID입니다.|  
|**xtype**|**tinyint**|물리적 저장소 유형 [sys.systypes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)합니다.|  
|**typestat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**tinyint**|확장 사용자 정의 데이터 형식의 ID입니다.|  
|**length**|**bigint**|최대 물리적 저장 길이 [sys.systypes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)합니다.|  
|**xprec**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xscale**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colid**|**int**|열 또는 매개 변수의 ID입니다.|  
|**xoffset**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**bitpos**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colstat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**cdefault**|**int**|이 열에 대한 기본값의 ID입니다.|  
|**domain**|**int**|이 열에 대한 CHECK 제약 조건 또는 규칙의 ID입니다.|  
|**number**|**int**|프로시저를 그룹화 하는 경우 하위 프로시저 번호 (**0** 프로시저가 아닌 항목에 대 한).|  
|**colorder**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**autoval**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**offset**|**int**|이 열이 나타나는 행으로의 오프셋입니다.|  
|**collationid**|**int**|열의 데이터 정렬 ID입니다. NULL이 아닌 문자에 대 한 열 기반합니다.|  
|**language**|**int**|열에 대한 언어 식별자입니다.|  
|**상태**|**int**|열 또는 매개 변수의 속성을 설명하는 데 사용하는 비트맵입니다.<br /><br /> **0x08** = 열 null 값을 허용 합니다.<br /><br /> **0x10** ANSI 패딩 = 때 적용 된 **varchar** 하거나 **varbinary** 열이 추가 되었습니다. 에 대 한 후행 공백을 유지 하며 **varchar** 후행 0을 유지 하 고 **varbinary** 열입니다.<br /><br /> **0x40** = 매개 변수가 출력 매개 변수입니다.<br /><br /> **0x80** = 열이 id 열입니다.|  
|**type**|**int**|물리적 저장소 유형 [sys.systypes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)합니다.|  
|**usertype**|**tinyint**|사용자 정의 데이터 형식의 ID [sys.systypes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)합니다.|  
|**printfmt**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**int**|이 열의 전체 자릿수 수준입니다.|  
|**scale**|**int**|이 열의 소수 자릿수입니다.|  
|**iscomputed**|**int**|열이 계산되었는지 표시하는 플래그입니다.<br /><br /> **0** = 조합이 있습니다.<br /><br /> **1** = 계산 합니다.|  
|**isoutparam**|**int**|프로시저 매개 변수가 출력 매개 변수인지 여부를 나타냅니다.<br /><br /> **1** = true입니다.<br /><br /> **0** = false.|  
|**isnullable**|**int**|열에 Null 값이 허용되는지 여부를 나타냅니다.<br /><br /> **1** = true입니다.<br /><br /> **0** = false.|  
|**collation**|**int**|열의 데이터 정렬 이름입니다. NULL이 아닌 문자에 대 한 열 기반합니다.|  
|**tdscollation**|**int**|TDS(tabular data stream)가 반환한 열의 데이터 정렬 이름입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
