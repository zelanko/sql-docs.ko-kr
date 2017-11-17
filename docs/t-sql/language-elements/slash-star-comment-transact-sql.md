---
title: "슬래시 별모양 주석 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- /*...*/_TSQL
- Comment
- /*...*/
dev_langs:
- TSQL
helpviewer_keywords:
- nonexecuting text strings [SQL Server]
- /*...*/ (comment)
- remarks [SQL Server]
- comments [SQL Server]
ms.assetid: 4d9ab1b2-4bbb-4c16-beb1-cafc1af7417c
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3e617c6f0108906046d6c6ea983d1bbc26082709
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="slash-star-comment-transact-sql"></a>슬래시 별모양 주석 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  사용자가 제공하는 텍스트를 나타냅니다. 사이의 텍스트는 / * 및 \*/ 서버에서 평가 되지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
/*  
text_of_comment  
*/  
```  
  
## <a name="arguments"></a>인수  
 *text_of_comment*  
 주석 텍스트입니다. 한 개 이상의 문자열로 구성됩니다.  
  
## <a name="remarks"></a>주의  
 주석은 별도의 줄 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 삽입될 수 있습니다. 여러 줄로 이루어진 주석은로 표시 되어야 합니다 / * 및 \*/ 합니다. 첫 번째 줄을 시작 하는 여러 줄로 이루어진 주석에 주로 사용 되는 스타일 규칙 /\*후속 줄은 \* \*, 하 고 끝나야 \*/ 합니다.  
  
 주석의 길이에는 제한이 없습니다.  
  
 주석의 중첩도 가능합니다. 경우는 / * 문자 패턴이 기존 주석 내에서 발생 하면 중첩 된 주석의 시작으로 처리 하 고, 따라서 닫는 데, \*/ 주석 표시가 있습니다. 닫는 주석 표시가 없으면 오류가 생성됩니다.  
  
 예를 들면 다음 코드는 오류를 생성합니다.  
  
```  
DECLARE @comment AS varchar(20);  
GO  
/*  
SELECT @comment = '/*';  
*/   
SELECT @@VERSION;  
GO   
```  
  
 오류를 해결하려면 다음과 같이 변경하세요.  
  
```  
DECLARE @comment AS varchar(20);  
GO  
/*  
SELECT @comment = '/*';  
*/ */  
SELECT @@VERSION;  
GO  
  
```  
  
## <a name="examples"></a>예  
 다음 예에서는 코드 섹션에서 수행되는 작업을 설명하기 위해 주석을 사용합니다.  
  
```  
USE AdventureWorks2012;  
GO  
/*  
This section of the code joins the Person table with the Address table,   
by using the Employee and BusinessEntityAddress tables in the middle to   
get a list of all the employees in the AdventureWorks2012 database   
and their contact information.  
*/  
SELECT p.FirstName, p.LastName, a.AddressLine1, a.AddressLine2, a.City, a.PostalCode  
FROM Person.Person AS p  
JOIN HumanResources.Employee AS e ON p.BusinessEntityID = e.BusinessEntityID   
JOIN Person.BusinessEntityAddress AS ea ON e.BusinessEntityID = ea.BusinessEntityID  
JOIN Person.Address AS a ON ea.AddressID = a.AddressID;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [-&#40; 설명 &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/comment-transact-sql.md)   
 [흐름 제어 언어 &#40; Transact SQL &#41;](~/t-sql/language-elements/control-of-flow.md)  
  
  


