---
title: 코드 감싸기 Transact-SQL 조각 삽입 | Microsoft 문서
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
- snippets [Transact-SQL], surround with
- IntelliSense [SQL Server], surround with snippets
- Transact-SQL snippets, surround with
ms.assetid: 5b5a8c6c-968e-4361-a7f5-9e2ac186d927
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 700bb80820ffe413158d4e728feb5673e7e7dcfa
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34333694"
---
# <a name="insert-surround-with-transact-sql-snippets"></a>코드 감싸기 Transact-SQL 조각 삽입
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  코드 감싸기 조각은 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 BEGIN, IF 또는 WHILE 블록으로 묶을 때 시작 지점으로 사용할 수 있는 템플릿입니다.  
  
## <a name="inserting-surround-with-snippets"></a>코드 감싸기 조각 삽입  
 코드 감싸기 조각은 바로 가기 키, **편집** 메뉴 및 상황에 맞는 메뉴의 세 가지 방법 중 하나로 시작할 수 있습니다.  
  
 코드 조각을 삽입한 후에는 올바른 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 되도록 대체 텍스트를 변경해야 합니다. 자세한 내용은 [Transact-SQL 코드 조각 완성](../../relational-databases/scripting/complete-transact-sql-snippets.md)을 참조하세요.  
  
#### <a name="to-insert-a-surround-with-snippet"></a>코드 감싸기 조각을 삽입하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창에서 블록에 포함할 일련의 문을 선택합니다.  
  
2.  다음 세 가지 방법 중 하나를 사용하여 코드 감싸기 조각 목록을 표시합니다.  
  
    -   Ctrl+K, Ctrl+S를 누릅니다.  
  
    -   **편집** 메뉴에서 **IntelliSense**를 가리킨 다음 **코드 감싸기** 명령을 선택합니다.  
  
    -   선택한 텍스트를 마우스 오른쪽 단추로 클릭한 다음 상황에 맞는 메뉴에서 **코드 감싸기** 명령을 선택합니다.  
  
3.  마우스를 사용하거나 코드 조각 이름을 입력하고 Tab 키 또는 Enter 키를 눌러 목록에서 코드 조각(BEGIN, IF 또는 WHILE)의 이름을 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-SQL 코드 조각 삽입](../../relational-databases/scripting/insert-transact-sql-snippets.md)  
  
  
