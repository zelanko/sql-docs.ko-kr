---
title: '방법: SQL Server 단위 테스트 실행 구성 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e0179429-13ce-4d23-ae27-e6419de0a575
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: df35cb91b59e9ea4734864ee9f839b2eef983eaa
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086305"
---
# <a name="how-to-configure-sql-server-unit-test-execution"></a>방법: SQL Server 단위 테스트 실행 구성
테스트 프로젝트를 구성하여 SQL Server 단위 테스트가 실행되는 방법의 여러 측면을 제어하는 몇 가지 설정을 지정할 수 있습니다. 이러한 구성 설정은 테스트 프로젝트의 app.config 파일에 저장됩니다. 이 파일을 직접 편집하는 경우 테스트 구성 대화 상자에 새 값이 나타납니다.  
  
솔루션에는 여러 테스트 프로젝트가 포함될 수 있습니다. 각 테스트 프로젝트는 하나의 app.config 파일(즉, 하나의 구성 설정 집합)을 포함합니다. 따라서 솔루션에는 서로 다르게 실행되도록 구성된 여러 단위 테스트 집합(각 테스트 프로젝트별로 하나의 집합)이 포함될 수 있습니다.  
  
이러한 설정은 테스트할 데이터베이스에 테스트를 연결하는 방법과 데이터베이스 프로젝트의 스키마를 해당 데이터베이스에 배포하는 방법을 제어합니다.  
  
-   **데이터베이스 연결**. 이 설정을 사용하여 테스트할 데이터베이스에 연결하는 데 사용되는 연결 문자열을 지정할 수 있습니다. 자세한 내용은 [연결 문자열 지정](#SpecifyConnectionStrings)을 참조하세요.  
  
-   **스키마 배포**. 데이터베이스 프로젝트는 데이터베이스의 오프라인 표현입니다. 데이터베이스 프로젝트는 데이터베이스 개체의 구조를 나타내지만 데이터를 포함하지는 않습니다. 데이터베이스 프로젝트에서 스키마를 변경한 후에 실제 데이터베이스에서 해당 스키마를 테스트할 수 있습니다. 스키마 배포 단계에서는 테스트할 데이터베이스 개체가 데이터베이스 프로젝트에서 테스트를 실행할 데이터베이스에 복사됩니다. 스키마 배포에 대한 자세한 내용은 [데이터베이스 스키마 배포](#DeployingDBSchema)를 참조하세요.  
  
    > [!NOTE]  
    > 테스트는 솔루션 폴더에서 실행되지 않고 로컬 하드 디스크에 있는 별도의 폴더에서 실행됩니다. 테스트 배포의 여러 측면을 구성할 수 있지만 일반적으로 단위 테스트에 대해서는 이를 구성할 필요가 없습니다. 테스트 배포에 대한 자세한 내용은 [테스트 실행](http://msdn.microsoft.com/library/dd286680(VS.100).aspx)을 참조하세요.  
  
## <a name="SpecifyConnectionStrings"></a>연결 문자열 지정  
  
#### <a name="to-specify-database-connection-strings"></a>데이터베이스 연결 문자열 지정하려면  
  
1.  **솔루션 탐색기**에서SQL Server 단위 테스트 프로젝트를 마우스 오른쪽 단추로 클릭하고 **SQL Server 테스트 구성**을 클릭합니다.  
  
    **SQL Server 테스트 구성 -‘<projectname>’** 대화 상자가 표시됩니다.  
  
2.  **데이터베이스 연결** 아래에서 다음을 수행할 수 있습니다.  
  
    -   단위 테스트를 실행할 데이터베이스 연결을 클릭합니다.  
  
    -   다른 데이터베이스 연결에 대해 테스트 실행의 유효성을 검사하려는 경우 **보조 데이터 연결을 사용하여 단위 테스트 유효성 검사** 확인란을 선택하고 목록에서 데이터베이스 연결을 클릭합니다.  
  
    -   **새 연결**을 클릭하여 각 목록에 연결을 추가합니다. **연결 편집**을 클릭하여 기존 연결에 대한 설정을 수정할 수도 있습니다.  
  
    이 단계에서는 단위 테스트에서 테스트 스크립트를 실행하는 데 사용되는 `ExecutionContext` 연결 문자열을 만듭니다. 보조 연결도 지정하는 경우에는 `PrivilegedContext` 연결 문자열도 만들어집니다. 이 연결은 단위 테스트에서 테스트 스크립트 외부 데이터베이스와의 상호 작용을 테스트하는 데 사용됩니다. 자세한 내용은 [연결 문자열 및 사용 권한 개요](../ssdt/overview-of-connection-strings-and-permissions.md)를 참조하세요.  
  
3.  **확인**을 클릭하여 **SQL Server 테스트 구성 -‘<projectname>’** 대화 상자를 닫습니다.  
  
4.  테스트 프로젝트를 다시 빌드하여 구성 변경 내용을 적용합니다.  
  
## <a name="DeployingDBSchema"></a>데이터베이스 스키마 배포  
  
#### <a name="to-deploy-to-a-database-the-schema-of-a-database-project"></a>데이터베이스 프로젝트의 스키마를 데이터베이스에 배포하려면  
  
1.  **솔루션 탐색기**에서 데이터베이스 프로젝트를 마우스 오른쪽 단추로 클릭한 후 **빌드**를 클릭합니다.  
  
    데이터베이스 프로젝트를 빌드할 때 Transact\-SQL 스크립트를 생성합니다. 이 스크립트는 데이터베이스에 대해 실행될 때 해당 데이터베이스에 데이터베이스 프로젝트의 구조를 다시 만듭니다.  
  
2.  구성할 테스트 프로젝트를 선택합니다.  
  
3.  **솔루션 탐색기**에서SQL Server 단위 테스트 프로젝트를 마우스 오른쪽 단추로 클릭하고 **SQL Server 테스트 구성**을 클릭합니다.  
  
    **SQL Server 테스트 구성 -‘<projectname>’** 대화 상자가 표시됩니다.  
  
4.  **배포** 아래에서 다음을 수행할 수 있습니다.  
  
    -   **테스트를 실행하기 전에 데이터베이스 프로젝트를 자동으로 배포** 확인란을 선택하여 테스트를 실행하기 전에 데이터베이스 프로젝트에 대한 스키마 변경 내용이 모두 커밋되도록 합니다.  
  
    -   **데이터베이스 프로젝트**에서 배포할 데이터베이스 프로젝트를 클릭하거나 줄임표를 클릭하여 다른 프로젝트를 찾습니다. 데이터베이스 프로젝트 파일의 확장명은 .dbproj입니다.  
  
    -   **배포 구성**에서 배포할 프로젝트 구성을 클릭합니다. **디버그**, **기본** 또는 **릴리스** 중에서 선택할 수 있습니다. 그러나 단위 테스트에 대한 구성을 만드는 경우 해당 구성도 옵션으로 나타납니다.  
  
5.  **확인**을 클릭하여 **SQL Server 테스트 구성 -‘<projectname>’** 대화 상자를 닫습니다.  
  
    테스트 실행이 시작되면 1단계에서 생성된 Transact\-SQL 스크립트가 실행됩니다. 이 작업은 대상 데이터베이스에 스키마를 배포합니다.  
  
6.  단위 테스트 프로젝트를 다시 빌드하여 구성 변경 내용을 적용합니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트 만들기 및 정의](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[SQL Server 단위 테스트를 사용하여 데이터베이스 코드 확인](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
