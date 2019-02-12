---
title: USER_ID(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 5fe880e39b2ace4b23356fbd9ab77b37193cc838
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56021428"
---
# <a name="userid-transact-sql"></a>USER_ID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  데이터베이스 사용자의 ID를 반환합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [DATABASE_PRINCIPAL_ID](../../t-sql/functions/database-principal-id-transact-sql.md)를 사용하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
USER_ID ( [ 'user' ] )  
```  
  
## <a name="arguments"></a>인수  
 *user*  
 사용할 사용자 이름입니다. *사용자*는 **nchar**입니다. **char** 값을 지정하면 암시적으로 **nchar**로 변환됩니다. 괄호가 필요합니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>Remarks  
 *사용자*를 생략하면 현재 사용자가 대신 사용됩니다. 매개 변수에 NULL이라는 단어가 포함되어 있으면 NULL이 반환됩니다. EXECUTE AS를 호출한 후 USER_ID를 호출하면 가장된 컨텍스트의 ID가 반환됩니다.  
  
 특정 데이터베이스 사용자에 매핑되지 않은 Windows 보안 주체가 그룹 멤버 자격으로 데이터베이스에 액세스하면 USER_ID가 0(public의 ID)을 반환합니다. 이러한 보안 주체가 스키마를 지정하지 않고 개체를 만들면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 해당 Windows 보안 주체에 매핑되는 암시적 사용자와 스키마를 생성합니다. 이렇게 생성된 사용자는 데이터베이스 연결에 사용할 수 없습니다. 암시적 사용자에 매핑되는 Windows 보안 주체로 USER_ID를 호출하면 암시적 사용자의 ID가 반환됩니다.  
  
 USER_ID는 SELECT 목록, WHERE 절 및 식을 사용할 수 있는 곳이면 어디에서나 사용할 수 있습니다. 자세한 내용은 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdventureWorks2012` 사용자인 `Harold`의 ID를 반환합니다.  
  
```  
USE AdventureWorks2012;  
SELECT USER_ID('Harold');  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [USER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [DATABASE_PRINCIPAL_ID &#40;Transact-SQL&#41;](../../t-sql/functions/database-principal-id-transact-sql.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
