---
title: sys.fn_check_object_signatures (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.fn_check_object_signatures_TSQL
- fn_check_object_signatures_TSQL
- fn_check_object_signatures
- sys.fn_check_object_signatures
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_check_object_signatures function
ms.assetid: 47509566-d3d7-46a9-89c1-91b4895d56b9
caps.latest.revision: 15
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= aps-pdw-2016 || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4d516472fb5ccec63498d7ab13401e2df1f4bf10
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38015155"
---
# <a name="sysfncheckobjectsignatures-transact-sql"></a>sys.fn_check_object_signatures(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  모든 서명 가능한 개체의 목록을 반환하고 개체가 지정된 인증서 또는 비대칭 키로 서명되었는지를 나타냅니다. 개체가 지정된 인증서 또는 비대칭 키로 서명된 경우 개체의 서명이 유효한지 여부도 반환됩니다.  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
fn_ check_object_signatures (   
    { '@class' } , { @thumbprint }   
  )   
```  
  
## <a name="arguments"></a>인수  
 {0} ' @*클래스*'}  
 제공되는 지문의 유형을 식별합니다.  
  
-   '인증서'  
  
-   '비대칭 키'  
  
 @*클래스* 됩니다 **sysname**합니다.  
  
 {@*지문을* }  
 키 암호화에 사용되는 인증서의 SHA-1 해시이거나 비대칭 키의 GUID입니다. @*지문을* 됩니다 **varbinary(20)** 합니다.  
  
## <a name="tables-returned"></a>반환된 테이블  
 다음 표에서 열을 나열 하는 **fn_check_object_signatures** 반환 합니다.  
  
|Column|형식|Description|  
|------------|----------|-----------------|  
|유형|**nvarchar(120)**|유형 설명 또는 어셈블리를 반환합니다.|  
|entity_id|**int**|평가 중인 개체의 개체 ID를 반환합니다.|  
|is_signed|**int**|개체가 제공된 지문으로 서명되지 않은 경우 0을 반환합니다. 개체가 제공된 지문으로 서명된 경우 1을 반환합니다.|  
|is_signature_valid|**int**|is_signed 값이 1일 때 서명이 유효하지 않으면 0을 반환하고, 서명이 유효하면 1을 반환합니다.<br /><br /> is_signed 값이 0일 때는 항상 0을 반환합니다.|  
  
## <a name="remarks"></a>Remarks  
 사용 하 여 **fn_check_object_signatures** 악의적인 사용자가 개체를 사용 하 여 훼손 되지 않았음을 확인 합니다.  
  
## <a name="permissions"></a>사용 권한  
 인증서 또는 비대칭 키에 대한 VIEW DEFINITION이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `master` 데이터베이스에 대한 스키마 서명 인증서를 찾고, 개체가 해당 스키마 서명 인증서로 서명되고 유효한 서명을 가진 경우 `is_signed` 값 1과 `is_signature_valid` 값 1을 반환합니다.  
  
```  
USE master;  
-- Declare a variable to hold the thumbprint.  
DECLARE @thumbprint varbinary(20) ;  
-- Populate the thumbprint variable with the master database schema signing certificate.  
SELECT @thumbprint = thumbprint   
FROM sys.certificates   
WHERE name LIKE '%SchemaSigningCertificate%' ;  
-- Evaluates the objects signed by the schema signing certificate  
SELECT type, entity_id, OBJECT_NAME(entity_id) AS [object name], is_signed, is_signature_valid  
FROM sys.fn_check_object_signatures ('certificate', @thumbprint) ;  
GO  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [IS_OBJECTSIGNED &#40;TRANSACT-SQL&#41;](../../t-sql/functions/is-objectsigned-transact-sql.md)  
  
  
