---
title: Transact-SQL 코드 조각 완성 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [SQL Server], completing snippets
- snippets [Transact-SQL], completing
- Transact-SQL snippets, completing
ms.assetid: a8316a58-bb57-485e-845f-84c23360314c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 19aefa1367904a2641d3584546c48f05ba807cf7
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34333354"
---
# <a name="complete-transact-sql-snippets"></a>Transact-SQL 코드 조각 완성
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드 조각을 스크립트에 삽입한 후 코드 조각의 내용을 편집하여 완전한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 만들 수 있습니다.  
  
## <a name="completing-snippets"></a>코드 조각 완성  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드 조각을 스크립트에 추가하면 삽입된 코드 조각 문에서 하나 이상의 대체 지점이 강조 표시됩니다. 마우스 포인터를 대체 지점에 놓으면 사용자가 지정할 수 있는 구문 요소에 대한 설명이 포함된 도구 설명이 나타납니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기는 원본 파일을 닫기 전까지는 코드 조각을 주변 스크립트와는 별개로 인식합니다. 대체 지점은 원본 파일을 닫을 때까지 활성 상태로 유지됩니다.  
  
 코드 조각을 통해 삽입된 템플릿 코드에 다른 구문 요소를 추가할 수도 있습니다. 예를 들어 Create Table 코드 조각 템플릿은 두 개의 열 정의를 생성합니다. 열이 둘 이상인 테이블을 만들려면 여기에 다른 열 정의를 추가해야 합니다.  
  
#### <a name="completing-the-snippet-statement"></a>코드 조각 문 완성  
  
1.  한 대체 지점에서 다음 대체 지점으로 이동하려면 Tab 키를 사용합니다. 이전 대체 지점으로 이동하려면 Shift+Tab을 사용합니다.  
  
2.  IntelliSense를 실행하려면 Ctrl+스페이스바를 누릅니다.  
  
3.  목록에서 항목을 선택하거나 원하는 대체 텍스트를 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-SQL 코드 조각 삽입](../../relational-databases/scripting/insert-transact-sql-snippets.md)   
 [코드 감싸기 Transact-SQL 조각 삽입](../../relational-databases/scripting/insert-surround-with-transact-sql-snippets.md)  
  
  
