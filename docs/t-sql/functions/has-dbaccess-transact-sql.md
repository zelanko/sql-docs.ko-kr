---
title: HAS_DBACCESS (Transact SQL) | Microsoft Docs
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
- HAS_DBACCESS_TSQL
- HAS_DBACCESS
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], verifying
- permissions [SQL Server], user access status
- HAS_DBACCESS
- checking permission status
- verifying permission status
- users [SQL Server], access rights status
- testing permissions
- status information [SQL Server], user access
ms.assetid: 99b43a72-0722-4a7b-a493-bdee1c74c7b9
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: efb5681a5ca390fb2c00033dbbfc70c27ae9544e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="hasdbaccess-transact-sql"></a>HAS_DBACCESS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  지정된 데이터베이스를 사용자가 액세스할 수 있는지에 대한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
HAS_DBACCESS ( 'database_name' )  
```  
  
## <a name="arguments"></a>인수  
 '*database_name*'  
 사용자가 액세스 정보를 얻으려고 하는 데이터베이스의 이름입니다. *a s e _* 은 **sysname**합니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>주의  
 HAS_DBACCESS는 사용자가 데이터베이스에 액세스할 수 있으면 1을 반환하고 사용자가 데이터베이스에 액세스할 수 없으면 0을 반환하며 데이터베이스 이름이 잘못되었으면 NULL을 반환합니다.  
  
 HAS_DBACCESS는 데이터베이스가 오프라인 또는 주의 대상이면 0을 반환합니다.  
  
 HAS_DBACCESS는 데이터베이스가 단일 사용자 모드에 있고 다른 사용자가 데이터베이스를 사용 중이면 0을 반환합니다.  
  
## <a name="permissions"></a>Permissions  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 사용자가 `AdventureWorks2012` 데이터베이스에 액세스할 수 있는지 테스트하는 방법을 보여 줍니다.  
  
```  
SELECT HAS_DBACCESS('AdventureWorks2012');  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 현재 사용자가 `AdventureWorksPDW2012` 데이터베이스에 액세스할 수 있는지 테스트하는 방법을 보여 줍니다.  
  
```  
SELECT HAS_DBACCESS('AdventureWorksPDW2012');  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Is_member&#40; Transact SQL &#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [IS_SRVROLEMEMBER&#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)  
  
  


