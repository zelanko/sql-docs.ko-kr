---
title: SESSION_USER (Transact SQL) | Microsoft Docs
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
- SESSION_USER_TSQL
- SESSION_USER
dev_langs:
- TSQL
helpviewer_keywords:
- usernames [SQL Server]
- current user names
- sessions [SQL Server], user names
- displaying user names
- viewing user names
- SESSION_USER function
ms.assetid: 3dbe8532-31b6-4862-8b2a-e58b00b964de
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 88b9d27bfc084e341712c374c54098984c0f3e95
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="sessionuser-transact-sql"></a>SESSION_USER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  SESSION_USER는 현재 데이터베이스에 있는 현재 컨텍스트의 사용자 이름을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SESSION_USER  
```  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar (128)**  
  
## <a name="remarks"></a>주의  
 SESSION_USER를 CREATE TABLE 또는 ALTER TABLE 문에서 DEFAULT 제약 조건으로 사용하거나 임의의 표준 함수로 사용합니다. 지정된 기본값이 없으면 SESSION_USER를 테이블에 삽입할 수 있습니다. 이 함수에는 인수가 필요하지 않습니다. SESSION_USER는 쿼리에서 사용할 수 있습니다.  
  
 컨텍스트 전환 후 SESSION_USER를 호출하면 가장된 컨텍스트의 사용자 이름이 반환됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-sessionuser-to-return-the-user-name-of-the-current-session"></a>1. SESSION_USER를 사용하여 현재 세션의 사용자 이름 반환  
 다음 예에서는 변수를 `nchar`로 선언하고 이 변수에 `SESSION_USER`의 현재 값을 할당한 다음 텍스트 설명과 함께 변수를 인쇄합니다.  
  
```  
DECLARE @session_usr nchar(30);  
SET @session_usr = SESSION_USER;  
SELECT 'This session''s current user is: '+ @session_usr;  
GO  
```  
  
 다음은 세션 사용자가 `Surya`일 때의 결과 집합입니다.  
  
 `--------------------------------------------------------------`  
  
 `This session's current user is: Surya`  
  
 `(1 row(s) affected)`  
  
### <a name="b-using-sessionuser-with-default-constraints"></a>2. DEFAULT 제약 조건으로 SESSION_USER 사용  
 다음 예에서는 배송물 수령을 기록하는 사람의 이름에 대한 `SESSION_USER` 제약 조건으로 `DEFAULT`를 사용하는 테이블을 만듭니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE deliveries3  
(  
 order_id int IDENTITY(5000, 1) NOT NULL,  
 cust_id  int NOT NULL,  
 order_date smalldatetime NOT NULL DEFAULT GETDATE(),  
 delivery_date smalldatetime NOT NULL DEFAULT   
    DATEADD(dd, 10, GETDATE()),  
 received_shipment nchar(30) NOT NULL DEFAULT SESSION_USER  
);  
GO  
```  
  
 테이블에 추가된 레코드에는 현재 사용자의 사용자 이름이 표시됩니다. 이 예에서 `Wanida`, `Sylvester` 및 `Alejandro`이 배송물 수령을 확인합니다. 이것은 `EXECUTE AS`를 통해 사용자 컨텍스트를 전환하여 에뮬레이트할 수 있습니다.  
  
```  
EXECUTE AS USER = 'Wanida'  
INSERT deliveries3 (cust_id)  
VALUES (7510);  
INSERT deliveries3 (cust_id)  
VALUES (7231);  
REVERT;  
EXECUTE AS USER = 'Sylvester'  
INSERT deliveries3 (cust_id)  
VALUES (7028);  
REVERT;  
EXECUTE AS USER = 'Alejandro'  
INSERT deliveries3 (cust_id)  
VALUES (7392);  
INSERT deliveries3 (cust_id)  
VALUES (7452);  
REVERT;  
GO  
```  
  
 다음 쿼리는 `deliveries3` 테이블에서 모든 정보를 선택합니다.  
  
```  
SELECT order_id AS 'Order #', cust_id AS 'Customer #',   
   delivery_date AS 'When Delivered', received_shipment   
   AS 'Received By'  
FROM deliveries3  
ORDER BY order_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Order #   Customer #  When Delivered       Received By`  
  
 `--------  ----------  -------------------  -----------`  
  
 `5000      7510        2005-03-16 12:02:14  Wanida`  
  
 `5001      7231        2005-03-16 12:02:14  Wanida`  
  
 `5002      7028        2005-03-16 12:02:14  Sylvester`  
  
 `5003      7392        2005-03-16 12:02:14  Alejandro`  
  
 `5004      7452        2005-03-16 12:02:14  Alejandro`  
  
 `(5 row(s) affected)`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-sessionuser-to-return-the-user-name-of-the-current-session"></a>C: SESSION_USER를 사용 하 여 현재 세션의 사용자 이름을 반환 하는  
 다음 예에서는 현재 세션에 대 한 세션 사용자를 반환 합니다.  
  
```  
SELECT SESSION_USER;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CURRENT_TIMESTAMP &#40; Transact SQL &#41;](../../t-sql/functions/current-timestamp-transact-sql.md)   
 [CURRENT_USER &#40; Transact SQL &#41;](../../t-sql/functions/current-user-transact-sql.md)   
 [SYSTEM_USER &#40; Transact SQL &#41;](../../t-sql/functions/system-user-transact-sql.md)   
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [User&#40; Transact SQL &#41;](../../t-sql/functions/user-transact-sql.md)   
 [USER_NAME &#40; Transact SQL &#41;](../../t-sql/functions/user-name-transact-sql.md)  
  
  


