---
title: '방법: SQL Server 단위 테스트에 테스트 조건 추가 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 85ba2e56-a0b2-489c-aea2-fb135cce0cfc
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 3f4dc9a023b74c104e232546ec6c4f8c2bd93919
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65103254"
---
# <a name="how-to-add-test-conditions-to-sql-server-unit-tests"></a>방법: SQL Server 단위 테스트에 테스트 조건 추가
**SQL Server 단위 테스트 디자이너**를 사용하여 SQL Server 단위 테스트에 테스트 조건을 추가할 수 있습니다. 테스트 클래스를 저장하면 해당 테스트 조건이 테스트 프로젝트에서 테스트 클래스를 포함하는 소스 코드 파일에 Visual C\# 또는 Visual Basic 코드로 자동 저장됩니다. 테스트 조건을 저장한 후에는 **SQL Server 단위 테스트 디자이너**나 해당 소스 코드 파일에서 테스트 조건을 편집할 수 있습니다.  
  
### <a name="to-add-test-conditions-to-a-sql-server-unit-test"></a>SQL Server 단위 테스트에 테스트 조건 추가  
  
1.  **SQL Server 단위 테스트 디자이너**에서 SQL Server 단위 테스트를 엽니다.  
  
    열린 테스트의 이름은 SQL Server 단위 테스트 디자이너 상단의 탐색 모음에 표시됩니다. 탐색 모음을 사용하면 테스트 클래스에 있는 여러 테스트 메서드를 선택할 수 있습니다.  
  
2.  탐색 모음에서 테스트 조건을 추가할 테스트 메서드를 클릭하거나 **일반 스크립트**를 클릭합니다.  
  
    > [!NOTE]  
    > 일반 스크립트는 특정 단위 테스트에 속하지 않고 테스트 클래스의 단위 테스트 전에 또는 후에 실행됩니다. 자세한 내용은 [SQL Server 단위 테스트의 스크립트](../ssdt/scripts-in-sql-server-unit-tests.md)를 참조하세요.  
  
3.  탐색 모음에서 테스트 조건을 추가할 Transact\-SQL 스크립트를 클릭합니다. 테스트 전, 테스트 또는 테스트 후 스크립트에 테스트 조건을 추가할 수 있습니다.  
  
    해당 테스트에 대한 Transact\-SQL 스크립트가 Transact\-SQL 편집기에 표시되고 해당 테스트 조건이 **테스트 조건** 창에 표시됩니다.  
  
4.  **테스트 조건** 선택 목록에서 테스트 조건을 클릭하고 **테스트 조건 추가**(+)를 클릭합니다.  
  
    테스트 조건이 단위 테스트 메서드에 추가됩니다.  
  
    > [!NOTE]  
    > 테스트 조건을 클릭한 후 **테스트 조건** 창에서 위쪽 및 아래쪽 화살표를 클릭하여 테스트 메서드 내에서 테스트 조건 순서를 바꿀 수 있습니다.  
  
5.  바로 전에 추가한 테스트 조건을 선택하고 **속성** 창을 확인합니다.  
  
    속성 창에서 테스트 조건을 구성합니다. 예를 들어 실행 시간 테스트 조건의 **실행 시간** 속성을 변경할 수 있습니다. 이 속성을 설정하면 Transact\-SQL 스크립트가 지정된 시간 내에 실행되지 않을 경우 테스트가 실패하도록 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트 만들기 및 정의](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[방법: 빈 SQL Server 단위 테스트 만들기](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)  
[방법: 함수, 트리거 및 저장 프로시저에 대한 SQL Server 단위 테스트 만들기](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)  
[SQL Server 단위 테스트에서 테스트 조건 사용](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)  
[SQL Server 단위 테스트의 스크립트](../ssdt/scripts-in-sql-server-unit-tests.md)  
[SQL Server 단위 테스트 결과 해석](../ssdt/interpreting-sql-server-unit-test-results.md)  
[방법: SQL Server 단위 테스트 실행](../ssdt/how-to-run-sql-server-unit-tests.md)  
  
