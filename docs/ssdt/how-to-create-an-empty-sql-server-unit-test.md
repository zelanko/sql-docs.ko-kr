---
title: 빈 SQL Server 단위 테스트 만들기
description: SQL Server 단위 테스트를 만드는 방법을 알아봅니다. 다른 테스트에서 사용하는 것과 동일한 TestInitialize 및 TestCleanup 스크립트를 사용하는 방법과 다른 스크립트를 사용하는 방법을 확인합니다.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.unittesting.createtest
ms.assetid: b6f3cd5a-3389-42d6-a93f-97b3ddf31b95
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 30869fbd4c9a57c068b56d638495cce76ac23789
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988697"
---
# <a name="how-to-create-an-empty-sql-server-unit-test"></a>방법: 빈 SQL Server 단위 테스트 만들기

데이터베이스 개체에 대한 변경 내용이 기존 기능을 중단하지 않는지 확인하기 위해서는 데이터베이스 프로젝트에 단위 테스트를 포함합니다. 다음 절차에서는 데이터베이스 개체에 대한 SQL Server 단위 테스트를 만드는 방법에 대해 설명합니다. SQL Server Data Tools에는 데이터베이스 함수, 트리거 및 저장 프로시저에 대한 추가 지원 기능이 포함되어 있습니다. 자세한 내용은 [방법: 함수, 트리거 및 저장 프로시저에 대한 SQL Server 단위 테스트 만들기](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)를 참조하세요.  
  
첫 번째 절차를 사용하여 SQL Server 단위 테스트를 만들 때는 테스트 프로젝트가 없을 경우 자동으로 만들어집니다. 테스트 프로젝트가 이미 있으면 이러한 프로젝트 중 하나에 새 테스트를 추가하거나 새 테스트 프로젝트를 만들도록 선택할 수 있습니다. 테스트 프로젝트에 대한 자세한 내용은 [방법: SQL Server 데이터베이스 단위 테스트용 테스트 프로젝트 만들기](../ssdt/how-to-create-a-test-project-for-sql-server-database-unit-testing.md)를 참조하세요.  
  
SQL Server 단위 테스트를 만들기 위한 두 가지 옵션은 다음과 같습니다.  
  
-   새 테스트 클래스 내에 새 SQL Server 단위 테스트를 만듭니다.  
  
    특정 테스트 클래스 내의 모든 SQL Server 단위 테스트는 동일한 TestInitialize 및 TestCleanup 스크립트를 사용합니다. 단위 테스트에서 다른 단위 테스트와 다른 TestInitialize 및 TestCleanup 스크립트를 사용하도록 하려면 새 테스트 클래스를 만듭니다. 자세한 내용은 [SQL Server 단위 테스트의 스크립트](../ssdt/scripts-in-sql-server-unit-tests.md)를 참조하세요.  
  
-   기존 테스트 클래스 내에 새 SQL Server 단위 테스트를 만듭니다.  
  
    단위 테스트에서 클래스 내의 다른 단위 테스트와 동일한 TestInitialize 및 TestCleanup 스크립트를 사용할 경우 이 옵션을 선택합니다.  
  
### <a name="to-create-a-sql-server-unit-test-inside-a-new-test-class"></a>새 테스트 클래스 내에 SQL Server 단위 테스트를 만들려면  
  
1.  **테스트** 메뉴에서 **새 테스트**를 클릭합니다.  
  
    **새 테스트 추가** 대화 상자가 나타납니다.  
  
2.  **템플릿**에서 **SQL Server 단위 테스트**를 클릭합니다.  
  
3.  **테스트 이름** 아래에 테스트 이름을 입력합니다.  
  
4.  **테스트 프로젝트에 추가**에서 이 테스트를 추가할 기존 테스트 프로젝트를 선택합니다. 테스트 프로젝트가 없거나 새 테스트 프로젝트를 만들려는 경우 **새 <language> 테스트 프로젝트 만들기**를 선택합니다.  
  
5.  **확인**을 클릭합니다.  
  
    테스트 프로젝트가 새 프로젝트인 경우 **새 테스트 프로젝트** 대화 상자가 나타납니다. 프로젝트 이름을 지정하고 **확인**을 클릭합니다.  
  
    테스트 프로젝트가 새 프로젝트이거나 아직 구성되지 않은 경우 **SQL Server 테스트 구성 <ProjectName>** 대화 상자가 나타납니다. 이 대화 상자에서는 테스트 프로젝트에 대해 다음 정보를 구성할 수 있습니다.  
  
    -   테스트 실행에 사용되는 데이터베이스 연결  
  
    -   테스트 결과의 유효성을 검사하고, 데이터베이스를 배포하고, 데이터를 생성하는 데 사용되는 데이터베이스 연결  
  
    -   단위 테스트를 실행하기 전 지정된 프로젝트 구성에 대한 데이터베이스 프로젝트 및 관련된 스키마 변경 내용의 자동 배포  
  
    자세한 내용은 [방법: SQL Server 단위 테스트 실행 구성](../ssdt/how-to-configure-sql-server-unit-test-execution.md)을 참조하세요.  
  
6.  프로젝트 구성 정보를 제공하고 **확인**을 클릭합니다.  
  
    \- 또는-  
  
    테스트 프로젝트를 구성하지 않고 단위 테스트를 만들려면 **취소**를 클릭합니다.  
  
    **SQL Server 단위 테스트 디자이너**에 빈 테스트가 나타납니다. 테스트 프로젝트를 만들기 위해 지정한 언어에 따라 Visual Basic 또는 Visual C\# 소스 코드 파일이 테스트 프로젝트에 추가됩니다. 이 파일에는 사용자가 바로 전에 만든 단위 테스트를 위해 SQL Server Data Tools에서 생성하는 SQL Server 단위 테스트 클래스가 포함됩니다. 이 테스트 클래스에는 SQL Server 단위 테스트 디자이너 또는 코드를 통해 테스트 클래스의 새 테스트 메서드로 추가할 수 있는 하나 이상의 SQL Server 단위 테스트가 포함될 수 있습니다.  
  
    다음을 수행하여 다른 테스트를 추가할 수도 있습니다.  
  
    -   **솔루션 탐색기**에서 테스트 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**, **새 테스트** 및 **SQL Server 단위 테스트**를 차례로 선택합니다.  
  
    -   SQL Server 개체 탐색기에서 [단위 테스트 만들기]를 선택합니다.  
  
    **솔루션 탐색기**에서 이 파일을 선택하면 기본적으로 SQL Server 단위 테스트 디자이너에 파일이 표시됩니다. 코드를 보거나 단위 테스트에 기능을 추가하도록 사용자 지정하려면 파일을 선택하고, 마우스 오른쪽 단추로 클릭한 후 **코드 보기**를 선택합니다.  
  
### <a name="to-create-a-sql-server-unit-test-inside-an-existing-test-class"></a>기존 테스트 클래스 내에 SQL Server 단위 테스트를 만들려면  
  
1.  **SQL Server 단위 테스트 디자이너**에서 기존 SQL Server 단위 테스트 클래스를 엽니다. **솔루션 탐색기**에서SQL Server 단위 테스트 소스 코드 파일을 두 번 클릭하여 **SQL Server 단위 테스트 디자이너**에 액세스할 수 있습니다.  
  
2.  탐색 모음에서 더하기( **+** ) 기호를 클릭하여 **단위 테스트 이름 지정** 대화 상자를 표시합니다.  
  
3.  이름을 입력하고 **확인**을 클릭합니다.  
  
    새 SQL Server 단위 테스트는 탐색 모음의 드롭다운 목록에서 사용할 수 있습니다. 또한 테스트 클래스에 새 테스트 메서드로도 추가됩니다. 코드에서 테스트 메서드를 보려면 클래스 파일을 선택하고, 마우스 오른쪽 단추로 클릭한 후 **코드 보기**를 선택합니다. 현재 테스트 클래스 파일의 이름은 **SQL Server 단위 테스트 디자이너** 상단의 탭에 표시됩니다.  
  
테스트 프로젝트를 구성하고 단위 테스트를 만든 후의 단계는 다음과 같습니다.  
  
-   Transact\- SQL 테스트 스크립트를 추가합니다.  
  
-   테스트 전 및 테스트 후 작업을 정의합니다.  
  
-   스크립트 결과를 확인하기 위한 테스트 조건 또는 다른 어설션 문을 추가합니다.  
  
> [!NOTE]  
> 결과 불충분 테스트 조건은 모든 테스트에 추가되는 기본 조건입니다. 이 테스트 조건은 테스트 확인이 구현되지 않았음을 나타내기 위해 포함됩니다. 이 테스트 조건은 다른 테스트 조건을 추가한 후 테스트에서 삭제합니다. 자세한 내용은 [방법: 데이터베이스 단위 테스트에 테스트 조건 추가](/previous-versions/visualstudio/visual-studio-2010/aa833242(v=vs.100))를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[방법: SQL Server 단위 테스트 실행](../ssdt/how-to-run-sql-server-unit-tests.md)  
[SQL Server 단위 테스트 만들기 및 정의](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[단위 테스트 만들기](/previous-versions/visualstudio/visual-studio-2008/ms182523(v=vs.90))  
