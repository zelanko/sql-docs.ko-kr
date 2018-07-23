---
title: '방법: 편집할 SQL Server 단위 테스트 열기 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c6af1b12-54cd-42f9-b2ef-7164f8078323
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1c2a7dfd1d5e9bafd023d2289c801758e9670629
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086625"
---
# <a name="how-to-open-a-sql-server-unit-test-to-edit"></a>방법: 편집할 SQL Server 단위 테스트 열기
SQL Server 단위 테스트를 만든 후에는 **SQL Server 단위 테스트 디자이너**를 사용하여 Transact\-SQL 문과 테스트 조건을 추가합니다. 디자이너를 사용하여 만든 테스트는 Visual C# 또는 Visual Basic 코드를 생성합니다. 이 코드는 테스트를 실행할 때 실행됩니다.  
  
테스트가 만족스러운 경우 테스트를 있는 그대로 실행할 수 있습니다. 이 단위 테스트에 기능을 더 추가하려면 테스트의 코드를 편집하면 됩니다. 이 코드는 테스트 프로젝트의 .cs 또는.vb 파일에 있습니다. 자세한 내용은 [SQL Server 단위 테스트 파일](../ssdt/sql-server-unit-test-files.md)을 참조하세요. 새 테스트 조건을 만들어 테스트를 사용자 지정할 수도 있습니다. 자세한 내용은 [방법: 데이터베이스 단위 테스트 디자이너용 테스트 조건 만들기(Visual Studio 2010)](http://msdn.microsoft.com/library/aa833409(VS.100).aspx)를 참조하세요.  
  
> [!NOTE]  
> .cs 또는 .vb 파일을 편집하여 테스트 메서드를 삭제하더라도 **SQL Server 단위 테스트 디자이너**에는 해당 테스트 메서드가 여전히 나타납니다. 테스트 클래스의 InitializeComponent 메서드에는 여전히 해당 테스트의 멤버 변수가 포함되어 있기 때문에 이러한 상황이 발생합니다. 디자이너에 테스트가 나타나더라도 해당 테스트의 코드는 더 이상 존재하지 않으므로 해당 테스트를 실행할 수는 없습니다. 이 테스트의 테스트 메서드를 다시 생성하려면 편집기에서 Transact\-SQL을 편집한 후 .cs 또는 .vb 테스트 파일을 저장하거나 테스트 프로젝트를 다시 빌드합니다.  
  
### <a name="to-open-the-source-code-file-of-a-sql-server-unit-test-from-solution-explorer"></a>솔루션 탐색기에서 SQL Server 단위 테스트의 소스 코드 파일을 열려면  
  
-   **솔루션 탐색기**에서 SQL Server 단위 테스트가 포함된 소스 코드 파일을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.  
  
    파일이 열리면 단위 테스트의 테스트 메서드가 Visual Studio의 주 편집 창에 나타납니다.  
  
### <a name="to-open-the-source-code-file-of-a-sql-server-unit-test-from-the-test-view-window-visual-studio-2010"></a>[테스트 뷰] 창에서 SQL Server 단위 테스트의 소스 코드 파일을 열려면(Visual Studio 2010)  
  
1.  단위 테스트를 실행합니다. 자세한 내용은 [연습: SQL Server 단위 테스트 만들기 및 실행](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)에서 “SQL Server 단위 테스트 실행” 섹션을 참조하세요.  
  
2.  [테스트 뷰] 창에서 테스트를 마우스 오른쪽 단추로 클릭하고 **테스트 열기**를 클릭합니다.  
  
    파일이 열리면 단위 테스트의 테스트 메서드가 Visual Studio의 주 편집 창에 나타납니다.  
  
### <a name="to-open-the-source-code-file-of-a-sql-server-unit-test-from-the-test-view-window-visual-studio-2012"></a>[테스트 뷰] 창에서 SQL Server 단위 테스트의 소스 코드 파일을 열려면(Visual Studio 2012)  
  
1.  단위 테스트를 실행합니다. 자세한 내용은 [연습: SQL Server 단위 테스트 만들기 및 실행](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)에서 “SQL Server 단위 테스트 실행” 섹션을 참조하세요.  
  
2.  테스트 탐색기 창에서 단위 테스트 원본 코드 파일의 이름을 클릭합니다.  
  
    파일이 열리면 단위 테스트의 테스트 메서드가 Visual Studio의 주 편집 창에 나타납니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트 만들기 및 정의](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[SQL Server 단위 테스트를 사용하여 데이터베이스 코드 확인](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
