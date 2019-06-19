---
title: 슬래시 별(주석 블록)(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 662aaa76f7af8a45513219af63c66fe3a65bede6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65981657"
---
# <a name="slash-star-block-comment-transact-sql"></a>슬래시 별(주석 블록)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]


  사용자가 제공하는 텍스트를 나타냅니다. /* 및 \*/ 사이의 텍스트는 서버에서 평가되지 않습니다.  
  
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
  
## <a name="remarks"></a>Remarks  
 주석은 별도의 줄 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 삽입될 수 있습니다. 여러 줄로 이루어진 주석은 /* 및 \*/로 표시되어야 합니다. 여러 줄로 이루어진 주석에 자주 사용되는 스타일 규칙은 첫 번째 줄을 /\*로 시작하고, 후속 줄은 \*\*로 시작하며, \*/로 끝나는 것입니다.  
  
 주석의 길이에는 제한이 없습니다.  
  
 주석의 중첩도 가능합니다. /* 문자 패턴이 기존 주석 내의 아무 곳에서 발생하면 중첩된 주석의 시작으로 처리되므로 \*/(주석 닫기 표시)가 필요합니다. 닫는 주석 표시가 없으면 오류가 생성됩니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [--&#40;주석&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/comment-transact-sql.md)   
 [흐름 제어 언어&#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)  
  
  

