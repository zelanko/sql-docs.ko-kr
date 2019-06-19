---
title: SQL Server의 사용자 지정 정적 코드 분석 규칙 어셈블리 작성 연습 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: f7b6ed8c-a4e0-4e33-9858-a8aa40aef309
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ba52dfc0ff41cb1ee4a92fda4a37e368f0533474
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65090162"
---
# <a name="walkthrough-authoring-a-custom-static-code-analysis-rule-assembly-for-sql-server"></a>SQL Server의 사용자 지정 정적 코드 분석 규칙 어셈블리 작성 연습
이 연습에서는 SQL Server 코드 분석 규칙을 만드는 데 사용되는 단계를 보여 줍니다. 이 연습에서 만든 규칙은 저장 프로시저, 트리거 및 함수에서 WAITFOR DELAY 문을 방지하는 데 사용됩니다.  
  
이 연습에서는 다음 프로세스를 사용하여 Transact\-SQL 정적 코드 분석에 대한 사용자 지정 규칙을 만듭니다.  
  
1.  클래스 라이브러리를 만들고 해당 프로젝트에 대해 서명을 사용하도록 설정하며 필요한 참조를 추가합니다.  
  
2.  Visual C\# 사용자 지정 규칙 클래스를 만듭니다.  
  
3.  두 도우미 Visual C\# 클래스를 만듭니다.  
  
4.  생성된 DLL을 설치하기 위해 Extensions 디렉터리에 복사합니다.  
  
5.  새로운 코드 분석 규칙이 설정되어 있는지 확인합니다.  
  
**필수 구성 요소**  
  
이 연습을 완료하려면 다음과 같은 구성 요소가 필요합니다.  
  
-   SQL Server Data Tools가 포함되고 Visual C\# 또는 Visual Basic 개발이 지원되는 Visual Studio 버전이 설치되어 있어야 합니다.  
  
-   SQL Server 개체가 포함된 SQL Server 프로젝트가 있어야 합니다.  
  
-   데이터베이스 프로젝트를 배포할 수 있는 SQL Server 인스턴스가 필요합니다.  
  
> [!NOTE]  
> 이 연습은 SQL Server Data Tools의 SQL Server 기능에 익숙한 사용자를 대상으로 합니다. 또한 코드 클래스를 만드는 방법 및 코드 편집기를 사용해서 클래스에 코드를 추가하는 방법과 같은 Visual Studio 개념에 대해서도 익숙해야 합니다.  
  
## <a name="creating-a-custom-code-analysis-rule-for-sql-server"></a>SQL Server에 대한 사용자 지정 코드 분석 규칙 만들기  
먼저 클래스 라이브러리를 만듭니다. 클래스 라이브러리 프로젝트를 만들려면:  
  
1.  SampleRules라는 Visual C\# 또는 Visual Basic 클래스 라이브러리 프로젝트를 만듭니다.  
  
2.  Class1.cs 파일의 이름을 AvoidWaitForDelayRule.cs로 변경합니다.  
  
3.  솔루션 탐색기에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭한 후 **참조 추가**를 클릭합니다.  
  
4.  프레임워크 탭에서 System.ComponentModel.Composition을 선택합니다.  
  
5.  **찾아보기**를 클릭하고 C:\Program Files (x86)\\MicrosoftSQL Server\120\SDK\Assemblies 디렉터리로 이동하고 Microsoft.SqlServer.TransactSql.ScriptDom.dll을 선택한 후 [확인]을 클릭합니다.  
  
6.  그런 다음 필요한 DACFx 참조를 설치합니다. **찾아보기**를 클릭하고 <Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\DAC\120 디렉터리로 이동합니다. Microsoft.SqlServer.Dac.dll, Microsoft.SqlServer.Dac.Extensions.dll 및 Microsoft.Data.Tools.Schema.Sql.dll 항목을 선택하고 **추가**를 클릭한 후 **확인**을 클릭합니다.  
  
    DACFx 바이너리가 이제 Visual Studio 설치 디렉터리 내부에 설치되어 있습니다. Visual Studio 2012의 경우 <Visual Studio Install Dir>은 일반적으로 C:\Program Files (x86)\\MicrosoftVisual Studio 11.0입니다. Visual Studio 2013의 경우 일반적으로 C:\Program Files (x86)\\MicrosoftVisual Studio 12.0입니다.  
  
다음 작업으로, 규칙에서 사용할 지원 클래스를 추가합니다.  
  
## <a name="creating-the-custom-code-analysis-rule-supporting-classes"></a>사용자 지정 코드 분석 규칙 지원 클래스 만들기  
규칙 자체의 클래스를 만들기 전에 방문자 클래스와 특성 클래스를 프로젝트에 추가합니다. 이러한 클래스는 추가 사용자 지정 규칙을 만드는 데 유용할 수 있습니다.  
  
정의해야 하는 첫 번째 클래스는 [TSqlConcreteFragmentVisitor](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.aspx)에서 파생된 WaitForDelayVisitor 클래스입니다. 이 클래스는 모델에서 WAITFOR DELAY 문에 대한 액세스를 제공합니다. 방문자 클래스는 SQL Server에서 제공하는 [ScriptDom](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.aspx) API를 사용합니다. 이 API에서 Transact\-SQL 코드는 AST(추상 구문 트리)로 표현되며 방문자 클래스는 WAITFORDELAY 문과 같은 특정 구문 개체를 찾으려고 할 때 유용할 수 있습니다. 이러한 개체는 특정 개체 속성 또는 관계와 연결되어 있지 않으므로 개체 모델을 사용하여 찾기가 어려울 수도 있지만 방문자 패턴과 [ScriptDom](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.aspx) API를 사용하면 쉽게 찾을 수 있습니다.  
  
### <a name="defining-the-waitfordelayvisitor-class"></a>WaitForDelayVisitor 클래스 정의  
  
1.  **솔루션 탐색기**에서 SampleRules 프로젝트를 선택합니다.  
  
2.  **프로젝트 메뉴**에서 **클래스 추가**를 선택합니다. **새 항목 추가** 대화 상자가 열립니다.  
  
3.  **이름** 텍스트 상자에 WaitForDelayVisitor.cs를 입력한 다음 **추가** 단추를 클릭합니다. WaitForDelayVisitor.cs 파일이 **솔루션 탐색기**에서 프로젝트에 추가됩니다.  
  
4.  WaitForDelayVisitor.cs 파일을 열고 다음 코드와 일치하도록 내용을 업데이트합니다.  
  
    ```  
    using System.Collections.Generic;  
    using Microsoft.SqlServer.TransactSql.ScriptDom;  
    namespace SampleRules {  
        class WaitForDelayVistor {}  
    }  
    ```  
  
5.  클래스 선언에서 액세스 한정자를 internal로 변경하고 TSqlConcreteFragmentVisitor에서 클래스를 파생시킵니다.  
  
    ```  
    internal class WaitForDelayVisitor : TSqlConcreteFragmentVisitor {}  
    ```  
  
6.  다음 코드를 추가하여 List 멤버 변수를 정의합니다.  
  
    ```  
    public IList<WaitForStatement> WaitForDelayStatements { get; private set; }  
    ```  
  
7.  다음 코드를 추가하여 클래스 생성자를 정의합니다.  
  
    ```  
    public WaitForDelayVisitor() {  
       WaitForDelayStatments = new List<WaitForStatement>();  
    }  
    ```  
  
8.  다음 코드를 추가하여 ExplicitVisit 메서드를 재정의합니다.  
  
    ```  
    public override void ExplicitVisit(WaitForStatement node) {  
       // We are only interested in WAITFOR DELAY occurrences  
       if (node.WaitForOption == WaitForOption.Delay)  
          WaitForDelayStatments.Add(node);  
    }  
    ```  
  
    이 메서드는 모델에서 WAITFOR 문을 방문하고 DELAY 옵션이 지정된 문을 WAITFOR DELAY 문 목록에 추가합니다. 여기서 참조되는 핵심 클래스는 [WaitForStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.waitforstatement.aspx)입니다.  
  
9. **파일** 메뉴에서 **저장**을 클릭합니다.  
  
두 번째 클래스는 LocalizedExportCodeAnalysisRuleAttribute.cs입니다. 이 클래스는 프레임워크에서 기본으로 제공되는 Microsoft.SqlServer.Dac.CodeAnalysis.ExportCodeAnalysisRuleAttribute의 확장으로, 리소스 파일에서 규칙을 통해 사용되는 DisplayName 및 Description을 읽을 수 있도록 지원합니다. 이 클래스는 여러 언어에서 규칙을 사용하려는 경우에 유용합니다.  
  
### <a name="defining-the-localizedexportcodeanalysisruleattribute-class"></a>LocalizedExportCodeAnalysisRuleAttribute 클래스 정의  
  
1.  **솔루션 탐색기**에서 SampleRules 프로젝트를 선택합니다.  
  
2.  **프로젝트 메뉴**에서 **클래스 추가**를 선택합니다. **새 항목 추가** 대화 상자가 열립니다.  
  
3.  **이름** 텍스트 상자에 LocalizedExportCodeAnalysisRuleAttribute.cs를 입력한 다음 **추가** 단추를 클릭합니다. 파일이 **솔루션 탐색기**에서 프로젝트에 추가됩니다.  
  
4.  파일을 열고 다음 코드와 일치하도록 내용을 업데이트합니다.  
  
    ```  
    using Microsoft.SqlServer.Dac.CodeAnalysis;  
    using System;  
    using System.Globalization;  
    using System.Reflection;  
    using System.Resources;  
  
    namespace SampleRules  
    {  
  
        internal class LocalizedExportCodeAnalysisRuleAttribute : ExportCodeAnalysisRuleAttribute  
        {  
            private readonly string _resourceBaseName;  
            private readonly string _displayNameResourceId;  
            private readonly string _descriptionResourceId;  
  
            private ResourceManager _resourceManager;  
            private string _displayName;  
            private string _descriptionValue;  
  
            /// <summary>  
            /// Creates the attribute, with the specified rule ID, the fully qualified  
            /// name of the resource file that will be used for looking up display name  
            /// and description, and the Ids of those resources inside the resource file.  
            /// </summary>  
            public LocalizedExportCodeAnalysisRuleAttribute(  
                string id,  
                string resourceBaseName,  
                string displayNameResourceId,  
                string descriptionResourceId)  
                : base(id, null)  
            {  
                _resourceBaseName = resourceBaseName;  
                _displayNameResourceId = displayNameResourceId;  
                _descriptionResourceId = descriptionResourceId;  
            }  
  
            /// <summary>  
            /// Rules in a different assembly would need to overwrite this  
            /// </summary>  
            /// <returns></returns>  
            protected virtual Assembly GetAssembly()  
            {  
                return GetType().Assembly;  
            }  
  
            private void EnsureResourceManagerInitialized()  
            {  
                var resourceAssembly = GetAssembly();  
  
                try  
                {  
                    _resourceManager = new ResourceManager(_resourceBaseName, resourceAssembly);  
                }  
                catch (Exception ex)  
                {  
                    var msg = String.Format(CultureInfo.CurrentCulture, RuleResources.CannotCreateResourceManager, _resourceBaseName, resourceAssembly);  
                    throw new RuleException(msg, ex);  
                }  
            }  
  
            private string GetResourceString(string resourceId)  
            {  
                EnsureResourceManagerInitialized();  
                return _resourceManager.GetString(resourceId, CultureInfo.CurrentUICulture);  
            }  
  
            /// <summary>  
            /// Overrides the standard DisplayName and looks up its value inside a resources file  
            /// </summary>  
            public override string DisplayName  
            {  
                get  
                {  
                    if (_displayName == null)  
                    {  
                        _displayName = GetResourceString(_displayNameResourceId);  
                    }  
                    return _displayName;  
                }  
            }  
  
            /// <summary>  
            /// Overrides the standard Description and looks up its value inside a resources file  
            /// </summary>  
            public override string Description  
            {  
                get  
                {  
                    if (_descriptionValue == null)  
                    {   
                        _descriptionValue = GetResourceString(_descriptionResourceId);  
                    }  
                    return _descriptionValue;  
                }  
            }  
        }  
    }  
    ```  
  
다음 작업으로, 규칙 이름, 규칙 설명 및 규칙이 규칙 구성 인터페이스에서 표시되는 범주를 정의할 리소스 파일을 추가합니다.  
  
### <a name="to-add-a-resource-file-and-three-resource-strings"></a>리소스 파일과 세 가지 리소스 문자열을 추가하려면  
  
1.  **솔루션 탐색기**에서 SampleRules 프로젝트를 선택합니다.  
  
2.  **프로젝트** 메뉴에서 **새 항목 추가**를 선택합니다. **새 항목 추가** 대화 상자가 열립니다.  
  
3.  **설치된 템플릿** 목록에서 **일반**을 클릭합니다.  
  
4.  세부 정보 창에서 **리소스 파일**을 클릭합니다.  
  
5.  **이름**에 RuleResources.resx를 입력합니다. 리소스가 정의되지 않은 상태로 리소스 편집기가 나타납니다.  
  
6.  다음과 같이 네 가지 리소스 문자열을 정의합니다.  
  
    |속성|값|  
    |--------|---------|  
    |AvoidWaitForDelay_ProblemDescription|WAITFOR DELAY 문이 {0}에 있습니다.|  
    |AvoidWaitForDelay_RuleName|저장 프로시저, 함수 및 트리거에서 WaitFor Delay 문을 사용하지 마세요.|  
    |CategorySamples|SamplesCategory|  
    |CannotCreateResourceManager|{1}에서 {0}에 대한 ResourceManager를 만들 수 없습니다.|  
  
7.  **파일** 메뉴에서 **RuleResources.resx 저장**을 클릭합니다.  
  
다음 작업으로, 사용자 인터페이스에서 규칙에 대한 정보를 표시하기 위해 Visual Studio에서 사용되는 리소스 파일의 리소스를 참조하는 클래스를 정의합니다.  
  
### <a name="defining-the-sampleconstants-class"></a>SampleConstants 클래스 정의  
  
1.  **솔루션 탐색기**에서 SampleRules 프로젝트를 선택합니다.  
  
2.  **프로젝트 메뉴**에서 **클래스 추가**를 선택합니다. **새 항목 추가** 대화 상자가 열립니다.  
  
3.  **이름** 텍스트 상자에 SampleRuleConstants.cs를 입력하고 **추가** 단추를 클릭합니다. SampleRuleConstants.cs 파일이 **솔루션 탐색기**에서 프로젝트에 추가됩니다.  
  
4.  SampleRuleConstants.cs 파일을 열고 다음 using 문을 파일에 추가합니다.  
  
    ```  
    namespace SampleRules  
    {   
        internal static class RuleConstants  
        {  
            /// <summary>  
            /// The name of the resources file to use when looking up rule resources  
            /// </summary>  
            public const string ResourceBaseName = "Public.Dac.Samples.Rules.RuleResources";  
  
            /// <summary>  
            /// Lookup name inside the resources file for the select asterisk rule name  
            /// </summary>  
            public const string AvoidWaitForDelay_RuleName = "AvoidWaitForDelay_RuleName";  
            /// <summary>  
            /// Lookup ID inside the resources file for the select asterisk description  
            /// </summary>  
            public const string AvoidWaitForDelay_ProblemDescription = "AvoidWaitForDelay_ProblemDescription";  
  
            /// <summary>  
            /// The design category (should not be localized)  
            /// </summary>  
            public const string CategoryDesign = "Design";  
  
            /// <summary>  
            /// The performance category (should not be localized)  
            /// </summary>  
            public const string CategoryPerformance = "Design";  
        }  
    }  
    ```  
  
5.  **파일** > **저장**을 클릭합니다.  
  
## <a name="creating-the-custom-code-analysis-rule-class"></a>사용자 지정 코드 분석 규칙 클래스 만들기  
사용자 지정 코드 분석 규칙에서 사용할 도우미 클래스를 추가했으므로 사용자 지정 규칙 클래스를 만들고 이름을 AvoidWaitForDelayRule로 지정하겠습니다. AvoidWaitForDelayRule 사용자 지정 규칙은 데이터베이스 개발자가 저장 프로시저, 트리거 및 함수에서 WAITFOR DELAY 문을 사용하지 않도록 하는 데 사용됩니다.  
  
### <a name="creating-the-avoidwaitfordelayrule-class"></a>AvoidWaitForDelayRule 클래스 만들기  
  
1.  **솔루션 탐색기**에서 SampleRules 프로젝트를 선택합니다.  
  
2.  **프로젝트 메뉴**에서 **클래스 추가**를 선택합니다. **새 항목 추가** 대화 상자가 열립니다.  
  
3.  **이름** 텍스트 상자에 AvoidWaitForDelayRule.cs를 입력한 다음 **추가**를 클릭합니다. AvoidWaitForDelayRule.cs 파일이 **솔루션 탐색기**에서 프로젝트에 추가됩니다.  
  
4.  AvoidWaitForDelayRule.cs 파일을 열고 다음 using 문을 파일에 추가합니다.  
  
    ```  
    using Microsoft.SqlServer.Dac.CodeAnalysis;  
    using Microsoft.SqlServer.Dac.Model;  
    using Microsoft.SqlServer.TransactSql.ScriptDom;  
    using System;  
    using System.Collections.Generic;  
    using System.Globalization;   
    namespace SampleRules {  
        class AvoidWaitForDelayRule {}  
    }  
    ```  
  
5.  AvoidWaitForDelayRule 클래스 선언에서 액세스 한정자를 public으로 변경합니다.  
  
    ```  
    /// <summary>  
    /// This is a rule that returns a warning message   
    /// whenever there is a WAITFOR DELAY statement appears inside a subroutine body.  
    /// This rule only applies to stored procedures, functions and triggers.  
    /// </summary>  
    public sealed class AvoidWaitForDelayRule  
    ```  
  
6.  Microsoft.SqlServer.Dac.CodeAnalysis.SqlCodeAnalysisRule 기본 클래스에서 AvoidWaitForDelayRule 클래스를 추출합니다.  
  
    ```  
    public sealed class AvoidWaitForDelayRule : SqlCodeAnalysisRule  
    ```  
  
7.  LocalizedExportCodeAnalysisRuleAttribute를 클래스에 추가합니다.  
  
    코드 분석 서비스에서는 LocalizedExportCodeAnalysisRuleAttribute를 사용하여 사용자 지정 코드 분석 규칙을 검색할 수 있습니다. ExportCodeAnalysisRuleAttribute(또는 이 특성에서 상속하는 특성)로 표시된 클래스만 코드 분석에서 사용될 수 있습니다.  
  
    LocalizedExportCodeAnalysisRuleAttribute는 서비스에서 사용되는 일부 필수 메타데이터를 제공합니다. 이러한 메타데이터에는 이 규칙의 고유 ID, Visual Studio 사용자 인터페이스에 표시될 표시 이름 및 문제를 식별할 때 규칙에서 사용할 수 있는 설명이 포함됩니다.  
  
    ```  
    [LocalizedExportCodeAnalysisRule(AvoidWaitForDelayRule.RuleId,  
        RuleConstants.ResourceBaseName,  
        RuleConstants.AvoidWaitForDelay_RuleName,   
        RuleConstants.AvoidWaitForDelay_ProblemDescription  
        Category = RuleConstants.CategoryPerformance,   
        RuleScope = SqlRuleScope.Element)]   
    public sealed class AvoidWaitForDelayRule : SqlCodeAnalysisRule  
    {  
       /// <summary>  
       /// The Rule ID should resemble a fully-qualified class name. In the Visual Studio UI  
       /// rules are grouped by "Namespace + Category", and each rule is shown using "Short ID: DisplayName".  
       /// For this rule, that means the grouping will be "Public.Dac.Samples.Performance", with the rule  
       /// shown as "SR1004: Avoid using WaitFor Delay statements in stored procedures, functions and triggers."  
       /// </summary>  
       public const string RuleId = "RuleSamples.SR1004";  
    }  
    ```  
  
    이 규칙은 특정 요소를 분석하기 때문에 RuleScope 속성은 Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleScope.Element여야 합니다. 규칙은 모델에서 일치하는 요소마다 한 번씩 호출됩니다. 전체 모델을 분석하려는 경우 Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleScope.Model을 대신 사용할 수 있습니다.  
  
8.  Microsoft.SqlServer.Dac.CodeAnalysis.SqlAnalysisRule.SupportedElementTypes를 설정하는 생성자를 추가합니다. 이 생성자는 요소 범위 규칙에 필요하며 이 규칙이 적용될 요소의 유형을 정의합니다. 이 경우에 규칙은 저장 프로시저, 트리거 및 함수에 적용됩니다. Microsoft.SqlServer.Dac.Model.ModelSchema 클래스는 분석할 수 있는 모든 요소 유형을 나열합니다.  
  
    ```  
    public AvoidWaitForDelayRule()  
    {  
       // This rule supports Procedures, Functions and Triggers. Only those objects will be passed to the Analyze method  
       SupportedElementTypes = new[]  
       {  
          // Note: can use the ModelSchema definitions, or access the TypeClass for any of these types  
          ModelSchema.ExtendedProcedure,  
          ModelSchema.Procedure,  
          ModelSchema.TableValuedFunction,  
          ModelSchema.ScalarFunction,  
  
          ModelSchema.DatabaseDdlTrigger,  
          ModelSchema.DmlTrigger,  
          ModelSchema.ServerDdlTrigger  
       };  
    }  
    ```  
  
9. Microsoft.SqlServer.Dac.CodeAnalysis.SqlAnalysisRule.Analyze(Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleExecutionContext) 메소드에 대한 재정의를 추가합니다. 이 메소드는 Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleExecutionContext를 입력 매개 변수로 사용합니다. 이 메서드는 잠재적 문제의 목록을 반환합니다.  
  
    메서드는 컨텍스트 매개 변수에서 Microsoft.SqlServer.Dac.Model.TSqlModel, Microsoft.SqlServer.Dac.Model.TSqlObject, [TSqlFragment](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.tsqlfragment.aspx)를 가져옵니다. WaitForDelayVisitor 클래스는 모델에서 모든 WAITFOR DELAY 문의 목록을 가져오는 데 사용됩니다.  
  
    그 목록에 있는 [WaitForStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.waitforstatement.aspx)마다 Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleProblem이 생성됩니다.  
  
    ```  
    /// <summary>  
    /// For element-scoped rules the Analyze method is executed once for every matching   
    /// object in the model.   
    /// </summary>  
    /// <param name="ruleExecutionContext">The context object contains the TSqlObject being   
    /// analyzed, a TSqlFragment  
    /// that's the AST representation of the object, the current rule's descriptor, and a   
    /// reference to the model being  
    /// analyzed.  
    /// </param>  
    /// <returns>A list of problems should be returned. These will be displayed in the Visual   
    /// Studio error list</returns>  
    public override IList<SqlRuleProblem> Analyze(  
        SqlRuleExecutionContext ruleExecutionContext)  
    {  
         IList<SqlRuleProblem> problems = new List<SqlRuleProblem>();  
  
         TSqlObject modelElement = ruleExecutionContext.ModelElement;  
  
         // this rule does not apply to inline table-valued function  
         // we simply do not return any problem in that case.  
         if (IsInlineTableValuedFunction(modelElement))  
         {  
             return problems;  
         }  
  
         string elementName = GetElementName(ruleExecutionContext, modelElement);  
  
         // The rule execution context has all the objects we'll need, including the   
         // fragment representing the object,  
         // and a descriptor that lets us access rule metadata  
         TSqlFragment fragment = ruleExecutionContext.ScriptFragment;  
         RuleDescriptor ruleDescriptor = ruleExecutionContext.RuleDescriptor;  
  
         // To process the fragment and identify WAITFOR DELAY statements we will use a   
         // visitor   
         WaitForDelayVisitor visitor = new WaitForDelayVisitor();  
         fragment.Accept(visitor);  
         IList<WaitForStatement> waitforDelayStatements = visitor.WaitForDelayStatements;  
  
         // Create problems for each WAITFOR DELAY statement found   
         // When creating a rule problem, always include the TSqlObject being analyzed. This   
         // is used to determine  
         // the name of the source this problem was found in and a best guess as to the   
         // line/column the problem was found at.  
         //  
         // In addition if you have a specific TSqlFragment that is related to the problem   
         //also include this  
         // since the most accurate source position information (start line and column) will   
         // be read from the fragment  
         foreach (WaitForStatement waitForStatement in waitforDelayStatements)  
         {  
            SqlRuleProblem problem = new SqlRuleProblem(  
                String.Format(CultureInfo.CurrentCulture,   
                    ruleDescriptor.DisplayDescription, elementName),  
                modelElement,  
                waitForStatement);  
            problems.Add(problem);  
        }  
        return problems;  
    }  
  
    private static string GetElementName(  
        SqlRuleExecutionContext ruleExecutionContext,   
        TSqlObject modelElement)  
    {  
        // Get the element name using the built in DisplayServices. This provides a number of   
        // useful formatting options to  
        // make a name user-readable  
        var displayServices = ruleExecutionContext.SchemaModel.DisplayServices;  
        string elementName = displayServices.GetElementName(  
            modelElement, ElementNameStyle.EscapedFullyQualifiedName);  
        return elementName;  
    }  
  
    private static bool IsInlineTableValuedFunction(TSqlObject modelElement)  
    {  
        return TableValuedFunction.TypeClass.Equals(modelElement.ObjectType)  
                       && FunctionType.InlineTableValuedFunction ==   
            modelElement.GetMetadata<FunctionType>(TableValuedFunction.FunctionType);  
    }  
    ```  
  
10. **파일** > **저장**을 클릭합니다.  
  
### <a name="building-the-class-library"></a>클래스 라이브러리 빌드  
  
1.  **프로젝트** 메뉴에서 **SampleRules 속성**을 클릭합니다.  
  
2.  **서명** 탭을 클릭합니다.  
  
3.  **어셈블리 서명**을 클릭합니다.  
  
4.  **강력한 이름 키 파일 선택**에서 **<New>** 를 클릭합니다.  
  
5.  **강력한 이름 키 만들기** 대화 상자의 **키 파일 이름**에 MyRefKey를 입력합니다.  
  
6.  (선택 사항) 강력한 이름 키 파일에 대한 암호를 지정할 수 있습니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
9. **빌드** 메뉴에서 **솔루션 빌드**를 클릭합니다.  
  
그런 다음, SQL Server 프로젝트를 빌드 및 배포할 때 로드되도록 어셈블리를 설치해야 합니다.  
  
## <a name="install-a-static-code-analysis-rule"></a>정적 코드 분석 규칙 설치  
규칙을 설치하려면 어셈블리 및 연관된 .pdb 파일을 Extensions 폴더에 복사해야 합니다.  
  
### <a name="to-install-the-samplerules-assembly"></a>SampleRules 어셈블리를 설치하려면  
이제 어셈블리 정보를 Extensions 디렉터리에 복사합니다. Visual Studio가 시작되면 <Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\DAC\120\Extensions 디렉터리 및 하위 디렉터리에서 확장을 식별하고 이를 사용할 수 있도록 설정합니다.  
  
Visual Studio 2012의 경우 <Visual Studio Install Dir>은 일반적으로 C:\Program Files (x86)\\MicrosoftVisual Studio 11.0입니다. Visual Studio 2013의 경우 일반적으로 C:\Program Files (x86)\\MicrosoftVisual Studio 12.0입니다.  
  
출력 디렉터리의 SampleRules.dll 어셈블리 파일을 <Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\DAC\120\Extensions 디렉터리에 복사합니다. 기본적으로 컴파일된 .dll 파일의 경로는 YourSolutionPath\YourProjectPath\bin\Debug 또는 YourSolutionPath\YourProjectPath\bin\Release입니다.  
  
규칙이 설치되었으며 Visual Studio를 다시 시작하면 나타납니다. 이제 새 Visual Studio 세션을 시작하고 데이터베이스 프로젝트를 만듭니다.  
  
### <a name="starting-a-new-visual-studio-session-and-creating-a-database-project"></a>새 Visual Studio 세션을 시작하고 데이터베이스 프로젝트 만들기  
  
1.  두 번째 Visual Studio 세션을 시작합니다.  
  
2.  **파일** > **새로 만들기** > **프로젝트**를 클릭합니다.  
  
3.  **새 프로젝트** 대화 상자의 **설치된 템플릿** 목록에서 **SQL Server** 노드를 확장한 후 **SQL Server 데이터베이스 프로젝트**를 클릭합니다.  
  
4.  **이름** 텍스트 상자에 SampleRulesDB를 입력하고 **확인**을 클릭합니다.  
  
마지막으로, SQL Server 프로젝트에 표시되는 새 규칙을 확인합니다. 새 AvoidWaitForRule 코드 분석 규칙을 보려면  
  
1.  **솔루션 탐색기**에서 SampleRulesDB 프로젝트를 선택합니다.  
  
2.  **프로젝트** 메뉴에서 **속성**을 클릭합니다. SampleRulesDB 속성 페이지가 표시됩니다.  
  
3.  **코드 분석**을 클릭합니다. RuleSamples.CategorySamples라는 새 범주가 표시됩니다.  
  
4.  RuleSamples .CategorySamples를 확장합니다. SR1004가 표시되어야 합니다. 저장 프로시저, 함수 및 트리거에서 WAITFOR DELAY 문을 사용하지 마세요.  
  
## <a name="see-also"></a>참고 항목  
[데이터베이스 코드 분석 규칙의 확장성 개요](../ssdt/overview-of-extensibility-for-database-code-analysis-rules.md)  
  
