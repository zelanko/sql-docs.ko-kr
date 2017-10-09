---
title: "데이터 정렬은 | Microsoft Docs"
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
- COLLATE
- COLLATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], COLLATE clause
- COLLATE clause
ms.assetid: 76763ac8-3e0d-4bbb-aa53-f5e7da021daa
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9154d293ca5b7737a9c80fef0754dcec6e461a46
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="collations"></a>데이터 정렬
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  데이터베이스 정의 또는 열 정의에 적용하여 데이터 정렬을 정의하거나 문자열 식에 적용하여 데이터 정렬 캐스트를 적용하기 위한 절입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
COLLATE { <collation_name> | database_default }  
<collation_name> :: =   
     { Windows_collation_name } | { SQL_collation_name }  
```  
  
## <a name="arguments"></a>인수  
 *데이터 정렬 이름*  
 식, 열 정의 또는 데이터베이스 정의에 적용할 데이터 정렬의 이름입니다. *데이터 정렬 이름* 수만 지정 *Windows_collation_name* 또는 *SQL_collation_name*합니다. *데이터 정렬 이름* 리터럴 값 이어야 합니다. *데이터 정렬 이름* 변수나 식으로 표현할 수 없습니다.  
  
 *Windows_collation_name* 에 대 한 데이터 정렬 이름는 [Windows 데이터 정렬 이름](../../t-sql/statements/windows-collation-name-transact-sql.md)합니다.  
  
 *SQL_collation_name* 에 대 한 데이터 정렬 이름는 [SQL Server 데이터 정렬 이름](../../t-sql/statements/sql-server-collation-name-transact-sql.md)합니다.  
  
 데이터베이스 정의 수준에서 데이터 정렬을 적용하면 COLLATE 절에서 Windows 유니코드 전용 데이터 정렬을 사용할 수 없습니다.  
  
 **database_default**  
 COLLATE 절이 현재 데이터베이스의 데이터 정렬을 상속하도록 합니다.  
  
## <a name="remarks"></a>주의  
 COLLATE 절은 여러 수준에서 지정할 수 있습니다. 여기에는 다음과 같은 옵션이 포함됩니다.  
  
1.  데이터베이스 만들기 또는 변경  
  
     CREATE DATABASE 또는 ALTER DATABASE 문의 COLLATE 절을 사용하여 데이터베이스의 기본 데이터 정렬을 지정할 수 있습니다. 또한 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 데이터베이스를 만들 때 데이터 정렬을 지정할 수 있습니다. 데이터 정렬을 지정하지 않은 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 기본 데이터 정렬이 데이터베이스에 할당됩니다.  
  
    > [!NOTE]  
    >  Windows 유니코드 전용 데이터 정렬은 사용 하 여 COLLATE 절에 데이터 정렬을 적용 하는 **nchar**, **nvarchar**, 및 **ntext** 열 수준에서 데이터 형식 및 식 수준 데이터; 데이터베이스 또는 서버 인스턴스의 데이터 정렬을 변경 하려면 COLLATE 절과 함께 사용할 수 없습니다.  
  
2.  테이블 열 만들기 또는 변경  
  
     CREATE TABLE 또는 ALTER TABLE 문의 COLLATE 절을 사용하여 각 문자열 열에 대한 데이터 정렬을 지정할 수 있습니다. 또한 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 테이블을 만들 때 데이터 정렬을 지정할 수 있습니다. 데이터 정렬을 지정하지 않은 경우에는 데이터베이스의 기본 데이터 정렬이 열에 할당됩니다.  
  
     사용할 수도 있습니다는 `database_default` COLLATE 절에서 임시 테이블의 열 대신 연결에 대 한 현재 사용자 데이터베이스의 데이터 정렬 기본값을 사용 하도록 지정 하려면 옵션 **tempdb**합니다.  
  
3.  식의 데이터 정렬 캐스팅  
  
     COLLATE 절을 사용하여 문자 식을 특정 데이터 정렬에 적용할 수 있습니다. 문자 리터럴과 변수에는 현재 데이터베이스의 기본 데이터 정렬이 할당됩니다. 열 참조에는 열의 기본 데이터 정렬이 할당됩니다.  
  
 식별자의 데이터 정렬은 식별자가 정의된 수준에 따라 달라집니다. 로그인과 데이터베이스 이름 등 인스턴스 수준 개체의 식별자에는 인스턴스의 기본 데이터 정렬이 할당됩니다. 테이블, 뷰, 열 이름 등 데이터베이스에 있는 개체의 식별자에는 데이터베이스의 기본 데이터 정렬이 할당됩니다. 예를 들어 대/소문자만 다르고 동일한 이름인 두 테이블은 데이터 정렬이 대/소문자를 구분하는 데이터베이스에서는 만들 수 있지만 대/소문자를 구분하지 않는 데이터베이스에서는 만들 수 없습니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.  
  
 변수, GOTO 레이블, 임시 저장 프로시저 및 임시 테이블은 연결 컨텍스트를 한 데이터베이스와 연결한 경우에 만들 수 있으며 컨텍스트를 다른 데이터베이스로 전환한 경우에 참조할 수 있습니다. 변수, GOTO 레이블, 임시 저장 프로시저 및 임시 테이블의 식별자는 서버 인스턴스의 기본 데이터 정렬에 있습니다.  
  
 COLLATE 절에 대해서만 적용할 수는 **char**, **varchar**, **텍스트**, **nchar**, **nvarchar** 및 **ntext** 데이터 형식입니다.  
  
 COLLATE 사용 하 여 *collate_name* SQL Server 데이터 정렬 또는 식, 열 정의 또는 데이터베이스 정의에 적용 될 Windows 데이터 정렬의 이름을 참조 하도록 합니다. *데이터 정렬 이름* 수만 지정 된 *Windows_collation_name* 또는 *SQL_collation_name* 하며 매개 변수는 리터럴 값을 포함 해야 합니다. *데이터 정렬 이름* 변수나 식으로 표현할 수 없습니다.  
  
 데이터 정렬은 설치할 때를 제외하고 일반적으로 데이터 정렬 이름으로 식별됩니다. 설치할 때는 Windows 데이터 정렬에 대해 루트 데이터 정렬 지정자(데이터 정렬 로캘)를 지정한 다음 대소문자와 악센트를 구분하거나 구분하지 않는 정렬 옵션을 지정합니다.  
  
 시스템 함수를 실행할 수 [fn_helpcollations](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) Windows 데이터 정렬 및 SQL Server 데이터 정렬에 대 한 모든 유효한 데이터 정렬 이름의 목록을 검색 하려면:  
  
```  
SELECT name, description  
FROM fn_helpcollations();  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 해당 운영 체제에서 지원되는 코드 페이지만 지원할 수 있습니다. 데이터 정렬을 기반으로 하는 동작을 수행할 때마다 참조된 개체가 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬은 시스템에서 실행 중인 운영 체제가 지원하는 코드 페이지를 사용해야 합니다. 여기에는 다음과 같은 동작이 포함됩니다.  
  
-   데이터베이스를 만들거나 변경할 때 데이터베이스에 대한 기본 데이터 정렬 지정  
  
-   테이블을 만들거나 변경할 때 열에 대한 데이터 정렬 지정  
  
-   복원 하거나 데이터베이스, 데이터베이스의 기본 데이터 정렬 및 모든 데이터 정렬에 연결할 때 **char**, **varchar**, 및 **텍스트** 열 또는 데이터베이스에 대 한 매개 변수 운영 체제에서 지원 되어야 합니다.  
  
     코드 페이지 변환이 지원 되는 **char** 및 **varchar** 데이터 형식에 대 한 **텍스트** 데이터 형식입니다. 코드 페이지 변환 중 데이터가 손실되어도 보고되지 않습니다.  
  
 지정 된 데이터 정렬 또는 참조 된 개체가 사용 되는 데이터 정렬에는 Windows에서 지원 되지 않습니다 코드 페이지를 사용 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류를 표시 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-specifying-collation-during-a-select"></a>1. 선택 중 데이터 정렬 지정  
 다음 예에서는 간단한 테이블을 만든 후 행 4개를 삽입합니다. 그런 다음 테이블에서 데이터를 선택할 때 두 데이터 정렬을 적용하여 `Chiapas`가 서로 다르게 정렬되는 방식을 보여 줍니다.  
  
```tsql  
CREATE TABLE Locations  
(Place varchar(15) NOT NULL);  
GO  
INSERT Locations(Place) VALUES ('Chiapas'),('Colima')  
                             , ('Cinco Rios'), ('California');  
GO  
--Apply an typical collation  
SELECT Place FROM Locations  
ORDER BY Place  
COLLATE Latin1_General_CS_AS_KS_WS ASC;  
GO  
-- Apply a Spanish collation  
SELECT Place FROM Locations  
ORDER BY Place  
COLLATE Traditional_Spanish_ci_ai ASC;  
GO  
```  

 다음은 첫 번째 쿼리의 결과입니다.  
  
 ```
 Place 
 ------------- 
 California 
 Chiapas 
 Cinco Rios 
 Colima
 ```  
  
 다음은 두 번째 쿼리의 결과입니다.  
  
 ```
 Place 
 ------------- 
 California 
 Cinco Rios 
 Colima 
 Chiapas
 ```  
  
### <a name="b-additional-examples"></a>2. 추가 예  
 사용 하는 추가 예제를 보려면 **COLLATE**, 참조 [CREATE database&#40; SQL Server transact-sql&#41; ](../../t-sql/statements/create-database-sql-server-transact-sql.md) 예제 **G. 데이터베이스 만들기 및 데이터 정렬 이름과 옵션 지정**, 및 [ALTER table&#40; Transact SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md) 예제 **열 데이터 정렬 변경 V.**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)   
 [데이터 정렬 선행 규칙&#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [상수 &#40; Transact SQL &#41;](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [테이블 &#40; Transact SQL &#41;](../../t-sql/data-types/table-transact-sql.md)  
  
  
