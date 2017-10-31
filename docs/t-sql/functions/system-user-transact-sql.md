---
title: SYSTEM_USER (Transact SQL) | Microsoft Docs
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
- SYSTEM_USER_TSQL
- SYSTEM_USER
dev_langs:
- TSQL
helpviewer_keywords:
- current user names
- system-supplied user names [SQL Server]
- users [SQL Server], logins
- logins [SQL Server], identification name
- current system user names
- SYSTEM_USER function
- inserting system user name into table
- system usernames [SQL Server]
- users [SQL Server], names
ms.assetid: 565984cd-60c6-4df7-83ea-2349b838ccb2
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d3f13d5db5d7787a60c455edc64644f4c23779fc
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="systemuser-transact-sql"></a>SYSTEM_USER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  기본값이 지정되지 않은 경우에 현재 로그인에 대해 시스템이 제공한 값을 테이블에 삽입할 수 있도록 허용합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SYSTEM_USER  
```  
  
## <a name="return-types"></a>반환 형식  
 **nchar**  
  
## <a name="remarks"></a>주의  
 CREATE TABLE 및 ALTER TABLE 문에서 SYSTEM_USER 함수를 DEFAULT 제약 조건으로 사용할 수 있습니다. 이 함수를 표준 함수로 사용할 수도 있습니다.  
  
 사용자 이름과 로그인 이름이 다르면 SYSTEM_USER가 로그인 이름을 반환합니다.  
  
 현재 사용자가에 로그인 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SYSTEM_USER 형식의 Windows 로그인 id 이름을 반환 Windows 인증을 사용 하 여: *도메인*\\*user_login_name*. 하지만 현재 사용자가 SQL Server 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로그인한 경우에는 SYSTEM_USER가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 ID 이름을 반환합니다. 예를 들어 `WillisJo`로 로그인한 사용자의 경우에는 `WillisJo`를 반환합니다.  
  
 SYSTEM_USER는 현재 실행 중인 컨텍스트의 이름을 반환합니다. EXECUTE AS 문이 컨텍스트를 전환하는 데 사용된 경우에는 SYSTEM_USER가 가장된 컨텍스트의 이름을 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-systemuser-to-return-the-current-system-user-name"></a>1. SYSTEM_USER를 사용하여 현재 시스템 사용자 이름 반환  
 다음 예에서는 `char` 변수를 선언하고 변수에 `SYSTEM_USER`의 현재 값을 저장한 다음에 변수에 저장된 값을 출력합니다.  
  
```  
DECLARE @sys_usr char(30);  
SET @sys_usr = SYSTEM_USER;  
SELECT 'The current system user is: '+ @sys_usr;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
----------------------------------------------------------
The current system user is: WillisJo

(1 row(s) affected)
 ```  
  
### <a name="b-using-systemuser-with-default-constraints"></a>2. DEFAULT 제약 조건으로 SYSTEM_USER 사용  
 다음 예에서는 `SYSTEM_USER` 열에 대한 `DEFAULT` 제약 조건으로 `SRep_tracking_user`를 사용하는 테이블을 만듭니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE Sales.Sales_Tracking  
(  
    Territory_id int IDENTITY(2000, 1) NOT NULL,  
    Rep_id  int NOT NULL,  
    Last_sale datetime NOT NULL DEFAULT GETDATE(),  
    SRep_tracking_user varchar(30) NOT NULL DEFAULT SYSTEM_USER  
);  
GO  
INSERT Sales.Sales_Tracking (Rep_id)  
VALUES (151);  
INSERT Sales.Sales_Tracking (Rep_id, Last_sale)  
VALUES (293, '19980515');  
INSERT Sales.Sales_Tracking (Rep_id, Last_sale)  
VALUES (27882, '19980620');  
INSERT Sales.Sales_Tracking (Rep_id)  
VALUES (21392);  
INSERT Sales.Sales_Tracking (Rep_id, Last_sale)  
VALUES (24283, '19981130');  
GO  
```  
  
 다음 쿼리는 `Sales_Tracking` 테이블에서 모든 정보를 선택합니다.  
  
```  
SELECT * FROM Sales_Tracking ORDER BY Rep_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Territory_id Rep_id Last_sale            SRep_tracking_user
-----------  ------ -------------------- ------------------
2000         151    Mar 4 1998 10:36AM   ArvinDak
2001         293    May 15 1998 12:00AM  ArvinDak
2003         21392  Mar 4 1998 10:36AM   ArvinDak
2004         24283  Nov 3 1998 12:00AM   ArvinDak
2002         27882  Jun 20 1998 12:00AM  ArvinDak
  
(5 row(s) affected)
 ```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-systemuser-to-return-the-current-system-user-name"></a>C: SYSTEM_USER를 사용 하 여 현재 시스템 사용자 이름 반환  
 현재 값을 반환 하는 다음 예제에서는 `SYSTEM_USER`합니다.  
  
```  
SELECT SYSTEM_USER;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CURRENT_TIMESTAMP &#40; Transact SQL &#41;](../../t-sql/functions/current-timestamp-transact-sql.md)   
 [CURRENT_USER &#40; Transact SQL &#41;](../../t-sql/functions/current-user-transact-sql.md)   
 [SESSION_USER &#40; Transact SQL &#41;](../../t-sql/functions/session-user-transact-sql.md)   
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [User&#40; Transact SQL &#41;](../../t-sql/functions/user-transact-sql.md)  
  
  


