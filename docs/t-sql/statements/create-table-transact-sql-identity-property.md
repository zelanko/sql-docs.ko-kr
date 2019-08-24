---
title: IDENTITY (Property)(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IDENTITY_TSQL
- IDENTITY
dev_langs:
- TSQL
helpviewer_keywords:
- IDENTITY property
- columns [SQL Server], creating
- identity columns [SQL Server], IDENTITY property
- autonumbers, identity numbers
ms.assetid: 8429134f-c821-4033-a07c-f782a48d501c
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8cf672f9aefc4b9fa0444c73596d2fac67089474
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938939"
---
# <a name="create-table-transact-sql-identity-property"></a>CREATE TABLE(Transact-SQL) IDENTITY (Property)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  테이블에 ID 열을 만듭니다. 이 속성은 CREATE TABLE 및 ALTER TABLE [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 사용됩니다.  
  
> [!NOTE]  
>  IDENTITY 속성은 열의 행 ID 속성을 표시하는 SQL-DMO **Identity** 속성과 다릅니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
IDENTITY [ (seed , increment) ]  
```  
  
## <a name="arguments"></a>인수  
 *seed*  
 테이블에 로드되는 첫 번째 행에 사용하는 값입니다.  
  
 *increment*  
 로드된 이전 행의 ID 값에 추가되는 증가값입니다.  
  
 초기값과 증가값을 모두 지정하거나 모두 지정하지 않아야 합니다. 둘 다 지정하지 않은 경우에는 기본값 (1,1)이 사용됩니다.  
  
## <a name="remarks"></a>Remarks  
 ID 열은 키 값을 생성하는 데 사용할 수 있습니다. 열에 있는 IDENTITY 속성은 다음 사항을 보장합니다.  
  
-   각각의 새 값은 현재 시드 및 증가를 기준으로 생성됩니다.  
  
-   특정 트랜잭션에 대한 각각의 새 값은 테이블의 각 동시 트랜잭션마다 다릅니다.  
  
 열에 있는 IDENTITY 속성은 다음 사항을 보장하지 않습니다.  
  
-   **값의 고유성** – 고유성은 **PRIMARY KEY** 또는 **UNIQUE** 제약 조건 또는 **UNIQUE** 인덱스를 사용하여 적용되어야 합니다.  
  
-   **트랜잭션 내에서 연속적인 값** – 테이블에서 다른 동시 삽입이 발생할 수 있기 때문에 여러 행 삽입 트랜잭션은 행에 대한 연속적인 값 가져오기를 보장하지 않습니다. 값이 연속적이어야 하는 경우 트랜잭션에서 테이블에 대해 배타적 잠금을 사용하거나 **SERIALIZABLE** 격리 수준을 사용해야 합니다.  
  
-   **서버 다시 시작 또는 다른 실패 후 연속적인 값** -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 성능상의 이유로 ID 값을 캐싱할 수 있으며 데이터베이스 오류 또는 서버 재시작 중에 지정된 값의 일부가 손실될 수 있습니다. 그러면 삽입 시 ID 값에서 간격이 발생할 수 있습니다. 간격이 허용되지 않는 경우 애플리케이션에서 고유 메커니즘을 사용하여 키 값을 생성해야 합니다. **NOCACHE** 옵션과 함께 시퀀스 생성기를 사용하면 커밋되지 않는 트랜잭션에 대한 간격을 제한할 수 있습니다.  
  
-   **값의 재사용** – 특정 IDENTITY 속성에 특정 시드/증가값이 지정된 경우, 이 ID 값은 엔진에서 다시 사용되지 않습니다. 특정 insert 문이 실패하거나 insert 문이 롤백되는 경우 사용된 ID 값은 손실되고 다시 생성되지 않습니다. 그 결과 후속 ID 값이 생성될 때 간격이 발생할 수 있습니다.  
  
 이러한 제한 사항은 일반적인 많은 상황에서 허용되므로 성능 개선을 위한 디자인의 일부입니다. 이러한 제한 사항 때문에 ID 값을 사용할 수 없는 경우 현재 값을 저장하는 별도 테이블을 만들고 애플리케이션에 대한 테이블 및 번호 지정 액세스를 관리하세요.  
  
 ID 열이 있는 테이블이 복제를 위해 게시된 경우 해당 ID 열은 사용되는 복제 유형에 적합한 방식으로 관리해야 합니다. 자세한 내용은 [ID 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)를 참조하세요.  
  
 ID 열은 테이블당 하나만 만들 수 있습니다.  
  
 메모리 최적화 테이블에서 초기값과 증가값은 둘 다 1,1로 설정되어야 합니다. 시드 또는 증가를 1 이외의 값으로 설정하면 다음과 같은 오류가 발생합니다. 1 이외의 시드 및 증가 사용은 메모리 최적화 테이블에서 지원되지 않습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-the-identity-property-with-create-table"></a>1\. CREATE TABLE에 IDENTITY 속성 사용  
 다음 예에서는 자동으로 ID를 증가시키는 `IDENTITY` 속성을 사용하여 새 테이블을 만듭니다.  
  
```  
USE AdventureWorks2012;  
  
IF OBJECT_ID ('dbo.new_employees', 'U') IS NOT NULL  
   DROP TABLE new_employees;  
GO  
CREATE TABLE new_employees  
(  
 id_num int IDENTITY(1,1),  
 fname varchar (20),  
 minit char(1),  
 lname varchar(30)  
);  
  
INSERT new_employees  
   (fname, minit, lname)  
VALUES  
   ('Karin', 'F', 'Josephs');  
  
INSERT new_employees  
   (fname, minit, lname)  
VALUES  
   ('Pirkko', 'O', 'Koskitalo');  
```  
  
### <a name="b-using-generic-syntax-for-finding-gaps-in-identity-values"></a>2\. 일반 구문을 사용하여 ID 값 간의 간격 찾기  
 다음 예에서는 데이터가 제거되었을 때 ID 값에서 간격을 찾기 위한 일반 구문을 보여 줍니다.  
  
> [!NOTE]  
>  다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트의 첫 번째 부분은 설명 목적으로만 제공되는 것입니다. 주석으로 시작하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 실행할 수 있습니다. `-- Create the img table`.  
  
```  
-- Here is the generic syntax for finding identity value gaps in data.  
-- The illustrative example starts here.  
SET IDENTITY_INSERT tablename ON;  
DECLARE @minidentval column_type;  
DECLARE @maxidentval column_type;  
DECLARE @nextidentval column_type;  
SELECT @minidentval = MIN($IDENTITY), @maxidentval = MAX($IDENTITY)  
    FROM tablename  
IF @minidentval = IDENT_SEED('tablename')  
   SELECT @nextidentval = MIN($IDENTITY) + IDENT_INCR('tablename')  
   FROM tablename t1  
   WHERE $IDENTITY BETWEEN IDENT_SEED('tablename') AND   
      @maxidentval AND  
      NOT EXISTS (SELECT * FROM tablename t2  
         WHERE t2.$IDENTITY = t1.$IDENTITY +   
            IDENT_INCR('tablename'))  
ELSE  
   SELECT @nextidentval = IDENT_SEED('tablename');  
SET IDENTITY_INSERT tablename OFF;  
-- Here is an example to find gaps in the actual data.  
-- The table is called img and has two columns: the first column   
-- called id_num, which is an increasing identification number, and the   
-- second column called company_name.  
-- This is the end of the illustration example.  
  
-- Create the img table.  
-- If the img table already exists, drop it.  
-- Create the img table.  
IF OBJECT_ID ('dbo.img', 'U') IS NOT NULL  
   DROP TABLE img;  
GO  
CREATE TABLE img (id_num int IDENTITY(1,1), company_name sysname);  
INSERT img(company_name) VALUES ('New Moon Books');  
INSERT img(company_name) VALUES ('Lucerne Publishing');  
-- SET IDENTITY_INSERT ON and use in img table.  
SET IDENTITY_INSERT img ON;  
  
DECLARE @minidentval smallint;  
DECLARE @nextidentval smallint;  
SELECT @minidentval = MIN($IDENTITY) FROM img  
 IF @minidentval = IDENT_SEED('img')  
    SELECT @nextidentval = MIN($IDENTITY) + IDENT_INCR('img')  
    FROM img t1  
    WHERE $IDENTITY BETWEEN IDENT_SEED('img') AND 32766 AND  
      NOT    EXISTS (SELECT * FROM img t2  
          WHERE t2.$IDENTITY = t1.$IDENTITY + IDENT_INCR('img'))  
 ELSE  
    SELECT @nextidentval = IDENT_SEED('img');  
SET IDENTITY_INSERT img OFF;  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DBCC CHECKIDENT&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [IDENT_INCR&#40;Transact-SQL&#41;](../../t-sql/functions/ident-incr-transact-sql.md)   
 [@@IDENTITY&#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)   
 [IDENTITY &#40;Function&#41; &#40;Transact-SQL&#41;](../../t-sql/functions/identity-function-transact-sql.md)   
 [IDENT_SEED &#40;Transact-SQL&#41;](../../t-sql/functions/ident-seed-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET IDENTITY_INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/set-identity-insert-transact-sql.md)   
 [ID 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  
