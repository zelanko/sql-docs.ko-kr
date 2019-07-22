---
title: '연습: 사용자 지정 테스트 조건을 사용하여 저장 프로시저 결과 확인 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 4c33b494-a85e-4dd2-97b6-c88ee858a99c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6ef888bf2cf4259ec904194a39aa74ed44040586
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068978"
---
# <a name="walkthrough-using-a-custom-test-condition-to-verify-the-results-of-a-stored-procedure"></a>연습: 사용자 지정 테스트 조건을 사용하여 저장 프로시저 결과 확인
이 기능 확장 연습에서는 테스트 조건을 만든 후 SQL Server 단위 테스트를 만들어 해당 기능을 확인합니다. 이 프로세스에는 테스트 조건에 대한 클래스 라이브러리 프로젝트를 만들고 이 프로젝트를 서명 및 설치하는 작업이 포함됩니다. 업데이트할 테스트 조건이 이미 있는 경우 [방법: 이전 릴리스의 Visual Studio 2010 사용자 지정 테스트 조건을 SQL Server Data Tools로 업그레이드](../ssdt/how-to-upgrade-visual-studio-2010-custom-test-condition-to-ssdt.md)를 참조하세요.  
  
이 연습에서는 다음 작업을 수행합니다.  
  
-   테스트 조건 만들기  
  
-   강력한 이름으로 어셈블리에 서명  
  
-   프로젝트에 필요한 참조 추가  
  
-   테스트 조건 빌드  
  
-   새 테스트 조건 설치  
  
-   새 테스트 조건 테스트  
  
이 연습을 완료하려면 최신 버전의 SQL Server Data Tools가 포함된 Visual Studio 2010 또는 Visual Studio 2012가 있어야 합니다. 자세한 내용은 [SQL Server Data Tools 설치](../ssdt/install-sql-server-data-tools.md)를 참조하세요.  
  
## <a name="creating-a-custom-test-condition"></a>사용자 지정 테스트 조건 만들기  
먼저 클래스 라이브러리를 만듭니다.  
  
1.  **파일** 메뉴에서 **새로 만들기**를 클릭하고 **프로젝트**를 클릭합니다.  
  
2.  **새 프로젝트** 대화 상자의 **프로젝트 형식**에서 Visual C\#을 클릭합니다.  
  
3.  **템플릿**에서 **클래스 라이브러리**를 선택합니다.  
  
4.  **이름** 텍스트 상자에 **ColumnCountCondition**을 입력하고 **확인**을 클릭합니다.  
  
이제 프로젝트에 서명합니다.  
  
1.  **프로젝트** 메뉴에서 **ColumnCountCondition 속성**을 클릭합니다.  
  
2.  **서명** 탭에서 **어셈블리 서명** 확인란을 선택합니다.  
  
3.  **강력한 이름 키 파일 선택** 상자에서 **\<새로 만들기...>** 를 클릭합니다.  
  
    **강력한 이름 키 만들기** 대화 상자가 나타납니다.  
  
4.  **키 파일 이름** 상자에 **SampleKey**를 입력합니다.  
  
5.  암호를 입력하고 확인을 위해 한 번 더 입력한 후 **확인**을 클릭합니다. 솔루션을 빌드할 때 이 키 파일이 어셈블리에 서명하는 데 사용됩니다.  
  
6.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
7.  **빌드** 메뉴에서 **솔루션 빌드**를 클릭합니다.  
  
이제 프로젝트에 필요한 참조를 추가합니다.  
  
1.  **솔루션 탐색기**에서 **ColumnCountCondition** 프로젝트를 선택합니다.  
  
2.  **프로젝트** 메뉴에서 **참조 추가**를 클릭하여 **참조 추가** 대화 상자를 표시합니다.  
  
3.  **.NET** 탭을 선택합니다.  
  
4.  **구성 요소 이름** 열에서 **System.ComponentModel.Composition** 구성 요소를 찾아 선택합니다. 구성 요소를 선택한 후 **확인**을 클릭합니다.  
  
5.  필요한 어셈블리 참조를 추가합니다. 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 클릭합니다. **찾아보기**를 클릭하고 C:\Program Files (x86)\\MicrosoftSQL Server\110\DAC\Bin 폴더로 이동합니다. Microsoft.Data.Tools.Schema.Sql.dll을 닫고 추가를 클릭한 다음 확인을 클릭합니다.  
  
6.  **프로젝트** 메뉴에서 **프로젝트 언로드**를 클릭합니다.  
  
7.  **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **<project name>.csproj 편집**을 선택합니다.  
  
8.  **Microsoft.CSharp.targets** 가져오기 뒤에 다음 Import 문을 추가합니다.  
  
    ```  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' == ''" />  
  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' != ''" />  
    ```  
  
9. 파일을 저장하고 닫습니다. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **프로젝트 다시 로드**를 선택합니다.  
  
    **솔루션 탐색기**에서 프로젝트의 **참조** 노드 아래에 필요한 참조가 표시됩니다.  
  
## <a name="creating-the-resultsetcolumncountcondition-class"></a>ResultSetColumnCountCondition 클래스 만들기  
이제 이름 **Class1**을 **ResultSetColumnCountCondition**으로 바꾸고 [testcondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx)에서 파생시킵니다. **ResultSetColumnCountCondition** 클래스는 결과 집합에 반환된 열 수를 확인하는 간단한 테스트 조건입니다. 이 조건을 사용하여 저장 프로시저에 대한 계약이 올바른지 확인할 수 있습니다.  
  
1.  **솔루션 탐색기**에서 Class1.cs를 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 클릭한 후 **ResultSetColumnCountCondition.cs**를 입력합니다.  
  
2.  **예**를 클릭하여 모든 참조의 이름을 Class1로 바꾸도록 확인합니다.  
  
3.  **ResultSetColumnCountCondition.cs** 파일을 열고 다음 using 문을 파일에 추가합니다.  
  
    ```  
    using System;  
    using System.ComponentModel;  
    using System.Data;  
    using System.Data.Common;  
    using Microsoft.Data.Tools.Schema.Sql.UnitTesting;  
    using Microsoft.Data.Tools.Schema.Sql.UnitTesting.Conditions;  
  
    namespace ColumnCountCondition {  
        public class ResultSetColumnCountCondition  
    ```  
  
4.  [testcondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx)에서 클래스를 파생시킵니다.  
  
    ```  
    public class ResultSetColumnCountCondition : TestCondition  
    ```  
  
5.  [ExportTestConditionAttribute](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.exporttestconditionattribute(v=vs.103).aspx)를 추가합니다. UnitTesting.Conditions.ExportTestConditionAttribute에 대한 자세한 내용은 [방법: SQL Server 단위 테스트 디자이너용 테스트 조건 만들기](../ssdt/how-to-create-test-conditions-for-the-sql-server-unit-test-designer.md)를 참조하세요.  
  
    ```  
    [ExportTestCondition("ResultSet Column Count", typeof(ResultSetColumnCountCondition))]  
        public class ResultSetColumnCountCondition : TestCondition  
    ```  
  
6.  멤버 변수와 생성자를 만듭니다.  
  
    ```  
            private int _resultSet;  
            private int _count;  
            private int _batch;  
  
            public ResultSetColumnCountCondition() {  
                _resultSet = 1;  
                _count = 0;  
                _batch = 1;  
            }  
    ```  
  
7.  **Assert** 메서드를 재정의합니다. 이 메서드에는 데이터베이스에 대한 연결을 나타내는 **IDbConnection**과 **SqlExecutionResult**에 대한 인수가 포함됩니다. 이 메서드는 오류 처리에 **DataSchemaException**을 사용합니다.  
  
    ```  
           //method you need to override  
            //to perform the condition verification  
            public override void Assert(DbConnection validationConnection, SqlExecutionResult[] results)  
            {  
                //call base for parameter validation  
                base.Assert(validationConnection, results);  
  
                //verify batch exists  
                if (results.Length < _batch)  
                    throw new DataException(String.Format("Batch {0} does not exist", _batch));  
  
                SqlExecutionResult result = results[_batch - 1];  
  
                //verify resultset exists  
                if (result.DataSet.Tables.Count < ResultSet)  
                    throw new DataException(String.Format("ResultSet {0} does not exist", ResultSet));  
  
                DataTable table = result.DataSet.Tables[ResultSet - 1];  
  
                //actual condition verification  
                //verify resultset column count matches expected  
                if (table.Columns.Count != Count)  
                    throw new DataException(String.Format(  
                        "ResultSet {0}: {1} columns did not match the {2} columns expected",  
                        ResultSet, table.Columns.Count, Count));  
            }  
  
    Add the following method, which overrides the ToString method:  
    C#  
            //this method is called to provide the string shown in the  
            //test conditions panel grid describing what the condition tests  
            public override string ToString()  
            {  
                return String.Format(  
                    "Condition fails if ResultSet {0} does not contain {1} columns",  
                    ResultSet, Count);  
            }  
    ```  
  
8.  **CategoryAttribute**, **DisplayNameAttribute** 및 **DescriptionAttribute** 특성을 사용하여 다음 테스트 조건 속성을 추가합니다.  
  
    ```  
            //below are the test condition properties  
            //that are exposed to the user in the property browser  
            #region Properties  
  
            //property specifying the resultset for which  
            //you want to check the column count  
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
  
            //property specifying  
            //expected column count  
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
    ```  
  
최종 코드는 다음과 같습니다.  
  
```  
using System;  
using System.ComponentModel;  
using System.Data;  
using System.Data.Common;  
using Microsoft.Data.Tools.Schema.Sql.UnitTesting;  
using Microsoft.Data.Tools.Schema.Sql.UnitTesting.Conditions;  
  
namespace ColumnCountCondition  
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
  
        //method you need to override  
        //to perform the condition verification  
        public override void Assert(DbConnection validationConnection, SqlExecutionResult[] results)  
        {  
            //call base for parameter validation  
            base.Assert(validationConnection, results);  
  
            //verify batch exists  
            if (results.Length < _batch)  
                throw new DataException(String.Format("Batch {0} does not exist", _batch));  
  
            SqlExecutionResult result = results[_batch - 1];  
  
            //verify resultset exists  
            if (result.DataSet.Tables.Count < ResultSet)  
                throw new DataException(String.Format("ResultSet {0} does not exist", ResultSet));  
  
            DataTable table = result.DataSet.Tables[ResultSet - 1];  
  
            //actual condition verification  
            //verify resultset column count matches expected  
            if (table.Columns.Count != Count)  
                throw new DataException(String.Format(  
                    "ResultSet {0}: {1} columns did not match the {2} columns expected",  
                    ResultSet, table.Columns.Count, Count));  
        }  
  
        //this method is called to provide the string shown in the  
        //test conditions panel grid describing what the condition tests  
        public override string ToString()  
        {  
            return String.Format(  
                "Condition fails if ResultSet {0} does not contain {1} columns",  
                ResultSet, Count);  
        }  
  
        //below are the test condition properties  
        //that are exposed to the user in the property browser  
        #region Properties  
  
        //property specifying the resultset for which  
        //you want to check the column count  
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
  
        //property specifying  
        //expected column count  
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
  
이제 프로젝트를 빌드합니다.  
  
## <a name="xxx"></a>프로젝트 컴파일 및 테스트 조건 설치  
**빌드** 메뉴에서 **솔루션 빌드**를 클릭합니다.  
  
이제 어셈블리 정보를 Extensions 디렉터리에 복사합니다. Visual Studio는 시작 시 %Program Files%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions 디렉터리 및 하위 디렉터리에 있는 모든 확장을 확인하고 이를 사용할 수 있도록 합니다.  
  
출력 디렉터리의 **ColumnCountCondition.dll** 어셈블리 파일을 %Program Files%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions 디렉터리에 복사합니다.  
  
기본적으로 컴파일된 .dll 파일의 경로는 *YourSolutionPath*\\*YourProjectPath*\bin\Debug 또는 *YourSolutionPath*\\*YourProjectPath*\bin\Release입니다.  
  
이제 새 Visual Studio 세션을 시작하고 데이터베이스 프로젝트를 만듭니다. 새 Visual Studio 세션을 시작하고 데이터베이스 프로젝트를 만들려면:  
  
1.  두 번째 Visual Studio 세션을 시작합니다.  
  
2.  **파일** 메뉴에서 **새로 만들기**를 클릭하고 **프로젝트**를 클릭합니다.  
  
3.  **새 프로젝트** 대화 상자의 설치된 템플릿 목록에서 **SQL Server** 노드를 선택합니다.  
  
4.  [세부 정보] 창에서 **SQL Server 데이터베이스 프로젝트**를 클릭합니다.  
  
5.  **이름** 텍스트 상자에 **SampleConditionDB**를 입력한 후 **확인**을 클릭합니다.  
  
이제 단위 테스트를 만들어야 합니다. 새 테스트 클래스 내에 SQL Server 단위 테스트를 만들려면:  
  
1.  **테스트** 메뉴에서 **새 테스트**를 클릭하여 **새 테스트 추가** 대화 상자를 표시합니다.  
  
    **솔루션 탐색기**를 열고 테스트 프로젝트를 마우스 오른쪽 단추로 클릭한 후 **추가**를 가리키고 **새 테스트**를 클릭해도 됩니다.  
  
2.  템플릿 목록에서 **SQL Server 단위 테스트**를 클릭합니다.  
  
3.  **테스트 이름**에 **SampleUnitTest**를 입력합니다.  
  
4.  **테스트 프로젝트에 추가**에서 **새 Visual C\# 테스트 프로젝트 만들기**를 클릭합니다. 그런 후 **확인**을 클릭하여 **새 테스트 프로젝트** 대화 상자를 표시합니다.  
  
5.  프로젝트 이름에 **SampleUnitTest**를 입력합니다.  
  
6.  **취소**를 클릭하여 데이터베이스 연결을 사용하도록 테스트 프로젝트를 구성하지 않고 SQL Server 단위 테스트를 만듭니다. SQL Server 단위 테스트 디자이너에 빈 테스트가 나타납니다. Visual C\# 소스 코드 파일이 테스트 프로젝트에 추가됩니다.  
  
    데이터베이스 연결이 포함된 데이터베이스 단위 테스트를 만들고 구성하는 방법에 대한 자세한 내용은 [방법: 빈 SQL Server 단위 테스트 만들기](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)를 참조하세요.  
  
7.  **만들려면 여기를 클릭합니다.** 를 클릭하여 단위 테스트 만들기를 마칩니다. 새 테스트 조건이 SQL Server 프로젝트에 표시됩니다.  
  
> [!NOTE]  
> 기존 단위 테스트 프로젝트와 함께 사용자 지정 테스트 조건을 사용하려면 새 SQL Server 단위 테스트 클래스를 하나 이상 만들어야 합니다. 테스트 클래스를 만드는 동안 테스트 조건 어셈블리에 대한 필요한 참조가 테스트 프로젝트에 추가됩니다.  
  
새 테스트 조건을 보려면  
  
1.  **SQL Server 단위 테스트 디자이너**의 **테스트 조건**에 있는 **이름** 열에서 inconclusiveCondition1 테스트를 클릭합니다.  
  
2.  **테스트 조건 삭제** 도구 모음 단추를 클릭하여 inconclusiveCondition1 테스트를 제거합니다.  
  
3.  **테스트 조건** 드롭다운을 클릭하고 **결과 집합 열 개수**를 선택합니다.  
  
4.  **테스트 조건 추가** 도구 모음 단추를 클릭하여 사용자 지정 테스트 조건을 추가합니다.  
  
5.  **속성** 창에서 Count, Enabled 및 ResultSet 속성을 구성합니다.  
  
    자세한 내용은 [방법: SQL Server 단위 테스트에 테스트 조건 추가](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트의 사용자 지정 테스트 조건](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)  
  
