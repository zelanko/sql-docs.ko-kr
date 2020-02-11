---
title: sp_helptext (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helptext
- sp_helptext_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helptext
ms.assetid: 24135456-05f0-427c-884b-93cf38dd47a8
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 160d52c8c145828f6a63c104aecb17e04867cee8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68048292"
---
# <a name="sp_helptext-transact-sql"></a>sp_helptext(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  사용자 정의 규칙, 기본값, 암호화되지 않은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저, 사용자 정의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수, 트리거, 계산 열, CHECK 제약 조건, 뷰 또는 시스템 저장 프로시저와 같은 시스템 개체의 정의를 표시합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helptext [ @objname = ] 'name' [ , [ @columnname = ] computed_column_name ]  
```  
  
## <a name="arguments"></a>인수  
`[ @objname = ] 'name'`사용자 정의 스키마 범위 개체의 정규화 된 이름 또는 정규화 되지 않은 이름입니다. 따옴표는 정규화된 개체를 지정하는 경우에만 필요합니다. 데이터베이스 이름을 포함한 정규화된 이름인 경우 반드시 현재 데이터베이스의 이름을 사용해야 합니다. 개체는 반드시 현재 데이터베이스에 있어야 합니다. *name* 은 **nvarchar (776)** 이며 기본값은 없습니다.  
  
`[ @columnname = ] 'computed_column_name'`정의 정보를 표시할 계산 열의 이름입니다. 열이 포함 된 테이블을 *이름*으로 지정 해야 합니다. *column_name* 는 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**본문**|**nvarchar(255)**|개체 정의|  
  
## <a name="remarks"></a>설명  
 sp_helptext는 여러 행에 개체를 만드는 데 사용하는 정의를 표시합니다. 각 행은 255자의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 정의를 포함합니다. 정의는 [sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) 카탈로그 뷰의 **정의** 열에 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다. 시스템 개체 정의는 공개적으로 표시됩니다. 개체 소유자나 ALTER, CONTROL, TAKE OWNERSHIP 또는 VIEW DEFINITION 권한 중 하나를 부여받은 사람은 사용자 개체의 정의를 볼 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-displaying-the-definition-of-a-trigger"></a>A. 트리거의 정의 표시  
 다음 예에서는 `dEmployee` 데이터베이스에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 트리거 정의를 표시합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helptext 'HumanResources.dEmployee';  
GO  
```  
  
### <a name="b-displaying-the-definition-of-a-computed-column"></a>B. 계산 열의 정의 표시  
 다음 예에서는 `TotalDue` 데이터베이스의 `SalesOrderHeader` 테이블에 있는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 계산 열의 정의를 표시하는 방법을 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
sp_helptext @objname = N'AdventureWorks2012.Sales.SalesOrderHeader', @columnname = TotalDue ;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Text`  
  
 `---------------------------------------------------------------------`  
  
 `(isnull(([SubTotal]+[TaxAmt])+[Freight],(0)))`  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;OBJECT_DEFINITION &#40;](../../t-sql/functions/object-definition-transact-sql.md)   
 [sp_help&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sql_modules &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
