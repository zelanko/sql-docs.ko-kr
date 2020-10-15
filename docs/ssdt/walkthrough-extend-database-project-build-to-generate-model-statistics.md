---
title: 데이터베이스 프로젝트 빌드를 확장하여 모델 통계 생성
description: 데이터베이스 프로젝트를 빌드할 때 SQL 데이터베이스 모델에서 통계를 출력하는 빌드 참가자를 만들고 설치하고 테스트하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: d44935ce-63bf-46df-976a-5a54866c8119
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 59c98e39bccbb6d4f74ddb5e9494e7fc4bced3eb
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91985079"
---
# <a name="walkthrough-extend-database-project-build-to-generate-model-statistics"></a>연습: 데이터베이스 프로젝트 빌드를 확장하여 모델 통계 생성

빌드 참가자를 만들어서 데이터베이스 프로젝트를 빌드할 때 사용자 지정 작업을 수행할 수 있습니다. 이 연습에서는 데이터베이스 프로젝트를 빌드할 때 SQL 데이터베이스 모델에서 통계를 출력하는 ModelStatistics라는 빌드 참가자를 만듭니다. 이 빌드 참가자는 빌드할 때 매개 변수가 사용되기 때문에 몇 가지 추가 단계가 필요합니다.  
  
이 연습에서 수행하는 주요 작업은 다음과 같습니다.  
  
-   [빌드 참가자 만들기](#CreateBuildContributor)  
  
-   [빌드 참가자 설치](#InstallBuildContributor)  
  
-   [빌드 참가자 테스트](#TestBuildContributor)  
  
## <a name="prerequisites"></a>필수 구성 요소  
이 연습을 완료하려면 다음과 같은 구성 요소가 필요합니다.  
  
-   SSDT(SQL Server Data Tools)가 포함되고 C# 또는 VB 개발이 지원되는 Visual Studio 버전이 설치되어 있어야 합니다.  
  
-   SQL 개체가 포함된 SQL 프로젝트가 있어야 합니다.  
  
> [!NOTE]  
> 이 연습은 SSDT의 SQL 기능에 익숙한 사용자를 대상으로 합니다. 또한 코드 클래스를 만드는 방법 및 코드 편집기를 사용해서 클래스에 코드를 추가하는 방법과 같은 기본적인 Visual Studio 개념에 대해서도 익숙해야 합니다.  
  
## <a name="build-contributor-background"></a>빌드 참가자 배경  
빌드 참가자는 프로젝트 빌드 중 프로젝트를 나타내는 모델이 생성된 후, 프로젝트가 디스크에 저장되기 전에 실행됩니다. 빌드 참가자는 다음과 같은 시나리오에서 사용할 수 있습니다.  
  
-   모델 콘텐츠 유효성 검사 및 유효성 검사를 호출자에게 보고. 이 작업을 수행하려면 OnExecute 메서드에 대해 매개 변수로 전달되는 목록에 오류를 추가합니다.  
  
-   모델 통계 생성 및 사용자에게 보고. 이 작업에 대해서는 여기에 표시된 예를 참조하십시오.  
  
빌드 참가자를 만들 때 주로 사용되는 첫 번째는 OnExecute 메서드입니다. BuildContributor에서 상속되는 모든 클래스는 이 메서드를 구현해야 합니다. BuildContributorContext 개체는 이 메서드에 전달됩니다. 여기에는 데이터베이스의 모델, 빌드 속성 및 빌드 기여자가 사용한 인수/파일과 같은 빌드에 대한 모든 관련 데이터가 포함됩니다.  
  
**TSqlModel 및 데이터베이스 모델 API**  
  
가장 유용한 개체는 TSqlModel 개체로 대표되는 데이터베이스 모델입니다. 이 개체는 모든 테이블, 뷰 및 기타 요소는 물론 이들 간의 관계까지 포함된 데이터베이스에 대한 논리적인 표현입니다. 특정 유형의 요소를 쿼리하고 필요한 관계를 트래버스하는 데에는 강력한 형식의 스키마를 사용할 수 있습니다. 이 스키마의 사용 방법에 대한 예는 연습 코드에서 확인할 수 있습니다.  
  
다음은 이 연습의 참가자 예에 사용된 일부 명령입니다.  
  
|**클래스**|**메서드/속성**|**설명**|  
|-------------|------------------------|-------------------|  
|[TSqlModel](/dotnet/api/microsoft.sqlserver.dac.model.tsqlmodel)|GetObjects()|모델에서 개체를 쿼리하며 모델 API를 사용하기 위한 기본 요소입니다. 테이블 또는 뷰와 같은 최상위 유형만 쿼리할 수 있으며, 열과 같은 유형은 모델 트래버스를 통해서만 찾을 수 있습니다. ModelTypeClass 필터가 지정되지 않았으면 모든 최상위 유형이 반환됩니다.|  
|[TSqlObject](/dotnet/api/microsoft.sqlserver.dac.model.tsqlobject)|GetReferencedRelationshipInstances()|현재 TSqlObject에서 참조되는 요소에 대한 관계를 찾습니다. 예를 들어 테이블의 경우 이 메서드는 테이블의 열과 같은 개체를 반환합니다. 이 예에서는 ModelRelationshipClass 필터를 사용해서 쿼리할 정확한 관계를 지정할 수 있습니다(예: "Table.Columns" 필터를 사용하면 열만 반환되도록 해야 합니다).<br /><br />이외에도 GetReferencingRelationshipInstances, GetChildren 및 GetParent와 같은 비슷한 메서드가 많이 있습니다. 자세한 내용은 API 설명서를 참조하십시오.|  
  
**참가자를 고유하게 식별**  
  
빌드 프로세스 중에는 사용자 지정 참가자가 표준 확장 디렉터리에서 로드됩니다. 빌드 참가자는 [ExportBuildContributor](/dotnet/api/microsoft.sqlserver.dac.deployment.exportbuildcontributorattribute) 특성으로 식별됩니다. 이 특성은 참가자를 검색하는 데 필요합니다. 이 특성은 다음과 비슷합니다.  
  
```  
[ExportBuildContributor("ExampleContributors.ModelStatistics", "1.0.0.0")]  
  
```  
  
이 경우 특성의 첫 번째 매개 변수는 고유 식별자여야 하며, 이 식별자는 프로젝트 파일에서 기여자를 식별하는 데 사용됩니다. 식별자를 생성하려면 라이브러리의 네임스페이스(이 연습에서는 "ExampleContributors")를 클래스 이름(이 연습에서는 "ModelStatistics")과 결합하는 것이 가장 좋습니다. 이 연습의 뒷부분에서는 이 네임스페이스를 사용해서 실행할 참가자를 지정하는 방법을 볼 수 있습니다.  
  
## <a name="create-a-build-contributor"></a><a name="CreateBuildContributor"></a>빌드 참가자 만들기  
빌드 참가자를 만들려면 다음 작업을 수행해야 합니다.  
  
-   클래스 라이브러리 프로젝트를 만들고 필요한 참조를 추가합니다.  
  
-   [BuildContributor](/dotnet/api/microsoft.sqlserver.dac.deployment.buildcontributor)로부터 상속되는 ModelStatistics라는 클래스를 정의합니다.  
  
-   OnExecute 메서드를 재정의합니다.  
  
-   프라이빗 도우미 메서드를 몇 개 추가합니다.  
  
-   결과 어셈블리를 빌드합니다.  
  
#### <a name="to-create-a-class-library-project"></a>클래스 라이브러리 프로젝트를 만들려면  
  
1.  MyBuildContributor라는 이름의 Visual Basic 또는 Visual C# 클래스 라이브러리 프로젝트를 만듭니다.  
  
2.  "Class1.cs" 파일 이름을 "ModelStatistics.cs"로 바꿉니다.  
  
3.  솔루션 탐색기에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭한 후 **참조 추가**를 클릭합니다.  
  
4.  **System.ComponentModel.Composition** 항목을 선택한 후 **확인**을 클릭합니다.  
  
5.  필요한 SQL 참조 추가: 프로젝트 노드를 마우스 오른쪽 단추로 클릭한 후 **참조 추가**를 클릭합니다. **찾아보기** 단추를 클릭합니다. **C:\Program Files (x86)\Microsoft SQL Server\110\DAC\Bin** 폴더로 이동합니다. **Microsoft.SqlServer.Dac.dll**, **Microsoft.SqlServer.Dac.Extensions.dll**및 **Microsoft.Data.Tools.Schema.Sql.dll** 항목을 선택한 후 **확인**을 클릭합니다.  
  
    그런 후 클래스에 코드 추가를 시작합니다.  
  
#### <a name="to-define-the-modelstatistics-class"></a>ModelStatistics 클래스를 정의하려면  
  
1.  ModelStatistics 클래스는 OnExecute 메서드에 전달된 데이터베이스 모델을 처리하고 모델 콘텐츠에 대한 세부 정보가 표시된 XML 보고서를 생성합니다.  
  
    코드 편집기에서 다음과 일치하도록 ModelStatistics.cs 파일을 업데이트합니다.  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.IO;  
    using System.Linq;  
    using System.Xml.Linq;  
    using Microsoft.Data.Schema;  
    using Microsoft.Data.Schema.Build;  
    using Microsoft.Data.Schema.Extensibility;  
    using Microsoft.Data.Schema.SchemaModel;  
    using Microsoft.Data.Schema.Sql;  
  
    namespace ExampleContributors  
    {  
    /// <summary>  
        /// A BuildContributor that generates statistics about a model and saves this to the output directory.  
        /// Will only run if a "GenerateModelStatistics=true" contributor argument is set in the project file, or a targets file.   
        /// Statistics can be sorted by "none, "name" or "value", with "none" being the default sort behavior.  
        ///   
        /// To set contributor arguments in a project file, add the following:  
        ///   
        /// <PropertyGroup>  
        ///     <ContributorArguments Condition="'$(Configuration)' == 'Debug'">  
        /// $(ContributorArguments);ModelStatistics.GenerateModelStatistics=true;ModelStatistics.SortModelStatisticsBy="name";  
        ///     </ContributorArguments>  
        /// <PropertyGroup>      
        ///   
        /// This will generate model statistics when building in Debug mode only - remove the condition to generate in all build modes.  
        /// </summary>  
        [ExportBuildContributor("ExampleContributors.ModelStatistics", "1.0.0.0")]  
        public class ModelStatistics : BuildContributor  
        {  
            public const string GenerateModelStatistics = "ModelStatistics.GenerateModelStatistics";  
            public const string SortModelStatisticsBy = "ModelStatistics.SortModelStatisticsBy";  
            public const string OutDir = "ModelStatistics.OutDir";  
            public const string ModelStatisticsFilename = "ModelStatistics.xml";  
            private enum SortBy { None, Name, Value };  
            private static Dictionary<string, SortBy> SortByMap = new Dictionary<string, SortBy>(StringComparer.OrdinalIgnoreCase)  
            {  
                { "none", SortBy.None },  
                { "name", SortBy.Name },  
                { "value", SortBy.Value },  
            };  
  
            private SortBy _sortBy = SortBy.None;  
  
            /// <summary>  
            /// Override the OnExecute method to perform actions when you build a database project.  
            /// </summary>  
            protected override void OnExecute(BuildContributorContext context, IList<ExtensibilityError> errors)  
            {  
                // handle related arguments, passed in as part of  
                // the context information.  
                bool generateModelStatistics;  
                ParseArguments(context.Arguments, errors, out generateModelStatistics);  
  
                // Only generate statistics if requested to do so  
                if (generateModelStatistics)  
                {  
                    // First, output model-wide information, such  
                    // as the type of database schema provider (DSP)  
                    // and the collation.  
                    StringBuilder statisticsMsg = new StringBuilder();  
                    statisticsMsg.AppendLine(" ")  
                                 .AppendLine("Model Statistics:")  
                                 .AppendLine("===")  
                                 .AppendLine(" ");  
                    errors.Add(new ExtensibilityError(statisticsMsg.ToString(), Severity.Message));  
  
                    var model = context.Model;  
  
                    // Start building up the XML that will later  
                    // be serialized.  
                    var xRoot = new XElement("ModelStatistics");  
  
                    SummarizeModelInfo(model, xRoot, errors);  
  
                    // First, count the elements that are contained   
                    // in this model.  
                    IList<TSqlObject> elements = model.GetObjects(DacQueryScopes.UserDefined).ToList();  
                    Summarize(elements, element => element.ObjectType.Name, "UserDefinedElements", xRoot, errors);  
  
                    // Now, count the elements that are defined in  
                    // another model. Examples include built-in types,  
                    // roles, filegroups, assemblies, and any   
                    // referenced objects from another database.  
                    elements = model.GetObjects(DacQueryScopes.BuiltIn | DacQueryScopes.SameDatabase | DacQueryScopes.System).ToList();  
                    Summarize(elements, element => element.ObjectType.Name, "OtherElements", xRoot, errors);  
  
                    // Now, count the number of each type  
                    // of relationship in the model.  
                    SurveyRelationships(model, xRoot, errors);  
  
                    // Determine where the user wants to save  
                    // the serialized XML file.  
                    string outDir;  
                    if (context.Arguments.TryGetValue(OutDir, out outDir) == false)  
                    {  
                        outDir = ".";  
                    }  
                    string filePath = Path.Combine(outDir, ModelStatisticsFilename);  
                    // Save the XML file and tell the user  
                    // where it was saved.  
                    xRoot.Save(filePath);  
                    ExtensibilityError resultArg = new ExtensibilityError("Result was saved to " + filePath, Severity.Message);  
                    errors.Add(resultArg);  
                }  
            }  
  
            /// <summary>  
            /// Examine the arguments provided by the user  
            /// to determine if model statistics should be generated  
            /// and, if so, how the results should be sorted.  
            /// </summary>  
            private void ParseArguments(IDictionary<string, string> arguments, IList<ExtensibilityError> errors, out bool generateModelStatistics)  
            {  
                // By default, we don't generate model statistics  
                generateModelStatistics = false;  
  
                // see if the user provided the GenerateModelStatistics   
                // option and if so, what value was it given.  
                string valueString;  
                arguments.TryGetValue(GenerateModelStatistics, out valueString);  
                if (string.IsNullOrWhiteSpace(valueString) == false)  
                {  
                    if (bool.TryParse(valueString, out generateModelStatistics) == false)  
                    {  
                        generateModelStatistics = false;  
  
                        // The value was not valid from the end user  
                        ExtensibilityError invalidArg = new ExtensibilityError(  
                            GenerateModelStatistics + "=" + valueString + " was not valid.  It can be true or false", Severity.Error);  
                        errors.Add(invalidArg);  
                        return;  
                    }  
                }  
  
                // Only worry about sort order if the user requested  
                // that we generate model statistics.  
                if (generateModelStatistics)  
                {  
                    // see if the user provided the sort option and  
                    // if so, what value was provided.  
                    arguments.TryGetValue(SortModelStatisticsBy, out valueString);  
                    if (string.IsNullOrWhiteSpace(valueString) == false)  
                    {  
                        SortBy sortBy;  
                        if (SortByMap.TryGetValue(valueString, out sortBy))  
                        {  
                            _sortBy = sortBy;  
                        }  
                        else  
                        {  
                            // The value was not valid from the end user  
                            ExtensibilityError invalidArg = new ExtensibilityError(  
                                SortModelStatisticsBy + "=" + valueString + " was not valid.  It can be none, name, or value", Severity.Error);  
                            errors.Add(invalidArg);  
                        }  
                    }  
                }  
            }  
  
            /// <summary>  
            /// Retrieve the database schema provider for the  
            /// model and the collation of that model.  
            /// Results are output to the console and added to the XML  
            /// being constructed.  
            /// </summary>  
            private static void SummarizeModelInfo(TSqlModel model, XElement xContainer, IList<ExtensibilityError> errors)  
            {  
                // use a Dictionary to accumulate the information  
                // that will later be output.  
                var info = new Dictionary<string, string>();  
  
                // Two things of interest: the database schema  
                // provider for the model, and the language id and  
                // case sensitivity of the collation of that  
                // model  
                info.Add("Version", model.Version.ToString());  
  
                TSqlObject options = model.GetObjects(DacQueryScopes.UserDefined, DatabaseOptions.TypeClass).FirstOrDefault();  
                if (options != null)  
                {  
                    info.Add("Collation", options.GetProperty<string>(DatabaseOptions.Collation));  
                }  
  
                // Output the accumulated information and add it to   
                // the XML.  
                OutputResult("Basic model info", info, xContainer, errors);  
            }  
  
            /// <summary>  
            /// For a provided list of model elements, count the number  
            /// of elements for each class name, sorted as specified  
            /// by the user.  
            /// Results are output to the console and added to the XML  
            /// being constructed.  
            /// </summary>  
            private void Summarize<T>(IList<T> set, Func<T, string> groupValue, string category, XElement xContainer, IList<ExtensibilityError> errors)  
            { // Use a Dictionary to keep all summarized information  
                var statistics = new Dictionary<string, int>();  
  
                // For each element in the provided list,  
                // count items based on the specified grouping  
                var groups =  
                    from item in set  
                    group item by groupValue(item) into g  
                    select new { g.Key, Count = g.Count() };  
  
                // order the groups as requested by the user  
                if (this._sortBy == SortBy.Name)  
                {  
                    groups = groups.OrderBy(group => group.Key);  
                }  
                else if (this._sortBy == SortBy.Value)  
                {  
                    groups = groups.OrderBy(group => group.Count);  
                }  
  
                // build the Dictionary of accumulated statistics  
                // that will be passed along to the OutputResult method.  
                foreach (var item in groups)  
                {  
                    statistics.Add(item.Key, item.Count);  
                }  
  
                statistics.Add("subtotal", set.Count);  
                statistics.Add("total items", groups.Count());  
  
                // output the results, and build up the XML  
                OutputResult(category, statistics, xContainer, errors);  
            }  
  
            /// <summary>  
            /// Iterate over all model elements, counting the  
            /// styles and types for relationships that reference each   
            /// element  
            /// Results are output to the console and added to the XML  
            /// being constructed.  
            /// </summary>  
            private static void SurveyRelationships(TSqlModel model, XElement xContainer, IList<ExtensibilityError> errors)  
            {  
                // get a list that contains all elements in the model  
                var elements = model.GetObjects(DacQueryScopes.All);  
                // We are interested in all relationships that  
                // reference each element.  
                var entries =  
                    from element in elements  
                    from entry in element.GetReferencedRelationshipInstances(DacExternalQueryScopes.All)  
                    select entry;  
  
                // initialize our counting buckets  
                var composing = 0;  
                var hierachical = 0;  
                var peer = 0;  
  
                // process each relationship, adding to the   
                // appropriate bucket for style and type.  
                foreach (var entry in entries)  
                {  
                    switch (entry.Relationship.Type)  
                    {  
                        case RelationshipType.Composing:  
                            ++composing;  
                            break;  
                        case RelationshipType.Hierarchical:  
                            ++hierachical;  
                            break;  
                        case RelationshipType.Peer:  
                            ++peer;  
                            break;  
                        default:  
                            break;  
                    }  
                }  
  
                // build a dictionary of data to pass along  
                // to the OutputResult method.  
                var stat = new Dictionary<string, int>  
                {  
                    {"Composing", composing},  
                    {"Hierarchical", hierachical},  
                    {"Peer", peer},  
                    {"subtotal", entries.Count()}  
                };  
  
                OutputResult("Relationships", stat, xContainer, errors);  
            }  
  
            /// <summary>  
            /// Performs the actual output for this contributor,  
            /// writing the specified set of statistics, and adding any   
            /// output information to the XML being constructed.  
            /// </summary>  
            private static void OutputResult<T>(string category, Dictionary<string, T> statistics, XElement xContainer, IList<ExtensibilityError> errors)  
            {  
                var maxLen = statistics.Max(stat => stat.Key.Length) + 2;  
                var format = string.Format("{{0, {0}}}: {{1}}", maxLen);  
  
                StringBuilder resultMessage = new StringBuilder();  
                //List<ExtensibilityError> args = new List<ExtensibilityError>();  
                resultMessage.AppendLine(category);  
                resultMessage.AppendLine("-----------------");  
  
                // Remove any blank spaces from the category name  
                var xCategory = new XElement(category.Replace(" ", ""));  
                xContainer.Add(xCategory);  
  
                foreach (var item in statistics)  
                {  
                    //Console.WriteLine(format, item.Key, item.Value);  
                    var entry = string.Format(format, item.Key, item.Value);  
                    resultMessage.AppendLine(entry);  
                    // Replace any blank spaces in the element key with  
                    // underscores.  
                    xCategory.Add(new XElement(item.Key.Replace(' ', '_'), item.Value));  
                }  
                resultMessage.AppendLine(" ");  
                errors.Add(new ExtensibilityError(resultMessage.ToString(), Severity.Message));  
            }  
        }  
    }  
  
    ```  
  
    그런 후 클래스 라이브러리를 빌드합니다.  
  
### <a name="to-sign-and-build-the-assembly"></a>어셈블리를 서명하고 빌드하려면  
  
1.  **프로젝트** 메뉴에서 **MyBuildContributor 속성**을 클릭합니다.  
  
2.  **서명** 탭을 클릭합니다.  
  
3.  **어셈블리 서명**을 클릭합니다.  
  
4.  **강력한 이름 키 파일 선택**에서 **<New>** 를 클릭합니다.  
  
5.  **강력한 이름 키 만들기** 대화 상자의 **키 파일 이름**에 **MyRefKey**를 입력합니다.  
  
6.  (선택 사항) 강력한 이름 키 파일에 대한 암호를 지정할 수 있습니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
9. **빌드** 메뉴에서 **솔루션 빌드**를 클릭합니다.  
  
    그런 다음 SQL 프로젝트를 빌드할 때 로드되도록 어셈블리를 설치해야 합니다.  
  
## <a name="install-a-build-contributor"></a><a name="InstallBuildContributor"></a>빌드 참가자 설치  
빌드 참가자를 설치하려면 어셈블리 및 연관된 .pdb 파일을 Extensions 폴더에 복사해야 합니다.  
  
#### <a name="to-install-the-mybuildcontributor-assembly"></a>MyBuildContributor 어셈블리를 설치하려면  
  
1.  이제 어셈블리 정보를 Extensions 디렉터리에 복사합니다. Visual Studio가 시작되면, %Program Files%\Microsoft SQL Server\110\DAC\Bin\Extensions 및 하위 디렉터리에서 확장을 식별하고 이를 사용할 수 있도록 설정합니다.  
  
2.  출력 디렉터리에서 %Program Files%\Microsoft SQL Server\110\DAC\Bin\Extensions 디렉터리로 **MyBuildContributor.dll** 어셈블리를 복사합니다.  
  
    > [!NOTE]  
    > 기본적으로 컴파일된 .dll 파일의 경로는 YourSolutionPath\YourProjectPath\bin\Debug 또는 YourSolutionPath\YourProjectPath\bin\Release입니다.  
  
## <a name="run-or-test-your-build-contributor"></a><a name="TestBuildContributor"></a>빌드 참가자 실행 또는 테스트  
빌드 참가자를 실행 또는 테스트하려면 다음 작업을 수행해야 합니다.  
  
-   빌드하려는 .sqlproj 파일에 속성을 추가합니다.  
  
-   MSBuild를 사용하고 적절한 매개 변수를 제공하여 데이터베이스 프로젝트를 빌드합니다.  
  
### <a name="add-properties-to-the-sql-project-sqlproj-file"></a>SQL 프로젝트(.sqlproj) 파일에 속성 추가  
실행하려는 참가자의 ID를 지정하려면 항상 SQL 프로젝트 파일을 업데이트해야 합니다. 또한 이 빌드 참가자는 MSBuild의 명령줄 매개 변수를 받으므로 사용자가 MSBuild를 통해 이러한 매개 변수를 전달할 수 있도록 SQL 프로젝트를 수정해야 합니다.  
  
이 작업은 다음 두 가지 방법 중 한 가지로 수행할 수 있습니다.  
  
-   .sqlproj 파일을 수동으로 수정해서 필요한 인수를 추가할 수 있습니다. 여러 프로젝트에서 이 빌드 참가자를 다시 사용할 의도가 없으면 이를 수행하도록 선택할 수 있습니다. 이 옵션을 선택할 경우, .sqlproj 파일에서 파일의 첫 번째 가져오기 노드 다음에 다음 문을 추가합니다.  
  
    ```  
    /// <PropertyGroup>  
    ///     <ContributorArguments Condition="'$(Configuration)' == 'Debug'">  
    ///         $(ContributorArguments);ModelStatistics.GenerateModelStatistics=true;ModelStatistics.SortModelStatisticsBy="name";  
    ///     </ContributorArguments>  
    /// <PropertyGroup>  
  
    ```  
  
-   두 번째 방법은 필요한 참가자 인수가 포함된 대상 파일을 만드는 것입니다. 이 방법은 기본값이 포함되기 때문에 여러 프로젝트에 대해 동일한 참가자를 사용하는 경우에 유용합니다.  
  
    이 경우에는 MSBuild 확장 경로에 대상 파일을 만듭니다.  
  
    1.  %Program Files%\MSBuild\\로 이동합니다.  
  
    2.  대상 파일을 저장할 "MyContributors"라는 새 폴더를 만듭니다.  
  
    3.  이 디렉터리 내에 "MyContributors.targets"라는 새 파일을 만들고 다음 텍스트를 추가한 다음, 파일을 저장합니다.  
  
        ```  
        <?xml version="1.0" encoding="utf-8"?>  
  
        <Project xmlns="https://schemas.microsoft.com/developer/msbuild/2003">  
          <PropertyGroup>  
            <BuildContributors>$(BuildContributors);ExampleContributors.ModelStatistics</BuildContributors>  
            <ContributorArguments Condition="'$(Configuration)' == 'Debug'">$(ContributorArguments);ModelStatistics.GenerateModelStatistics=true;ModelStatistics.SortModelStatisticsBy=name;</ContributorArguments>  
          </PropertyGroup>  
        </Project>  
        ```  
  
    4.  참가자를 실행하려는 프로젝트의 .sqlproj 파일 내에서 .sqlproj 파일의 \<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.SqlTasks.targets" \/> 노드 뒤에 다음 문을 추가하여 대상 파일을 가져옵니다.  
  
        ```  
        <Import Project="$(MSBuildExtensionsPath)\MyContributors\MyContributors.targets " />  
        ```  
  
이러한 방법 중 하나에 따라 작업한 후에는 MSBuild를 사용해서 명령줄 빌드에 대한 매개 변수를 전달할 수 있습니다.  
  
> [!NOTE]  
> 참가자 ID를 지정하려면 항상 "BuildContributors" 속성을 업데이트해야 합니다. 이 ID는 기여자 원본 파일의 "ExportBuildContributor" 속성에 사용된 것과 동일한 ID입니다. 이 ID가 없으면 프로젝트를 빌드할 때 참가자가 실행되지 않습니다. "ContributorArguments" 속성은 기여자가 실행하기에 필요한 인수가 있는 경우에만 업데이트해야 합니다.  
  
### <a name="build-the-sql-project"></a>SQL 프로젝트 빌드  
  
##### <a name="to-rebuild-your-database-project-by-using-msbuild-and-generate-statistics"></a>MSBuild를 사용해서 데이터베이스 프로젝트를 다시 빌드하고 통계를 생성하려면  
  
1.  Visual Studio에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 "다시 빌드"를 선택합니다. 그러면 프로젝트가 다시 빌드되고 모델 통계가 생성되며, 해당 결과가 빌드 출력에 포함되고 ModelStatistics.xml에 저장됩니다. xml 파일을 보려면 솔루션 탐색기에서 "모든 파일 표시"를 선택해야 할 수 있습니다.  
  
2.  Visual Studio 명령 프롬프트 열기: **시작** 메뉴에서 **모든 프로그램**, **Microsoft Visual Studio <Visual Studio Version>**, **Visual Studio Tools**, **Visual Studio 명령 프롬프트(<Visual Studio Version>)** 를 차례로 클릭합니다.  
  
3.  명령 프롬프트에서 SQL 프로젝트가 있는 폴더로 이동합니다.  
  
4.  명령 프롬프트에서 다음 명령을 입력합니다.  
  
    ```  
    MSBuild /t:Rebuild MyDatabaseProject.sqlproj /p:BuildContributors=$(BuildContributors);ExampleContributors.ModelStatistics /p:ContributorArguments=$(ContributorArguments);GenerateModelStatistics=true;SortModelStatisticsBy=name;OutDir=.\;  
    ```  
  
    *MyDatabaseProject* 를 빌드하려는 데이터베이스 프로젝트의 이름으로 바꿉니다. 프로젝트가 마지막으로 빌드된 후 변경되었으면 /t:Rebuild 대신 /t:Build를 사용할 수 있습니다.  
  
    출력 내에는 다음과 비슷한 빌드 정보가 표시됩니다.  
  
```  
Model Statistics:  
===  
  
Basic model info  
-----------------  
    Version: Sql110  
  Collation: SQL_Latin1_General_CP1_CI_AS  
  
UserDefinedElements  
-----------------  
  DatabaseOptions: 1  
         subtotal: 1  
      total items: 1  
  
OtherElements  
-----------------  
                Assembly: 1  
       BuiltInServerRole: 9  
           ClrTypeMethod: 218  
  ClrTypeMethodParameter: 197  
         ClrTypeProperty: 20  
                Contract: 6  
                DataType: 34  
                Endpoint: 5  
               Filegroup: 1  
             MessageType: 14  
                   Queue: 3  
                    Role: 10  
                  Schema: 13  
                 Service: 3  
                    User: 4  
         UserDefinedType: 3  
                subtotal: 541  
             total items: 16  
  
Relationships  
-----------------  
     Composing: 477  
  Hierarchical: 6  
          Peer: 19  
      subtotal: 502  
  
```  
  
1.  ModelStatistics.xml을 열고 내용을 확인합니다.  
  
    보고된 결과는 XML 파일에도 저장됩니다.  
  
## <a name="next-steps"></a>다음 단계  
출력 XML 파일의 처리를 수행하기 위한 추가 도구를 만들 수도 있습니다. 이 예는 빌드 참가자의 한 가지 예일 뿐입니다. 예를 들어 빌드의 일부로 데이터 사전 파일을 출력하는 빌드 참가자를 만들 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[빌드 및 배포 참가자를 사용하여 데이터베이스 빌드 및 배포 사용자 지정](../ssdt/use-deployment-contributors-to-customize-database-build-and-deployment.md)  
[연습: 데이터베이스 프로젝트 배포를 확장하여 배포 계획 분석](../ssdt/walkthrough-extend-database-project-deployment-to-analyze-the-deployment-plan.md)  
