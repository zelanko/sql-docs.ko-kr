---
title: SCOPE_IDENTITY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SCOPE_IDENTITY
- SCOPE_IDENTITY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identity columns [SQL Server], SCOPE_IDENTITY function
- SCOPE_IDENTITY function
- last-inserted identity values
- identity values [SQL Server], last-inserted
ms.assetid: eef24670-059b-4f10-91d4-a67bc1ed12ab
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1950d65a35d6fab52025d069e0338493ee7c639d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="scopeidentity-transact-sql"></a>SCOPE_IDENTITY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  같은 범위에서 ID 열에 삽입된 마지막 ID 값을 반환합니다. 범위는 저장 프로시저, 트리거, 함수 또는 일괄 처리와 같은 모듈입니다. 따라서 두 문이 같은 저장된 프로시저, 함수 또는 일괄 처리에 있으면 동일한 범위에 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SCOPE_IDENTITY()  
```  
  
## <a name="return-types"></a>반환 형식  
 **38, 0**  
  
## <a name="remarks"></a>주의  
 SCOPE_IDENTITY, IDENT_CURRENT 및 @@IDENTITY 는 id 열에 삽입 된 값을 반환 되기 때문에 비슷한 함수입니다.  
  
 IDENT_CURRENT는 범위와 세션으로 제한되는 것이 아니라 지정된 테이블로 제한됩니다. IDENT_CURRENT는 임의 세션 및 범위에 있는 특정 테이블에 생성된 값을 반환합니다. 자세한 내용은 참조 [IDENT_CURRENT &#40; Transact SQL &#41; ](../../t-sql/functions/ident-current-transact-sql.md).  
  
 SCOPE_IDENTITY 및 @@IDENTITY 현재 세션의 모든 테이블에서 생성 된 마지막 id 값을 반환 합니다. SCOPE_IDENTITY는 현재 범위 내에 삽입 된 값을 반환 하는 반면 @@IDENTITY 특정 범위로 제한 되지 않습니다.  
  
 예를 들어 두 개의 테이블 T1과 T2가 있고 T1에 INSERT 트리거가 정의되어 있다고 가정합니다. T1에 행이 삽입될 때 트리거가 발생하고 T2에서 행을 삽입합니다. 이 시나리오에서는 T1에서의 삽입과 트리거에 의한 T2에서의 삽입이라는 두 범위를 보여 줍니다.  
  
 T 1과 T2 모두 id 열이 있고 이라고 가정할@IDENTITY SCOPE_IDENTITY t 1에 INSERT 문이 끝날 때 다른 값을 반환 합니다. @@IDENTITY 현재 세션의 모든 범위에서 삽입 된 마지막 id 열 값을 반환 합니다. 이 값은 T2에 삽입된 값입니다. Scope_identity ()는 t 1에 삽입 된 ID 값을 반환 합니다. 이 값은 같은 범위에서 발생한 마지막 삽입 값입니다. Scope_identity () 함수 범위에 id 열에 INSERT 문이 발생 하기 전에 함수 호출 하는 경우 null 값을 반환 합니다.  
  
 문 및 트랜잭션이 실패해도 테이블의 현재 ID가 변경되고 ID 열 값 간에 간격이 생성될 수 있습니다. 테이블에 값을 삽입하려고 시도한 트랜잭션이 커밋되지 않아도 ID 값은 롤백되지 않습니다. 예를 들어 IGNORE_DUP_KEY 위반으로 인해 INSERT 문이 실패해도 테이블의 현재 ID 값은 계속 증가합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-identity-and-scopeidentity-with-triggers"></a>1. 를 사용 하 여@IDENTITY 및 트리거와 함께 SCOPE_IDENTITY  
 다음 예에서는 두 개의 테이블 `TZ` 및 `TY`를 만들고 `TZ`에서 INSERT 트리거를 만듭니다. `TZ` 테이블에 행이 삽입될 때 트리거(`Ztrig`)가 발생하고 `TY`에서 행을 삽입합니다.  
  
```sql  
USE tempdb;  
GO  
CREATE TABLE TZ (  
   Z_id  int IDENTITY(1,1)PRIMARY KEY,  
   Z_name varchar(20) NOT NULL);  
  
INSERT TZ  
   VALUES ('Lisa'),('Mike'),('Carla');  
  
SELECT * FROM TZ;  
```     
결과 집합: 테이블 TZ 표시 하는 방법입니다.  
  
```  
Z_id   Z_name  
-------------  
1      Lisa  
2      Mike  
3      Carla  
```  
```sql 
CREATE TABLE TY (  
   Y_id  int IDENTITY(100,5)PRIMARY KEY,  
   Y_name varchar(20) NULL);  
  
INSERT TY (Y_name)  
   VALUES ('boathouse'), ('rocks'), ('elevator');  
  
SELECT * FROM TY;  
```   
결과 집합: TY 표시 하는 방법입니다.  
```  
Y_id  Y_name  
---------------  
100   boathouse  
105   rocks  
110   elevator  
```  

행이 테이블 TZ에에서 삽입 하는 경우 TY 테이블의 행을 삽입 하는 트리거를 만듭니다.  
```sql  
CREATE TRIGGER Ztrig  
ON TZ  
FOR INSERT AS   
   BEGIN  
   INSERT TY VALUES ('')  
   END;  
```  
트리거를 시작 하 고 어떤 id 값으로 가져올 결정는 @@IDENTITY 및 SCOPE_IDENTITY 함수입니다.   
```sql
INSERT TZ VALUES ('Rosalie');  
  
SELECT SCOPE_IDENTITY() AS [SCOPE_IDENTITY];  
GO  
SELECT @@IDENTITY AS [@@IDENTITY];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
```
/*SCOPE_IDENTITY returns the last identity value in the same scope. This was the insert on table TZ.*/`  
SCOPE_IDENTITY  
4  

/*@@IDENTITY returns the last identity value inserted to TY by the trigger. 
  This fired because of an earlier insert on TZ.*/
@@IDENTITY  
115  
```  
  
### <a name="b-using-identity-and-scopeidentity-with-replication"></a>2. 를 사용 하 여@IDENTITY 및 복제와 scope_identity)  
 다음 예에서는 병합 복제용으로 게시된 데이터베이스에서 삽입을 위해 `@@IDENTITY` 및 `SCOPE_IDENTITY()`를 사용하는 방법을 보여 줍니다. 이 예의 두 테이블은 모두 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스에 있습니다. `Person.ContactType`은 게시되지 않았고 `Sales.Customer`는 게시되었습니다. 병합 복제는 게시된 테이블에 트리거를 추가합니다. 따라서 `@@IDENTITY`는 사용자 테이블에 대한 삽입 대신 복제 시스템 테이블에 대한 삽입에서 값을 반환할 수 있습니다.  
  
 `Person.ContactType` 테이블에 최대 id 값은 20입니다. 테이블에 행을 삽입하면 `@@IDENTITY` 및 `SCOPE_IDENTITY()`에서 동일한 값을 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
INSERT INTO Person.ContactType ([Name]) VALUES ('Assistant to the Manager');  
GO  
SELECT SCOPE_IDENTITY() AS [SCOPE_IDENTITY];  
GO  
SELECT @@IDENTITY AS [@@IDENTITY];  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
```  
SCOPE_IDENTITY  
21  
@@IDENTITY  
21
```  
  
 `Sales.Customer` 테이블의 최대 ID 값은 29483입니다. 테이블에 행을 삽입하면 `@@IDENTITY` 및 `SCOPE_IDENTITY()`에서 서로 다른 값을 반환합니다. `SCOPE_IDENTITY()`는 사용자 테이블에 대한 삽입에서 값을 반환하는 반면 `@@IDENTITY`는 복제 시스템 테이블에 대한 삽입에서 값을 반환합니다. 삽입된 ID 값에 액세스해야 하는 응용 프로그램에 대해 `SCOPE_IDENTITY()`를 사용합니다.  
  
```sql  
INSERT INTO Sales.Customer ([TerritoryID],[PersonID]) VALUES (8,NULL);  
GO  
SELECT SCOPE_IDENTITY() AS [SCOPE_IDENTITY];  
GO  
SELECT @@IDENTITY AS [@@IDENTITY];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
 ```
 SCOPE_IDENTITY  
 29484  
 @@IDENTITY  
 89
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [@@IDENTITY&#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)  
  
  

