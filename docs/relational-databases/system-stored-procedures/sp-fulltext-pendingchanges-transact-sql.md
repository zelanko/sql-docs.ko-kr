---
title: sp_fulltext_pendingchanges (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_pendingchanges_TSQL
- sp_fulltext_pendingchanges
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_pendingchanges
ms.assetid: fee042fe-4781-4a33-a01b-d98fb5629f1b
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d4d8cbd7082a3ec8d19ccc6df7212a70b101e6b8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68124224"
---
# <a name="sp_fulltext_pendingchanges-transact-sql"></a>sp_fulltext_pendingchanges(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  변경 내용 추적을 사용하는 지정된 테이블에 대해 보류 중인 삽입, 업데이트, 삭제 등의 처리되지 않은 변경 내용을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_fulltext_pendingchanges table_id  
```  
  
## <a name="arguments"></a>인수  
 *table_id*  
 테이블 ID입니다. 테이블이 전체 텍스트 인덱싱된 테이블이 아니거나 변경 내용 추적을 사용하고 있지 않으면 오류가 반환됩니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**Key**|*|지정한 테이블의 전체 텍스트 키 값입니다.|  
|**DocId**|**bigint**|키 값에 해당하는 내부 문서 ID(DocId) 열입니다.|  
|**상태**|**int**|0 = 행이 전체 텍스트 인덱스에서 제거됩니다.<br /><br /> 1 = 행이 전체 텍스트 인덱싱됩니다.<br /><br /> 2 = 행이 최신 상태입니다.<br /><br /> -1 = 행이 과도기적(일괄 처리되었지만 커밋되지는 않음) 상태 또는 오류 상태에 있습니다.|  
|**DocState**|**tinyint**|내부 문서 ID(DocId) 맵 상태 열의 원시 덤프입니다.|  
  
 <sup>* Key의 데이터 형식은 기본 테이블의 전체 텍스트 키 열의 데이터 형식과 동일합니다.</sup>  
  
## <a name="permissions"></a>사용 권한  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="remarks"></a>설명  
 처리할 변경 내용이 없으면 빈 행 집합이 반환됩니다.  
  
 전체 텍스트 검색 쿼리는 **Status** 값이 0인 행을 반환하지 않습니다. 이는 이러한 행이 기본 테이블에서 삭제되었고 전체 텍스트 인덱스에서도 삭제 대기 중이기 때문입니다.  
  
 특정 테이블에 대해 보류 중인 변경 내용이 얼마나 되는지 확인하려면 OBJECTPROPERTYEX 함수의 **TableFullTextPendingChanges** 속성을 사용하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;전체 텍스트 검색 및 의미 체계 검색 저장 프로시저](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [OBJECTPROPERTYEX&#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)  
  
  
