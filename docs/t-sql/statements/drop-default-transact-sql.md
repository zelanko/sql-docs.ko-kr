---
title: DROP DEFAULT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_DEFAULT_TSQL
- DROP DEFAULT
dev_langs:
- TSQL
helpviewer_keywords:
- DROP DEFAULT statement
- defaults [SQL Server], removing
ms.assetid: d2d3af25-8877-46ba-95d9-1844961d97ee
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 72accd7718280b4994c3339531c8e5d0fef067c1
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210793"
---
# <a name="drop-default-transact-sql"></a>DROP DEFAULT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스에서 하나 이상의 사용자 정의 기본값을 제거합니다.  
  
> [!IMPORTANT]
>  DROP DEFAULT는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다음 버전에서 제거될 예정입니다. 향후 개발 작업에서는 DROP DEFAULT를 사용하지 않도록 하고 현재 이것을 사용하는 응용 프로그램은 수정하십시오. [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 또는 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)의 DEFAULT 키워드를 사용하여 만들 수 있는 기본 정의를 대신 사용하십시오.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DROP DEFAULT [ IF EXISTS ] { [ schema_name . ] default_name } [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *IF EXISTS*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 이미 있는 경우에만 기본값을 조건부로 삭제합니다.  
  
 *schema_name*  
 기본값이 속한 스키마의 이름입니다.  
  
 *default_name*  
 기존 기본값의 이름입니다. 존재하는 기본값의 목록을 보려면 **sp_help**를 실행합니다. 기본값은 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다. 기본 스키마 이름을 지정하는 것은 선택 사항입니다.  
  
## <a name="remarks"></a>Remarks  
 열 또는 별칭 데이터 형식에 기본값이 바인딩된 경우 기본값을 삭제하기 전에 **sp_unbindefault**를 실행하여 기본값의 바인딩을 해제합니다.  
  
 Null 값이 허용되는 열에서 기본값을 삭제한 후 행을 추가하고 값을 명시적으로 제공하지 않으면 해당 위치에 NULL이 삽입됩니다. NOT NULL 열에서 기본값을 삭제한 후 행을 추가하고 값을 명시적으로 제공하지 않으면 오류 메시지가 반환됩니다. 이러한 행은 나중에 일반적인 INSERT 문을 실행하여 추가할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 DROP DEFAULT를 실행하려면 적어도 기본값이 속한 스키마에 대한 ALTER 권한을 가지고 있어야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-dropping-a-default"></a>1. 기본값 삭제  
 기본값이 열 또는 별칭 데이터 형식에 바인딩되지 않은 경우 단순히 DROP DEFAULT를 사용하여 삭제할 수 있습니다. 다음은 사용자가 만든 `datedflt`라는 기본값을 제거하는 예입니다.  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.objects  
         WHERE name = 'datedflt'   
            AND type = 'D')  
   DROP DEFAULT datedflt;  
GO  
```  
  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터는 다음 구문을 사용할 수 있습니다.  
  
```  
DROP DEFAULT IF EXISTS datedflt;  
GO  
```  
  
### <a name="b-dropping-a-default-that-has-been-bound-to-a-column"></a>2. 열에 바인딩된 기본값 삭제  
 다음은 `EmergencyContactPhone` 테이블의 `Contact` 열과 연결된 기본값의 바인딩을 해제하고 `phonedflt`라는 기본값을 삭제하는 예입니다.  
  
```  
USE AdventureWorks2012;  
GO  
   BEGIN   
      EXEC sp_unbindefault 'Person.Contact.Phone'  
      DROP DEFAULT phonedflt  
   END;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE DEFAULT&#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [sp_helptext&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_help&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_unbindefault&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)  
  
  
