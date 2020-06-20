---
title: 옵션 (텍스트 편집기-Transact-sql-IntelliSense) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.SQL.Advanced
- VS.ToolsOptionsPages.Text_Editor.SQL_Server_Tools.Advanced
dev_langs:
- TSQL
ms.assetid: 1855d916-5bf9-4d94-b0fb-9f9bb05ff950
author: rothja
ms.author: jroth
ms.openlocfilehash: b130152a8817550b32eb3c923c24feaea96bf5b0
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929754"
---
# <a name="options-text-editor-transact-sql-intellisense"></a>옵션 (텍스트 편집기-Transact-sql-IntelliSense)
  **옵션** 대화 상자를 사용하여 [!INCLUDE[ssDE](../includes/ssde-md.md)] 쿼리 편집기에 대한 IntelliSense 설정을 변경할 수 있습니다. 이러한 설정은 **도구** 메뉴에서 **옵션**을 클릭하고 **텍스트 편집기** 폴더와 **Transact-SQL** 폴더를 차례로 확장한 다음 **고급**을 클릭하면 볼 수 있습니다.  
  
## <a name="transact-sql-intellisense-settings"></a>Transact-SQL IntelliSense 설정  
 [!INCLUDE[ssDE](../includes/ssde-md.md)] 쿼리 편집기에 대한 IntelliSense 옵션을 지정합니다.  
  
### <a name="enable-intellisense"></a>IntelliSense 사용  
 IntelliSense 기능을 사용하도록 설정합니다. 이 상자가 선택되어 있지 않으면 특정 IntelliSense 옵션을 사용할 수 없습니다. 이 확인란은 기본적으로 선택되어 있습니다.  
  
 **오류에 밑줄 표시**  
 쿼리 창에서 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에 있는 구문 및 의미 체계 오류를 식별합니다. 모든 오류와 경고는 빨간색으로 표시됩니다. 오류와 경고는 IntelliSense를 구현한 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에 대해서만 지원됩니다. 이 확인란은 기본적으로 선택되어 있습니다.  
  
 **개요 문 표시**  
 파일을 열 때 개요 기능을 사용하도록 설정합니다. 이렇게 하면 축소 가능한 [!INCLUDE[tsql](../includes/tsql-md.md)] 코드 블록이 만들어집니다. 이 확인란은 기본적으로 선택되어 있습니다.  
  
 **최대 스크립트 크기**  
 IntelliSense 기능을 사용할 수 없게 하는 크기를 지정합니다. 스크립트가 지정된 크기를 초과하면 경고 메시지가 나타나고 해당 편집기 창에서 색 구분 기능을 제외한 모든 IntelliSense 기능을 사용할 수 없습니다. 스크립트 크기가 제한 크기 이내로 줄어들도록 텍스트를 충분히 삭제하면 IntelliSense를 다시 사용할 수 있습니다. IntelliSense를 대용량 스크립트에 사용하면 컴퓨터의 성능이 느려질 수 있습니다. 허용되는 크기는 100KB, 500KB, 1MB, 2MB 및 제한 없음입니다. 기본값은 1MB입니다.  
  
 **기본 제공 함수 이름의 대/소문자 구분**  
 완성 목록에 포함된 기본 제공 [!INCLUDE[tsql](../includes/tsql-md.md)] 함수 이름에서 대문자(예: DATEADD) 또는 소문자(예: dateadd) 중 어떤 문자를 사용할 것인지를 지정합니다. 사용 중인 [!INCLUDE[tsql](../includes/tsql-md.md)] 코딩 규칙에 가장 적합한 옵션을 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [IntelliSense &#40;SQL Server Management Studio&#41;문제 해결](../relational-databases/scripting/troubleshooting-intellisense.md)  
  
  
