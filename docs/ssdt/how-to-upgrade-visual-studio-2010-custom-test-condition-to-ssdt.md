---
title: 이전 릴리스의 Visual Studio 2010 사용자 지정 테스트 조건 업그레이드
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 44c895a3-dee0-4032-a60f-812f5fe3c713
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 333ef282fe4e1f9d7af53cd3569371e88018a03f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251069"
---
# <a name="how-to-upgrade-a-visual-studio-2010-custom-test-condition-from-a-previous-release-to-sql-server-data-tools"></a>방법: 이전 릴리스의 Visual Studio 2010 사용자 지정 테스트 조건을 SQL Server Data Tools로 업그레이드

SQL Server Data Tools 이전 버전에서 만든 단위 테스트 조건을 사용하려면 이를 업그레이드해야 합니다.  
  
-   [참조 업데이트](#UpdateReferences)  
  
-   [클래스 특성 및 형식 참조 업데이트](#UpdateClassAttributesandTypeReference)  
  
-   [업그레이드한 테스트 조건 설치](#ApplytheNewRegistrationProcess)  
  
## <a name="UpdateReferences"></a>참조 업데이트  
프로젝트 참조를 업데이트하려면  
  
1.  Visual Basic에서만 **솔루션 탐색기**의 **모든 파일 표시**를 클릭합니다.  
  
2.  **솔루션 탐색기**에서 **참조** 노드를 확장합니다.  
  
3.  다음 어셈블리 참조를 마우스 오른쪽 단추로 클릭하고 **제거**를 클릭합니다.  
  
    1.  Microsoft.Data.Schema.UnitTesting  
  
    2.  Microsoft.Data.Schema  
  
4.  **프로젝트** 메뉴에서, 또는 **솔루션 탐색기**에서 프로젝트 폴더를 마우스 오른쪽 단추로 클릭하여 **참조 추가**를 클릭합니다.  
  
5.  **.NET** 탭을 클릭합니다.  
  
6.  **구성 요소 이름** 목록에서 **System.ComponentModel.Composition**을 선택하고 **확인**을 클릭합니다.  
  
7.  필요한 어셈블리 참조를 추가합니다. 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 클릭합니다. **찾아보기**를 클릭하고 C:\Program Files (x86)\\MicrosoftSQL Server\110\DAC\Bin 폴더로 이동합니다. Microsoft.Data.Tools.Schema.Sql.dll을 닫고 추가를 클릭한 다음 확인을 클릭합니다.  
  
8.  **프로젝트** 메뉴에서 **프로젝트 언로드**를 클릭합니다.  
  
9. **솔루션 탐색기**에서 **프로젝트**를 마우스 오른쪽 단추로 클릭하고 `project_name` **.csproj** **편집**을 선택합니다.  
  
10. `Microsoft.CSharp.targets` 가져오기 뒤에 다음 Import 문을 추가합니다.  
  
    ```  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' == ''" />  
  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' != ''" />  
    ```  
  
11. 파일을 저장하고 닫습니다. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **프로젝트 다시 로드**를 선택합니다.  
  
12. 테스트 조건 클래스를 열고 **Microsoft.Data.Schema**로 시작하는 모든 using 문을 제거합니다. 이렇게 하는 가장 쉬운 방법은 파일을 마우스 오른쪽 단추로 클릭하고 **Using 구성**을 선택한 후 **제거 및 정렬**을 선택하는 것입니다. 다음 using 문을 제거해야 합니다.  
  
    ```  
    using Microsoft.Data.Schema.UnitTesting;  
    using Microsoft.Data.Schema.UnitTesting.Conditions;  
    using Microsoft.Data.Schema.Extensibility;  
    using Microsoft.Data.Schema;  
    ```  
  
13. 파일에 다음 using 문이 없으면 추가합니다.  
  
    ```  
    using System.ComponentModel;  
    using Microsoft.Data.Tools.Schema.Sql.UnitTesting;  
    using Microsoft.Data.Tools.Schema.Sql.UnitTesting.Conditions;  
    ```  
  
이제 해당 테스트 조건에서는 SQL Server 단위 테스트 어셈블리 참조를 사용합니다.  
  
## <a name="UpdateClassAttributesandTypeReference"></a>클래스 특성 및 형식 참조 업데이트  
이전 단위 테스트 클래스 특성을 새 특성으로 바꿉니다. SQL Server 단위 테스트 확장성은 이제 MEF(Managed Extensibility Framework)를 기반으로 합니다. 일부 형식 참조도 업데이트해야 합니다.  
  
### <a name="update-class-attributes"></a>클래스 특성 업데이트  
코드를 다음과 같이 업데이트합니다.  
  
1.  `DatabaseSchemaProviderCompatibility` 특성을 제거합니다. 이 특성은 이전 버전의 확장성 기능에서 필요했지만 SQL Server 단위 테스트에서는 지원되지 않습니다.  
  
2.  `DisplayName` 특성을 제거합니다. 표시 이름은 새 특성에 포함되어 있습니다.  
  
3.  새 `ExportTestCondition` 특성을 추가합니다. 이 특성이 있어야 SQL Server 단위 테스트에서 테스트 조건이 검색되고 사용됩니다. `ExportTestCondition`은 `DatabaseSchemaProviderCompatibility` 특성을 대체합니다. `ExportTestCondition`에는 다음 두 개의 매개 변수가 사용됩니다.  
  
    -   `DisplayName`은 첫 번째 매개 변수입니다. 이 매개 변수는 `DisplayName` 특성을 대체하며 이 형식의 모든 테스트 조건을 설명하는 데 사용됩니다.  
  
    -   두 번째 매개 변수는 해당 확장을 고유하게 식별하는 데 사용됩니다. 형식은 고유해야 하므로 `typeof(NewTestCondition)`를 사용하여 간단히 형식을 전달할 수 있습니다. 그러나 원하는 경우 문자열 ID도 전달할 수 있습니다.  
  
4.  클래스 정의는 다음과 같이 변경되어야 합니다.  
  
    이전:  
  
    ```  
    [DatabaseSchemaProviderCompatibility(typeof(DatabaseSchemaProvider))]  
    [DatabaseSchemaProviderCompatibility(null)]  
    [DisplayName("NewTestCondition")]  
    public class NewTestCondition:TestCondition  
    {  
       // Additional implementation to be added here  
    }  
    ```  
  
    이후:  
  
    ```  
    [ExportTestCondition("NewTestCondition ", typeof(NewTestCondition))]  
    public class NewTestCondition:TestCondition  
    {  
       // Additional implementation to be added here  
    }  
    ```  
  
### <a name="update-type-references"></a>형식 참조 업데이트  
SQL Server 단위 테스트 프레임워크에서는 일부 형식 이름이 변경되었습니다. 새 형식 이름을 사용하도록 코드를 업데이트하려면 **편집** 메뉴에서 **찾기 및 바꾸기**를 사용합니다. 형식 이름은 이제 **Sql**로 시작합니다. 클래스 이름은 다음과 같이 업데이트되어야 합니다.  
  
|이전 형식 이름|새 형식 이름|  
|-----------------|-----------------|  
|`ExecutionResult`|`SqlExecutionResult`|  
  
## <a name="ApplytheNewRegistrationProcess"></a>업그레이드한 테스트 조건 설치  
이전 버전의 데이터베이스 단위 테스트에서는 테스트 조건을 전역 어셈블리 캐시에 설치하거나 어셈블리 정보를 포함하는 XML 파일을 만들어야 했습니다. SQL Server 단위 테스트를 사용할 경우 이 추가 프로세스가 더 이상 필요하지 않습니다. 자세한 내용은 [프로젝트 컴파일 및 테스트 조건 설치](../ssdt/walkthrough-use-custom-test-condition-to-verify-stored-procedure-results.md#xxx)를 참조하세요.  
  
참조를 업데이트한 후에는 어셈블리가 서명되고 컴파일되었는지 확인합니다.  
  
다음에는 출력 디렉터리(기본적으로 My Documents\Visual Studio 2010\Projects\\<yoursolutionname>\\<yourprojectname>\bin\Debug\\)의 어셈블리 파일을 %Program Files%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions 디렉터리에 복사합니다. Visual Studio는 시작 시 TestConditions 디렉터리의 확장을 확인하고 이를 세션에서 사용할 수 있도록 합니다.  
  
## <a name="upgrade-existing-tests-that-need-to-use-the-new-test-condition"></a>새 테스트 조건을 사용해야 하는 기존 테스트 업그레이드  
이전 테스트 조건을 사용하며 새 조건을 사용해야 하는 모든 테스트 프로젝트를 찾습니다. 이러한 테스트 프로젝트를 업그레이드해야 합니다. 자세한 내용은 [데이터베이스 단위 테스트가 포함된 이전 테스트 프로젝트 업그레이드](../ssdt/upgrade-an-older-test-project-containing-database-unit-tests.md)를 참조하세요.  
  
이전 테스트 조건에 대한 어셈블리 참조를 제거합니다.  
  
프로젝트에 새 SQL Server 단위 테스트를 추가하여 프로젝트에 업그레이드된 테스트 조건에 대한 어셈블리 참조를 만듭니다. 참조를 만들려면 테스트 클래스를 추가해야 합니다. 참조를 추가한 후에는 테스트 클래스를 삭제할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트의 사용자 지정 테스트 조건](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)  
  
