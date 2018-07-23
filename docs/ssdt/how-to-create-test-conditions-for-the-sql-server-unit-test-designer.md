---
title: '방법: SQL Server 단위 테스트 디자이너용 테스트 조건 만들기 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 48076062-1ef5-419a-8a55-3c7b4234cc35
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 90e82370a658109ae6a8ccc653affc5e15614a55
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39087175"
---
# <a name="how-to-create-test-conditions-for-the-sql-server-unit-test-designer"></a>방법: SQL Server 단위 테스트 디자이너용 테스트 조건 만들기
확장 가능한 [TestCondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx) 클래스를 사용하여 새 테스트 조건을 만들 수 있습니다. 예를 들어 결과 집합의 열 또는 값 수를 확인하는 새 테스트 조건을 만들 수 있습니다.  
  
## <a name="to-create-a-test-condition"></a>테스트 조건을 만들려면  
이 절차에서는 SQL Server 단위 테스트 디자이너에 표시할 테스트 조건을 만드는 방법에 대해 설명합니다.  
  
1.  Visual Studio에서 클래스 라이브러리 프로젝트를 만듭니다.  
  
2.  **프로젝트** 메뉴에서 **참조 추가**를 클릭합니다.  
  
3.  **.NET** 탭을 클릭합니다.  
  
4.  **구성 요소 이름** 목록에서 **System.ComponentModel.Composition**을 선택하고 **확인**을 클릭합니다.  
  
5.  필요한 어셈블리 참조를 추가합니다. 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 클릭합니다. **찾아보기**를 클릭하고 C:\Program Files (x86)\\MicrosoftSQL Server\110\DAC\Bin 폴더로 이동합니다. Microsoft.Data.Tools.Schema.Sql.dll을 닫고 추가를 클릭한 다음 확인을 클릭합니다.  
  
6.  **프로젝트** 메뉴에서 **프로젝트 언로드**를 클릭합니다.  
  
7.  **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **<project name>.csproj 편집**을 선택합니다.  
  
8.  Microsoft.CSharp.targets 가져오기 뒤에 다음 Import 문을 추가합니다.  
  
    ```  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' == ''" />  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' != ''" />  
    ```  
  
9. 파일을 저장하고 닫습니다. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **프로젝트 다시 로드**를 선택합니다.  
  
10. [TestCondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx) 클래스에서 클래스를 파생시킵니다.  
  
11. 강력한 이름으로 어셈블리에 서명합니다. 자세한 내용은 [방법: 강력한 이름으로 어셈블리 서명](http://msdn.microsoft.com/library/xc31ft41.aspx)을 참조하세요.  
  
12. 클래스 라이브러리를 빌드합니다.  
  
13. 새 테스트 조건을 사용하려면 서명된 어셈블리를 %Program Files%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions 폴더에 복사해야 합니다. 이 폴더가 없으면 새로 만듭니다. 이 디렉터리에 복사하려면 컴퓨터에 대한 관리 권한이 있어야 합니다.  
  
14. 테스트 조건을 설치합니다. 자세한 내용은 [SQL Server 단위 테스트의 사용자 지정 테스트 조건](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)을 참조하세요.  
  
15. 프로젝트에 새 SQL Server 단위 테스트를 추가하여 프로젝트에 추가할 테스트 조건에 대한 참조를 만듭니다. 프로젝트에서 테스트 조건 어셈블리에 대한 참조를 수동으로 추가할 수 있습니다. 이 단계를 수행한 후 디자이너를 다시 로드합니다.  
  
    > [!NOTE]  
    > 참조를 만들려면 테스트 클래스를 추가해야 합니다. 참조를 추가한 후에는 테스트 클래스를 삭제할 수 있습니다.  
  
다음 예에서는 결과 집합에 반환된 열 수를 확인하는 간단한 테스트 조건을 만듭니다. 이 간단한 테스트 조건을 사용하여 저장 프로시저에 대한 계약이 올바른지 확인할 수 있습니다.  
  
```  
using System;  
using System.ComponentModel;  
using System.Data;  
using System.Data.Common;  
using Microsoft.Data.Tools.Schema.Sql.UnitTesting;  
using Microsoft.Data.Tools.Schema.Sql.UnitTesting.Conditions;  
  
namespace Ssdt.Samples.SqlUnitTesting  
{  
  
    [ExportTestCondition("ResultSet Column Count", typeof(ResultSetColumnCountCondition))]  
    public class ResultSetColumnCountCondition : TestCondition  
    {  
        private int _resultSet;  
        private int _count;  
        private int _batch;  
  
        public ResultSetColumnCountCondition()  
        {  
            _resultSet = 1;  
            _count = 0;  
            _batch = 1;  
        }  
  
        // method you need to override  
        // to perform the condition verification  
        public override void Assert(DbConnection validationConnection, SqlExecutionResult[] results)  
        {  
            // call base for parameter validation  
            base.Assert(validationConnection, results);  
  
            // verify batch exists  
            if (results.Length < _batch)  
                throw new DataException(String.Format("Batch {0} does not exist", _batch));  
  
            SqlExecutionResult result = results[_batch - 1];  
  
            // verify resultset exists  
            if (result.DataSet.Tables.Count < ResultSet)  
                throw new DataException(String.Format("ResultSet {0} does not exist", ResultSet));  
  
            DataTable table = result.DataSet.Tables[ResultSet - 1];  
  
            // actual condition verification  
            // verify resultset column count matches expected  
            if (table.Columns.Count != Count)  
                throw new DataException(String.Format(  
                    "ResultSet {0}: {1} columns did not match the {2} columns expected",  
                    ResultSet, table.Columns.Count, Count));  
        }  
  
        // this method is called to provide the string shown in the  
        // test conditions panel grid describing what the condition tests  
        public override string ToString()  
        {  
            return String.Format(  
                "Condition fails if ResultSet {0} does not contain {1} columns",  
                ResultSet, Count);  
        }  
  
        // below are the test condition properties  
        // that are exposed to the user in the property browser  
        #region Properties  
  
        // property specifying the resultset for which  
        // you want to check the column count  
        [Category("Test Condition")]  
        [DisplayName("ResultSet")]  
        [Description("ResultSet Number")]  
        public int ResultSet  
        {  
            get { return _resultSet; }  
  
            set  
            {  
                //basic validation  
                if (value < 1)  
                    throw new ArgumentException("ResultSet cannot be less than 1");  
  
                _resultSet = value;  
            }  
        }  
  
        // property specifying  
        // expected column count  
        [Category("Test Condition")]  
        [DisplayName("Count")]  
        [Description("Column Count")]  
        public int Count  
        {  
            get { return _count; }  
  
            set  
            {  
                //basic validation  
                if (value < 0)  
                    throw new ArgumentException("Count cannot be less than 0");  
  
                _count = value;  
            }  
        }  
  
        #endregion  
    }  
}  
```  
  
사용자 지정 테스트 조건의 클래스는 기본 [TestCondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx) 클래스에서 상속합니다. 사용자 지정 테스트 조건에는 추가 속성이 있으므로 사용자가 조건을 설치한 후 속성 창에서 조건을 구성할 수 있습니다.  
  
[ExportTestConditionAttribute](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.exporttestconditionattribute(v=vs.103).aspx)는 [TestCondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx)을 확장하는 클래스에 추가되어야 합니다. 이 특성을 사용하면 해당 클래스가 SQL Server Data Tools에서 검색되어 SQL Server 단위 테스트 디자인 및 실행 중에 사용됩니다. 이 특성에는 다음 두 개의 매개 변수가 사용됩니다.  
  
|특성 매개 변수|위치|설명|  
|-----------------------|------------|---------------|  
|DisplayName|@shouldalert|"테스트 조건" 콤보 상자의 문자열을 식별합니다. 이 이름은 고유해야 합니다. 두 조건의 표시 이름이 동일한 경우 첫 번째로 발견된 조건이 사용자에게 표시되고 Visual Studio 오류 관리자에 경고가 표시됩니다.|  
|ImplementingType|2|이 매개 변수는 해당 확장을 고유하게 식별하는 데 사용됩니다. 특성을 추가하려는 형식과 일치하도록 이 매개 변수를 변경해야 합니다. 이 예제에서는 **ResultSetColumnCountCondition** 유형을 사용하므로 **typeof(ResultSetColumnCountCondition)** 를 사용합니다. 유형이 **NewTestCondition**인 경우에는 **typeof(NewTestCondition)** 를 사용합니다.|  
  
이 예에서는 두 개의 속성을 추가합니다. 사용자 지정 테스트 조건의 사용자는 ResultSet 속성을 사용하여 열 수를 확인할 결과 집합을 지정할 수 있습니다. 그런 다음 Count 속성을 사용하여 예상 열 수를 지정할 수 있습니다.  
  
각 속성에 대해 다음 세 개의 특성이 추가됩니다.  
  
-   속성을 구성하는 데 유용한 범주 이름  
  
-   속성의 표시 이름  
  
-   속성에 대한 설명  
  
ResultSet 속성의 값이 1보다 작지 않은지와 Count 속성의 값이 0보다 큰지를 확인하기 위해 속성에 대한 유효성 검사가 수행됩니다.  
  
Assert 메서드는 테스트 조건의 기본 태스크를 수행합니다. Assert 메서드를 재정의하여 예상된 조건이 충족되는지 확인할 수 있습니다. 이 메서드는 다음 두 개의 매개 변수를 제공합니다.  
  
-   첫 번째 매개 변수는 테스트 조건의 유효성을 검사하는 데 사용되는 데이터베이스 연결입니다.  
  
-   두 번째이자 더 중요한 매개 변수는 실행된 각 일괄 처리에 대해 단일 배열 요소를 반환하는 결과 배열입니다.  
  
각 테스트 스크립트에 대해 하나의 일괄 처리만 지원됩니다. 따라서 테스트 조건은 항상 첫 번째 배열 요소를 검사합니다. 배열 요소에는 데이터 집합이 포함되어 있고 이 데이터 집합에는 테스트 스크립트의 반환된 결과 집합이 포함되어 있습니다. 이 예의 코드는 데이터 집합의 데이터 테이블에 적절한 수의 열이 포함되어 있는지 확인합니다. 자세한 내용은 데이터 집합을 참조하십시오.  
  
서명할 테스트 조건을 포함하는 클래스 라이브러리를 설정해야 하며 이 작업은 서명 탭의 프로젝트 속성에서 수행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트의 사용자 지정 테스트 조건](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)  
  
