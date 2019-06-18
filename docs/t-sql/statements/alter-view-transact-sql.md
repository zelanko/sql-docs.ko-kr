---
title: ALTER VIEW(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/25/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_VIEW_TSQL
- ALTER VIEW
dev_langs:
- TSQL
helpviewer_keywords:
- indexed views [SQL Server], modifying
- views [SQL Server], modifying
- modifying views
- ALTER VIEW statement
ms.assetid: 03eba220-13e2-49e3-bd9d-ea9df84dc28c
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 780d2929180657afc705335ff2110b9f3f9cc6c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62664717"
---
# <a name="alter-view-transact-sql"></a>ALTER VIEW(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  인덱싱된 뷰를 포함하여 이전에 만든 뷰를 수정합니다. ALTER VIEW는 종속된 저장 프로시저 또는 트리거에 영향을 주지 않으며 사용 권한을 변경하지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ALTER VIEW [ schema_name . ] view_name [ ( column [ ,...n ] ) ]   
[ WITH <view_attribute> [ ,...n ] ]   
AS select_statement   
[ WITH CHECK OPTION ] [ ; ]  
  
<view_attribute> ::=   
{   
    [ ENCRYPTION ]  
    [ SCHEMABINDING ]  
    [ VIEW_METADATA ]       
}   
```  
  
## <a name="arguments"></a>인수  
 *schema_name*  
 뷰가 속한 스키마의 이름입니다.  
  
 *view_name*  
 변경할 뷰입니다.  
  
 *column*  
 지정된 뷰에 포함될 하나 이상의 열 이름을 쉼표로 구분하여 지정합니다.  
  
> [!IMPORTANT]  
>  열 사용 권한을 유지하려면 ALTER VIEW 실행 전후에 동일한 열 이름을 사용해야 합니다.  
  
> [!NOTE]  
>  뷰에 대한 열에서 열 이름에 대한 사용 권한은 기본 데이터의 원본에 상관없이 CREATE VIEW 또는 ALTER VIEW 문에 적용할 수 있습니다. 예를 들어 CREATE VIEW 문에서 **SalesOrderID** 열에 사용 권한이 부여된 경우 ALTER VIEW 문에서 **SalesOrderID** 열의 이름을 **OrderRef**로 변경할 수 있으며 이때 **SalesOrderID**를 사용하는 뷰와 관련된 권한은 계속 유지됩니다.  
  
 ENCRYPTION  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]까지  
  
 ALTER VIEW 문의 텍스트가 포함된 [sys.syscomments](../../relational-databases/system-compatibility-views/sys-syscomments-transact-sql.md) 항목을 암호화합니다. WITH ENCRYPTION은 뷰가 SQL Server 복제의 일부로 게시되는 것을 방지합니다.  
  
 SCHEMABINDING  
 기본 테이블의 스키마에 뷰를 바인딩합니다. SCHEMABINDING을 지정하면 뷰 정의에 영향을 줄 수 있는 경우에는 기본 테이블을 수정할 수 없습니다. 수정할 테이블의 종속성을 제거하려면 우선 뷰 정의 자체를 수정 또는 삭제해야 합니다. SCHEMABINDING을 사용하는 경우 _select\_statement_에 참조되는 테이블, 뷰 또는 사용자 정의 함수의 두 부분으로 구성된 이름(_schema_ **.** _object_)이 있어야 합니다. 참조된 개체는 모두 같은 데이터베이스에 있어야 합니다.  
  
 SCHEMABINDING 절로 만든 뷰에서 사용하는 뷰 또는 테이블은 뷰가 삭제되거나 변경되어 스키마 바인딩이 더 이상 존재하지 않는 경우에만 삭제할 수 있습니다. 그렇지 않으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 오류가 발생합니다. 또한 ALTER TABLE 문이 뷰 정의에 영향을 미치는 경우에 스키마 바인딩이 있는 뷰에서 사용하는 테이블에 ALTER TABLE 문을 실행하면 실패합니다.  
  
 VIEW_METADATA  
 뷰를 참조하는 쿼리에 대해 찾아보기 모드 메타데이터가 요청된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 기본 테이블 대신 뷰에 대한 메타데이터 정보를 DB-Library, ODBC 및 OLE DB API에 반환하도록 지정합니다. 찾아보기 모드 메타데이터는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스가 클라이언트 쪽 DB-Library, ODBC 및 OLE DB API에 반환하는 추가 메타데이터입니다. 이 메타데이터를 사용하면 클라이언트 쪽 API가 업데이트할 수 있는 클라이언트 쪽 커서를 구현할 수 있습니다. 찾아보기 모드 메타데이터에는 결과 집합의 열이 속한 기본 테이블에 대한 정보가 포함되어 있습니다.  
  
 VIEW_METADATA를 사용하여 만든 뷰의 경우 찾아보기 모드 메타데이터는 결과 집합의 뷰에서 열을 설명할 때 기본 테이블 이름 대신 뷰 이름을 반환합니다.  
  
 WITH VIEW_METADATA를 사용하여 뷰를 만든 경우 뷰에 INSERT 또는 UPDATE INSTEAD OF 트리거가 있으면 뷰의 모든 열(**timestamp** 제외)을 업데이트할 수 있습니다. 자세한 내용은 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)을 참조하세요.  
  
 AS  
 뷰가 수행할 동작입니다.  
  
 *select_statement*  
 뷰를 정의하는 SELECT 문입니다.  
  
 WITH CHECK OPTION  
 뷰에 대해 실행된 모든 데이터 수정 명령문이 *select_statement* 내의 기준 집합을 준수하도록 설정합니다.  
  
## <a name="remarks"></a>Remarks  
 ALTER TRIGGER에 대한 자세한 내용은 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)의 설명 부분을 참조하세요.  
  
> [!NOTE]  
>  이전 뷰 정의를 WITH ENCRYPTION 또는 CHECK OPTION을 사용하여 만든 경우 이러한 옵션은 ALTER VIEW에 포함된 경우에만 설정됩니다.  
  
 현재 사용 중인 뷰를 ALTER VIEW를 사용하여 수정하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 해당 뷰에 대한 배타적 스키마 잠금을 얻습니다. 잠금이 부여되고 현재 뷰를 사용 중인 사용자가 없으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 프로시저 캐시에서 뷰의 복사본을 모두 삭제합니다. 해당 뷰를 참조하는 기존 계획은 캐시에 남아 있지만 다음 호출 시 다시 컴파일됩니다.  
  
 인덱싱된 뷰에도 ALTER VIEW를 적용할 수 있지만 ALTER VIEW는 뷰에 대한 모든 인덱스를 무조건 삭제합니다.  
  
## <a name="permissions"></a>사용 권한  
 ALTER VIEW를 실행하려면 최소 OBJECT에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 모든 직원 및 이들의 채용일을 포함하는 `EmployeeHireDate`라는 뷰를 만듭니다. 해당 뷰에 권한이 부여되었지만 채용일이 특정 날짜 이전인 직원을 선택하도록 요구 사항이 변경됩니다. 그러면 `ALTER VIEW`를 사용하여 기존 뷰를 바꿉니다.  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE VIEW HumanResources.EmployeeHireDate  
AS  
SELECT p.FirstName, p.LastName, e.HireDate  
FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
ON e.BusinessEntityID = p.BusinessEntityID ;  
GO  
  
```  
  
 뷰는 `2002`년 이전에 채용된 직원만 포함하도록 변경되어야 합니다. ALTER VIEW를 사용하지 않고 대신 해당 뷰를 삭제하거나 새로 만든 경우 이전에 사용한 GRANT 문 및 이 뷰와 관련된 권한을 처리한 다른 모든 문을 다시 입력해야 합니다.  
  
```  
ALTER VIEW HumanResources.EmployeeHireDate  
AS  
SELECT p.FirstName, p.LastName, e.HireDate  
FROM HumanResources.Employee AS e JOIN Person.Person AS p  
ON e.BusinessEntityID = p.BusinessEntityID  
WHERE HireDate < CONVERT(DATETIME,'20020101',101) ;  
GO  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [DROP VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/drop-view-transact-sql.md)   
 [저장 프로시저 만들기](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [게시 데이터베이스의 스키마 변경](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  
