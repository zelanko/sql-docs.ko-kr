---
title: "DROP 서명 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP SIGNATURE
- DROP_SIGNATURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting signatures
- dropping signatures
- DROP SIGNATURE statement
- removing signatures
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 8a1fd8c5-0e75-4b2f-9d3c-c296bed56cc7
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 81823a549f608bdcddb631084904fb303a1ddc9f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-signature-transact-sql"></a>DROP SIGNATURE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  저장 프로시저, 함수, 트리거 또는 어셈블리에서 디지털 서명을 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP [ COUNTER ] SIGNATURE FROM module_name   
    BY <crypto_list> [ ,...n ]  
  
<crypto_list> ::=  
    CERTIFICATE cert_name  
    | ASYMMETRIC KEY Asym_key_name  
```  
  
## <a name="arguments"></a>인수  
 *모듈*  
 저장 프로시저, 함수, 어셈블리 또는 트리거의 이름입니다.  
  
 인증서 *cert_name*  
 저장 프로시저, 함수, 어셈블리 또는 트리거의 서명에 사용된 인증서의 이름입니다.  
  
 비대칭 키 *Asym_key_name*  
 저장 프로시저, 함수, 어셈블리 또는 트리거의 서명에 사용된 비대칭 키의 이름입니다.  
  
## <a name="remarks"></a>주의  
 서명 정보는 sys.crypt_properties 카탈로그 뷰에 표시됩니다.  
  
## <a name="permissions"></a>Permissions  
 개체에 대한 ALTER 권한과 인증서 또는 비대칭 키에 대한 CONTROL 권한이 필요합니다. 연결된 개인 키가 암호로 보호되어 있으면 사용자도 암호가 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 인증서의 서명을 제거 `HumanResourcesDP` 저장된 프로시저에서 `HumanResources.uspUpdateEmployeeLogin`합니다.  
  
```  
USE AdventureWorks2012;  
DROP SIGNATURE FROM HumanResources.uspUpdateEmployeeLogin   
    BY CERTIFICATE HumanResourcesDP;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.crypt_properties &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-crypt-properties-transact-sql.md)   
 [서명 추가 &#40; Transact SQL &#41;](../../t-sql/statements/add-signature-transact-sql.md)  
  
  

