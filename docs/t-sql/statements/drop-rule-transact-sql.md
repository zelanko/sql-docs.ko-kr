---
title: DROP RULE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_RULE_TSQL
- DROP RULE
dev_langs:
- TSQL
helpviewer_keywords:
- rules [SQL Server], removing
- deleting roles
- DROP RULE statement
- removing roles
- dropping roles
ms.assetid: 8370b730-7fd5-43fe-a7f6-8300b3caa16d
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 17a6075b5a1cc6e49ac894f41f5d8267294d60ef
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47723741"
---
# <a name="drop-rule-transact-sql"></a>DROP RULE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스에서 하나 이상의 사용자 정의 규칙을 제거합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서는 DROP RULE이 제거됩니다. 향후 개발 작업에서는 DROP RULE을 사용하지 않도록 하고 현재 이것을 사용하는 응용 프로그램은 수정하십시오. 대신 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 또는 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)의 CHECK 키워드로 만들 수 있는 CHECK 제약 조건을 사용하십시오. 자세한 내용은 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DROP RULE [ IF EXISTS ] { [ schema_name . ] rule_name } [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *IF EXISTS*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 이미 있는 경우에만 역할을 조건부로 삭제합니다.  
  
 *schema_name*  
 규칙이 속한 스키마의 이름입니다.  
  
 *rule*  
 제거할 규칙입니다. 규칙 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 적용되는 규칙을 준수해야 합니다. 규칙 스키마 이름을 지정하는 것은 선택 사항입니다.  
  
## <a name="remarks"></a>Remarks  
 현재 규칙이 열이나 별칭 데이터 형식에 바인딩된 경우 규칙을 삭제하려면 먼저 언바인딩해야 합니다. 규칙을 언바인딩하려면 **sp_unbindrule**을 사용하십시오. 바인딩된 규칙을 삭제하려고 시도하면 오류 메시지가 표시되고 DROP RULE 문이 취소됩니다.  
  
 규칙을 삭제한 후 이전에 규칙이 적용되었던 열에 새 데이터를 입력하면 해당 규칙의 제약 조건에 구애 받지 않고 입력됩니다. 기존 데이터는 아무런 영향도 받지 않습니다.  
  
 DROP RULE 문은 CHECK 제약 조건에 적용되지 않습니다. CHECK 제약 조건 삭제 방법은 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)을 참조하십시오.  
  
## <a name="permissions"></a>Permissions  
 DROP RULE을 실행하려면 최소한 규칙이 속한 스키마에 대한 ALTER 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `VendorID_rule`이라는 규칙을 언바인딩한 후 삭제합니다. 
  
```  
sp_unbindrule 'Production.ProductVendor.VendorID'  
DROP RULE VendorID_rule  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE RULE&#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [sp_bindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_help&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_unbindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [USE&#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  

