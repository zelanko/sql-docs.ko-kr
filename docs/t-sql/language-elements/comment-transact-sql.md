---
title: "-(주석) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- --_TSQL
- Comment
- --
dev_langs: TSQL
helpviewer_keywords:
- nonexecuting text strings [SQL Server]
- remarks [SQL Server]
- -- (comment character)
- comments [SQL Server]
ms.assetid: 676ea8c2-52c1-4ef6-9354-320f1a091153
caps.latest.revision: "43"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a5615aa149b6f7a36b962550fa6094d3badae0a2
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="---comment-transact-sql"></a>-- (주석)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  사용자가 제공하는 텍스트를 나타냅니다. 주석은 별도의 줄에 입력되고 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령줄 끝에 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 중첩될 수 있습니다. 서버는 주석을 평가하지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
-- text_of_comment  
```  
  
## <a name="arguments"></a>인수  
 *text_of_comment*  
 주석의 텍스트를 포함하는 문자열입니다.  
  
## <a name="remarks"></a>주의  
 한 줄 또는 중첩된 주석에는 두 개의 하이픈(--)을 사용하세요. --으로 삽입된 주석은 새 줄 문자로 종료됩니다. 주석의 길이에는 제한이 없습니다. 다음 표에서는 텍스트를 주석으로 처리하거나 텍스트의 주석 처리를 제거하는 데 사용할 수 있는 바로 가기 키를 나열합니다.  
  
|동작|Standard|  
|------------|--------------|  
|선택한 텍스트를 주석으로 만들기|Ctrl+K, Ctrl+C|  
|선택한 텍스트의 주석 처리 제거|Ctrl+K, Ctrl+U|  
  
 바로 가기 키에 대 한 자세한 내용은 참조 [SQL Server Management Studio Keyboard Shortcuts](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md)합니다.  
  
 여러 줄로 된 주석에 대 한 참조 [슬래시 별 &#40; 블록 주석 &#41; &#40; Transact SQL &#41; ](../../t-sql/language-elements/slash-star-comment-transact-sql.md).  
  
## <a name="examples"></a>예  
 다음 예에서는 -- 주석 달기 문자를 사용하는 방법을 보여 줍니다.  
  
```  
-- Choose the AdventureWorks2012 database.  
USE AdventureWorks2012;  
GO  
-- Choose all columns and all rows from the Address table.  
SELECT *  
FROM Person.Address  
ORDER BY PostalCode ASC; -- We do not have to specify ASC because   
-- that is the default.  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [흐름 제어 언어 &#40; Transact SQL &#41;](~/t-sql/language-elements/control-of-flow.md)  
  
  
