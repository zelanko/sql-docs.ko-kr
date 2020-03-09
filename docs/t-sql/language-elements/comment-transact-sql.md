---
title: --(주석)(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- --_TSQL
- Comment
- --
dev_langs:
- TSQL
helpviewer_keywords:
- nonexecuting text strings [SQL Server]
- remarks [SQL Server]
- -- (comment character)
- comments [SQL Server]
ms.assetid: 676ea8c2-52c1-4ef6-9354-320f1a091153
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d7e9aaab99194646874c0823abb61100cdc524aa
ms.sourcegitcommit: 639842f0b70e8c2c9ad5e86f9bfc3a4aad61a1df
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/04/2020
ms.locfileid: "78261712"
---
# <a name="---comment-transact-sql"></a>-- (주석)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  사용자가 제공하는 텍스트를 나타냅니다. 주석은 별도의 줄에 입력되고 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령줄 끝에 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 중첩될 수 있습니다. 서버는 주석을 평가하지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
-- text_of_comment  
```  
  
## <a name="arguments"></a>인수  
 *text_of_comment*  
 주석의 텍스트를 포함하는 문자열입니다.  
  
## <a name="remarks"></a>설명  
한 줄 또는 중첩된 주석에는 두 개의 하이픈( **--** )을 사용하세요. **--** 와 함께 삽입된 주석은 캐리지 리턴 문자(U+000A), 줄 바꿈 문자(U+000D) 또는 둘의 조합으로 지정된 새 줄로 종료됩니다. 주석의 길이에는 제한이 없습니다. 다음 표에서는 텍스트를 주석으로 처리하거나 텍스트의 주석 처리를 제거하는 데 사용할 수 있는 바로 가기 키를 나열합니다.
  
|작업|Standard|  
|------------|--------------|  
|선택한 텍스트를 주석으로 만들기|Ctrl+K, Ctrl+C|  
|선택한 텍스트의 주석 처리 제거|Ctrl+K, Ctrl+U|  
  
 바로 가기 키의 자세한 내용을 보려면 [SQL Server Management Studio 바로 가기 키](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)를 참조하세요.  
  
 여러 줄로 된 주석의 경우 [슬래시 별표&#40;블록 주석&#41;& #40;Transact SQL&#41;](../../t-sql/language-elements/slash-star-comment-transact-sql.md)을 참조하세요.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [흐름 제어 언어&#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)  
  
  
