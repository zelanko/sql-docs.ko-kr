---
title: DROP SECURITY POLICY (Transact SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_SECURITY_POLICY_TSQL
- DROP SECURITY POLICY
- DROP SECURITY
- DROP_SECURITY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP SECURITY POLICY statement
ms.assetid: 5bd3393d-2fa5-4db0-a69a-a1a72d638e9d
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 146d8d9341ae1d7c8cb63f4ebf186be95914a04f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-security-policy-transact-sql"></a>DROP SECURITY POLICY (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  보안 정책을 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DROP SECURITY POLICY [ IF EXISTS ] [schema_name. ] security_policy_name    
[;]  
```  
  
## <a name="arguments"></a>인수  
 *경우에 존재*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 조건에 따라 이미 있는 경우에 보안 정책을 삭제 합니다.  
  
 *schema_name*  
 보안 정책이 속한 스키마의 이름입니다.  
  
 *security_policy_name*  
 보안 정책의 이름입니다. 보안 정책 이름은 식별자에 대한 규칙을 따라야 하며 데이터베이스에서 각 스키마별로 고유해야 합니다.  
  
## <a name="remarks"></a>주의  
  
## <a name="permissions"></a>Permissions  
 스키마에 대한 ALTER ANY SECURITY POLICY 권한 및 ALTER 권한이 필요합니다.  
  
## <a name="example"></a>예제  
  
```  
DROP SECURITY POLICY secPolicy;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [행 수준 보안](../../relational-databases/security/row-level-security.md)   
 [CREATE SECURITY POLICY&#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [ALTER SECURITY POLICY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-security-policy-transact-sql.md)   
 [sys.security_policies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [sys.security_predicates&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)  
  
  

