---
title: USER_ID (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- USER_ID
- USER_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- USER_ID function
- identification numbers [SQL Server]
- IDs [SQL Server], databases
- users [SQL Server], database ID numbers
- database IDs [SQL Server]
- identification numbers [SQL Server], databases
ms.assetid: 67fd29bc-eda9-4d4d-b148-5d3659181a43
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a40853c10e17969c78ef88e4b75995e77b8a1bac
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="userid-transact-sql"></a>USER_ID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  데이터베이스 사용자의 ID를 반환합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]사용 하 여 [DATABASE_PRINCIPAL_ID](../../t-sql/functions/database-principal-id-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
USER_ID ( [ 'user' ] )  
```  
  
## <a name="arguments"></a>인수  
 *사용자*  
 사용할 사용자 이름입니다. *사용자* 은 **nchar**합니다. 경우는 **char** 값을 지정 하면 암시적으로 변환 됩니다 **nchar**합니다. 괄호가 필요합니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>주의  
 때 *사용자* 은 생략 하면 현재 사용자 가정 됩니다. 매개 변수에 NULL이라는 단어가 포함되어 있으면 NULL이 반환됩니다. EXECUTE AS를 호출한 후 USER_ID를 호출하면 가장된 컨텍스트의 ID가 반환됩니다.  
  
 특정 데이터베이스 사용자에 매핑되지 않은 Windows 보안 주체가 그룹 멤버 자격으로 데이터베이스에 액세스하면 USER_ID가 0(public의 ID)을 반환합니다. 이러한 보안 주체가 스키마를 지정하지 않고 개체를 만들면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 해당 Windows 보안 주체에 매핑되는 암시적 사용자와 스키마를 생성합니다. 이렇게 생성된 사용자는 데이터베이스 연결에 사용할 수 없습니다. 암시적 사용자에 매핑되는 Windows 보안 주체로 USER_ID를 호출하면 암시적 사용자의 ID가 반환됩니다.  
  
 USER_ID는 SELECT 목록, WHERE 절 및 식을 사용할 수 있는 곳이면 어디에서나 사용할 수 있습니다. 자세한 내용은 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdventureWorks2012` 사용자인 `Harold`의 ID를 반환합니다.  
  
```  
USE AdventureWorks2012;  
SELECT USER_ID('Harold');  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [USER_NAME &#40; Transact SQL &#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [DATABASE_PRINCIPAL_ID &#40; Transact SQL &#41;](../../t-sql/functions/database-principal-id-transact-sql.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  

