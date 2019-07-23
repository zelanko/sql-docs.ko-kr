---
title: '연습: 데이터베이스 프로젝트 배포를 확장하여 배포 계획 분석 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 9ead8470-93ba-44e3-8848-b59322e37621
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 167667590df0b2172e05674c462cfa9833d45acd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912783"
---
# <a name="walkthrough-extend-database-project-deployment-to-analyze-the-deployment-plan"></a>연습: 데이터베이스 프로젝트 배포를 확장하여 배포 계획 분석
배포 참가자를 만들어서 SQL 프로젝트를 배포할 때 사용자 지정 작업을 수행할 수 있습니다. 배포 참가자는 DeploymentPlanModifier 또는 DeploymentPlanExecutor 중에서 만들 수 있습니다. DeploymentPlanModifier를 사용하면 계획을 실행하기 전에 항목을 변경할 수 있고 DeploymentPlanExecutor를 사용하면 계획을 실행하는 동안 작업을 수행할 수 있습니다. 이 연습에서는 데이터베이스 프로젝트를 배포할 때 수행된 작업에 대한 보고서를 만드는 DeploymentUpdateReportContributor라는 DeploymentPlanExecutor를 만듭니다. 이 빌드 참가자는 보고서가 생성되는지 여부를 제어하기 위한 매개 변수를 받기 때문에 추가 필수 단계를 수행해야 합니다.  
  
이 연습에서 수행하는 주요 작업은 다음과 같습니다.  
  
-   [DeploymentPlanExecutor 유형의 배포 참가자 만들기](#CreateDeploymentContributor)  
  
-   [배포 참가자 설치](#InstallDeploymentContributor)  
  
-   [배포 참가자 테스트](#TestDeploymentContributor)  
  
## <a name="prerequisites"></a>사전 요구 사항  
이 연습을 완료하려면 다음과 같은 구성 요소가 필요합니다.  
  
-   SSDT(SQL Server Data Tools)가 포함되고 C# 또는 VB 개발이 지원되는 Visual Studio 버전이 설치되어 있어야 합니다.  
  
-   SQL 개체가 포함된 SQL 프로젝트가 있어야 합니다.  
  
-   데이터베이스 프로젝트를 배포할 수 있는 SQL Server 인스턴스가 필요합니다.  
  
> [!NOTE]  
> 이 연습은 SSDT의 SQL 기능에 익숙한 사용자를 대상으로 합니다. 또한 코드 클래스를 만드는 방법 및 코드 편집기를 사용해서 클래스에 코드를 추가하는 방법과 같은 기본적인 Visual Studio 개념에 대해서도 익숙해야 합니다.  
  
## <a name="CreateDeploymentContributor"></a>배포 참가자 만들기  
배포 참가자를 만들려면 다음 작업을 수행해야 합니다.  
  
-   클래스 라이브러리 프로젝트를 만들고 필요한 참조를 추가합니다.  
  
-   [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx)로부터 상속되는 DeploymentUpdateReportContributor라는 클래스를 정의합니다.  
  
-   OnExecute 메서드를 재정의합니다.  
  
-   프라이빗 도우미 클래스를 추가합니다.  
  
-   결과 어셈블리를 빌드합니다.  
  
#### <a name="to-create-a-class-library-project"></a>클래스 라이브러리 프로젝트를 만들려면  
  
1.  MyDeploymentContributor라는 이름의 Visual Basic 또는 Visual C# 클래스 라이브러리 프로젝트를 만듭니다.  
  
2.  “Class1.cs” 파일 이름을 “DeploymentUpdateReportContributor.cs”로 바꿉니다.  
  
3.  솔루션 탐색기에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭한 후 **참조 추가**를 클릭합니다.  
  
4.  [프레임워크] 탭에서 **System.ComponentModel.Composition**을 선택합니다.  
  
5.  필요한 SQL 참조 추가: 프로젝트 노드를 마우스 오른쪽 단추로 클릭한 후 **참조 추가**를 클릭합니다. **찾아보기**를 클릭하고 **C:\Program Files (x86)\Microsoft SQL Server\110\DAC\Bin** 폴더로 이동합니다. **Microsoft.SqlServer.Dac.dll**, **Microsoft.SqlServer.Dac.Extensions.dll** 및 **Microsoft.Data.Tools.Schema.Sql.dll** 항목을 선택하고 **추가**를 클릭한 후 **확인**을 클릭합니다.  
  
    그런 후 클래스에 코드 추가를 시작합니다.  
  
#### <a name="to-define-the-deploymentupdatereportcontributor-class"></a>DeploymentUpdateReportContributor 클래스를 정의하려면  
  
1.  코드 편집기에서 다음 **using** 문과 일치하도록 DeploymentUpdateReportContributor.cs 파일을 업데이트합니다.  
  
    ```csharp  
    using System;  
    using System.IO;  
    using System.Text;  
    using System.Xml;  
    using Microsoft.SqlServer.Dac.Deployment;  
    using Microsoft.SqlServer.Dac.Extensibility;  
    using Microsoft.SqlServer.Dac.Model;  
  
    ```  
  
2.  다음과 일치하도록 클래스 정의를 업데이트합니다.  
  
    ```csharp  
    /// <summary>  
        /// An executor that generates a report detailing the steps in the deployment plan. Will only run  
        /// if a "GenerateUpdateReport=true" contributor argument is set in the project file, in a targets file or  
        /// passed as an additional argument to the DacServices API. To set in a project file, add the following:  
        ///   
        /// <PropertyGroup>  
        ///     <ContributorArguments Condition="'$(Configuration)' == 'Debug'">  
        /// $(ContributorArguments);DeploymentUpdateReportContributor.GenerateUpdateReport=true;  
        ///     </ContributorArguments>  
        /// <PropertyGroup>  
        ///   
        /// </summary>  
        [ExportDeploymentPlanExecutor("MyDeploymentContributor.DeploymentUpdateReportContributor", "1.0.0.0")]  
        public class DeploymentUpdateReportContributor : DeploymentPlanExecutor  
        {  
        }  
  
    ```  
  
    이제 DeploymentPlanExecutor로부터 상속되는 배포 참가자가 정의되었습니다. 빌드 및 배포 프로세스 중에 사용자 지정 참가자가 표준 확장 디렉터리에서 로드됩니다. 배포 계획 Executor 참가자는 [ExportDeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.exportdeploymentplanexecutorattribute.aspx) 특성으로 식별됩니다.  
  
    이 특성은 참가자를 검색하는 데 필요합니다. 결과는 다음과 비슷합니다.  
  
    ```csharp  
    [ExportDeploymentPlanExecutor("MyDeploymentContributor.DeploymentUpdateReportContributor", "1.0.0.0")]  
  
    ```  
  
    이 경우 특성의 첫 번째 매개 변수는 고유 식별자여야 하며, 이 식별자는 프로젝트 파일에서 기여자를 식별하는 데 사용됩니다. 식별자를 만들 때는 라이브러리의 네임스페이스(이 연습에서는 MyDeploymentContributor)를 클래스 이름(이 연습에서는 DeploymentUpdateReportContributor)과 결합하는 것이 가장 좋습니다.  
  
3.  그런 다음 이 공급자가 명령줄 매개 변수를 받도록 설정하기 위해 사용할 다음 멤버를 추가합니다.  
  
    ```csharp  
    public const string GenerateUpdateReport = "DeploymentUpdateReportContributor.GenerateUpdateReport";  
    ```  
  
    이 멤버는 사용자가 GenerateUpdateReport 옵션을 사용해서 보고서를 생성할지 여부를 지정할 수 있게 해줍니다.  
  
    그런 다음 데이터베이스 프로젝트를 배포할 때 실행할 코드를 추가하도록 OnExecute 메서드를 재정의합니다.  
  
#### <a name="to-override-onexecute"></a>OnExecute를 재정의하려면  
  
-   DeploymentUpdateReportContributor 클래스에 다음 메서드를 추가합니다.  
  
    ```csharp  
    /// <summary>  
            /// Override the OnExecute method to perform actions when you execute the deployment plan for  
            /// a database project.  
            /// </summary>  
            protected override void OnExecute(DeploymentPlanContributorContext context)  
            {  
                // determine whether the user specified a report is to be generated  
                bool generateReport = false;  
                string generateReportValue;  
                if (context.Arguments.TryGetValue(GenerateUpdateReport, out generateReportValue) == false)  
                {  
                    // couldn't find the GenerateUpdateReport argument, so do not generate  
                    generateReport = false;  
                }  
                else  
                {  
                    // GenerateUpdateReport argument was specified, try to parse the value  
                    if (bool.TryParse(generateReportValue, out generateReport))  
                    {  
                        // if we end up here, the value for the argument was not valid.  
                        // default is false, so do nothing.  
                    }  
                }  
  
                if (generateReport == false)  
                {  
                    // if user does not want to generate a report, we are done  
                    return;  
                }  
  
                // We will output to the same directory where the deployment script  
                // is output or to the current directory  
                string reportPrefix = context.Options.TargetDatabaseName;  
                string reportPath;  
                if (string.IsNullOrEmpty(context.DeploymentScriptPath))  
                {  
                    reportPath = Environment.CurrentDirectory;  
                }  
                else  
                {  
                    reportPath = Path.GetDirectoryName(context.DeploymentScriptPath);  
                }  
                FileInfo summaryReportFile = new FileInfo(Path.Combine(reportPath, reportPrefix + ".summary.xml"));  
                FileInfo detailsReportFile = new FileInfo(Path.Combine(reportPath, reportPrefix + ".details.xml"));  
  
                // Generate the reports by using the helper class DeploymentReportWriter  
                DeploymentReportWriter writer = new DeploymentReportWriter(context);  
                writer.WriteReport(summaryReportFile);  
                writer.IncludeScripts = true;  
                writer.WriteReport(detailsReportFile);  
  
                string msg = "Deployment reports ->"  
                    + Environment.NewLine + summaryReportFile.FullName  
                    + Environment.NewLine + detailsReportFile.FullName;  
  
                ExtensibilityError reportMsg = new ExtensibilityError(msg, Severity.Message);  
                base.PublishMessage(reportMsg);  
            }  
        /// <summary>  
        /// Override the OnExecute method to perform actions when you execute the deployment plan for  
        /// a database project.  
        /// </summary>  
            protected override void OnExecute(DeploymentPlanContributorContext context)  
            {  
                // determine whether the user specified a report is to be generated  
                bool generateReport = false;  
                string generateReportValue;  
                if (context.Arguments.TryGetValue(GenerateUpdateReport, out generateReportValue) == false)  
                {  
                    // couldn't find the GenerateUpdateReport argument, so do not generate  
                    generateReport = false;  
                }  
                else  
                {  
                    // GenerateUpdateReport argument was specified, try to parse the value  
                    if (bool.TryParse(generateReportValue, out generateReport))  
                    {  
                        // if we end up here, the value for the argument was not valid.  
                        // default is false, so do nothing.  
                    }  
                }  
  
                if (generateReport == false)  
                {  
                    // if user does not want to generate a report, we are done  
                    return;  
                }  
  
                // We will output to the same directory where the deployment script  
                // is output or to the current directory  
                string reportPrefix = context.Options.TargetDatabaseName;  
                string reportPath;  
                if (string.IsNullOrEmpty(context.DeploymentScriptPath))  
                {  
                    reportPath = Environment.CurrentDirectory;  
                }  
                else  
                {  
                    reportPath = Path.GetDirectoryName(context.DeploymentScriptPath);  
                }  
                FileInfo summaryReportFile = new FileInfo(Path.Combine(reportPath, reportPrefix + ".summary.xml"));  
                FileInfo detailsReportFile = new FileInfo(Path.Combine(reportPath, reportPrefix + ".details.xml"));  
  
                // Generate the reports by using the helper class DeploymentReportWriter  
                DeploymentReportWriter writer = new DeploymentReportWriter(context);  
                writer.WriteReport(summaryReportFile);  
                writer.IncludeScripts = true;  
                writer.WriteReport(detailsReportFile);  
  
                string msg = "Deployment reports ->"  
                    + Environment.NewLine + summaryReportFile.FullName  
                    + Environment.NewLine + detailsReportFile.FullName;  
  
                DataSchemaError reportMsg = new DataSchemaError(msg, ErrorSeverity.Message);  
                base.PublishMessage(reportMsg);  
            }  
    ```  
  
    OnExecute 메서드에는 지정된 모든 인수, 원본 및 대상 데이터베이스 모델, 빌드 속성 및 확장 파일에 대한 액세스를 제공하는 [DeploymentPlanContributorContext](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributorcontext.aspx) 개체가 전달됩니다. 이 예에서는 모델을 가져온 후 모델에 대한 정보를 출력하기 위한 도우미 함수를 호출합니다. 기본 클래스에서 PublishMessage 도우미 메서드를 사용하여 발생한 모든 오류를 보고합니다.  
  
    중요한 추가 유형 및 메서드는 다음과 같습니다. [TSqlModel](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlmodel.aspx), [ModelComparisonResult](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.modelcomparisonresult.aspx), [DeploymentPlanHandle](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanhandle.aspx) 및 [SqlDeploymentOptions](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqldeploymentoptions.aspx).  
  
    그런 다음 배포 계획의 세부 정보를 자세히 살펴보는 도우미 클래스를 정의합니다.  
  
#### <a name="to-add-the-helper-class-that-generates-the-report-body"></a>보고서 본문을 생성하는 도우미 클래스를 추가하려면  
  
-   다음 코드를 추가하여 도우미 클래스 및 해당 멤버를 추가합니다.  
  
    ```csharp  
    /// <summary>  
            /// This class is used to generate a deployment  
            /// report.   
            /// </summary>  
            private class DeploymentReportWriter  
            {  
                readonly TSqlModel _sourceModel;  
                readonly ModelComparisonResult _diff;  
                readonly DeploymentStep _planHead;  
  
                /// <summary>  
                /// The constructor accepts the same context info  
                /// that was passed to the OnExecute method of the  
                /// deployment contributor.  
                /// </summary>  
                public DeploymentReportWriter(DeploymentPlanContributorContext context)  
                {  
                    if (context == null)  
                    {  
                        throw new ArgumentNullException("context");  
                    }  
  
                    // save the source model, source/target differences,  
                    // and the beginning of the deployment plan.  
                    _sourceModel = context.Source;  
                    _diff = context.ComparisonResult;  
                    _planHead = context.PlanHandle.Head;  
                }  
                /// <summary>  
                /// Property indicating whether script bodies  
                /// should be included in the report.  
                /// </summary>  
                public bool IncludeScripts { get; set; }  
  
                /// <summary>  
                /// Drives the report generation, opening files,   
                /// writing the beginning and ending report elements,  
                /// and calling helper methods to report on the  
                /// plan operations.  
                /// </summary>  
                internal void WriteReport(FileInfo reportFile)  
                {// Assumes that we have a valid report file  
                    if (reportFile == null)  
                    {  
                        throw new ArgumentNullException("reportFile");  
                    }  
  
                    // set up the XML writer  
                    XmlWriterSettings xmlws = new XmlWriterSettings();  
                    // Indentation makes it a bit more readable  
                    xmlws.Indent = true;  
                    FileStream fs = new FileStream(reportFile.FullName, FileMode.Create, FileAccess.Write, FileShare.ReadWrite);  
                    XmlWriter xmlw = XmlWriter.Create(fs, xmlws);  
  
                    try  
                    {  
                        xmlw.WriteStartDocument(true);  
                        xmlw.WriteStartElement("DeploymentReport");  
  
                        // Summary report of the operations that  
                        // are contained in the plan.  
                        ReportPlanOperations(xmlw);  
  
                        // You could add a method call here  
                        // to produce a detailed listing of the   
                        // differences between the source and  
                        // target model.  
                        xmlw.WriteEndElement();  
                        xmlw.WriteEndDocument();  
                        xmlw.Flush();  
                        fs.Flush();  
                    }  
                    finally  
                    {  
                        xmlw.Close();  
                        fs.Dispose();  
                    }  
                }  
  
                /// <summary>  
                /// Writes details for the various operation types  
                /// that could be contained in the deployment plan.  
                /// Optionally writes script bodies, depending on  
                /// the value of the IncludeScripts property.  
                /// </summary>  
                private void ReportPlanOperations(XmlWriter xmlw)  
                {// write the node to indicate the start  
                    // of the list of operations.  
                    xmlw.WriteStartElement("Operations");  
  
                    // Loop through the steps in the plan,  
                    // starting at the beginning.  
                    DeploymentStep currentStep = _planHead;  
                    while (currentStep != null)  
                    {  
                        // Report the type of step  
                        xmlw.WriteStartElement(currentStep.GetType().Name);  
  
                        // based on the type of step, report  
                        // the relevant information.  
                        // Note that this procedure only handles   
                        // a subset of all step types.  
                        if (currentStep is SqlRenameStep)  
                        {  
                            SqlRenameStep renameStep = (SqlRenameStep)currentStep;  
                            xmlw.WriteAttributeString("OriginalName", renameStep.OldName);  
                            xmlw.WriteAttributeString("NewName", renameStep.NewName);  
                            xmlw.WriteAttributeString("Category", GetElementCategory(renameStep.RenamedElement));  
                        }  
                        else if (currentStep is SqlMoveSchemaStep)  
                        {  
                            SqlMoveSchemaStep moveStep = (SqlMoveSchemaStep)currentStep;  
                            xmlw.WriteAttributeString("OrignalName", moveStep.PreviousName);  
                            xmlw.WriteAttributeString("NewSchema", moveStep.NewSchema);  
                            xmlw.WriteAttributeString("Category", GetElementCategory(moveStep.MovedElement));  
                        }  
                        else if (currentStep is SqlTableMigrationStep)  
                        {  
                            SqlTableMigrationStep dmStep = (SqlTableMigrationStep)currentStep;  
                            xmlw.WriteAttributeString("Name", GetElementName(dmStep.SourceTable));  
                            xmlw.WriteAttributeString("Category", GetElementCategory(dmStep.SourceElement));  
                        }  
                        else if (currentStep is CreateElementStep)  
                        {  
                            CreateElementStep createStep = (CreateElementStep)currentStep;  
                            xmlw.WriteAttributeString("Name", GetElementName(createStep.SourceElement));  
                            xmlw.WriteAttributeString("Category", GetElementCategory(createStep.SourceElement));  
                        }  
                        else if (currentStep is AlterElementStep)  
                        {  
                            AlterElementStep alterStep = (AlterElementStep)currentStep;  
                            xmlw.WriteAttributeString("Name", GetElementName(alterStep.SourceElement));  
                            xmlw.WriteAttributeString("Category", GetElementCategory(alterStep.SourceElement));  
                        }  
                        else if (currentStep is DropElementStep)  
                        {  
                            DropElementStep dropStep = (DropElementStep)currentStep;  
                            xmlw.WriteAttributeString("Name", GetElementName(dropStep.TargetElement));  
                            xmlw.WriteAttributeString("Category", GetElementCategory(dropStep.TargetElement));  
                        }  
  
                        // If the script bodies are to be included,  
                        // add them to the report.  
                        if (this.IncludeScripts)  
                        {  
                            using (StringWriter sw = new StringWriter())  
                            {  
                                currentStep.GenerateBatchScript(sw);  
                                string tsqlBody = sw.ToString();  
                                if (string.IsNullOrEmpty(tsqlBody) == false)  
                                {  
                                    xmlw.WriteCData(tsqlBody);  
                                }  
                            }  
                        }  
  
                        // close off the current step  
                        xmlw.WriteEndElement();  
                        currentStep = currentStep.Next;  
                    }  
                    xmlw.WriteEndElement();  
                }  
  
                /// <summary>  
                /// Returns the category of the specified element  
                /// in the source model  
                /// </summary>  
                private string GetElementCategory(TSqlObject element)  
                {  
                    return element.ObjectType.Name;  
                }  
  
                /// <summary>  
                /// Returns the name of the specified element  
                /// in the source model  
                /// </summary>  
                private static string GetElementName(TSqlObject element)  
                {  
                    StringBuilder name = new StringBuilder();  
                    if (element.Name.HasExternalParts)  
                    {  
                        foreach (string part in element.Name.ExternalParts)  
                        {  
                            if (name.Length > 0)  
                            {  
                                name.Append('.');  
                            }  
                            name.AppendFormat("[{0}]", part);  
                        }  
                    }  
  
                    foreach (string part in element.Name.Parts)  
                    {  
                        if (name.Length > 0)  
                        {  
                            name.Append('.');  
                        }  
                        name.AppendFormat("[{0}]", part);  
                    }  
  
                    return name.ToString();  
                }  
            }        /// <summary>  
            /// This class is used to generate a deployment  
            /// report.   
            /// </summary>  
            private class DeploymentReportWriter  
            {  
                /// <summary>  
                /// The constructor accepts the same context info  
                /// that was passed to the OnExecute method of the  
                /// deployment contributor.  
                /// </summary>  
                public DeploymentReportWriter(DeploymentPlanContributorContext context)  
                {  
               }  
                /// <summary>  
                /// Property indicating whether script bodies  
                /// should be included in the report.  
                /// </summary>  
                public bool IncludeScripts { get; set; }  
  
                /// <summary>  
                /// Drives the report generation, opening files,   
                /// writing the beginning and ending report elements,  
                /// and calling helper methods to report on the  
                /// plan operations.  
                /// </summary>  
                internal void WriteReport(FileInfo reportFile)  
                {  
                }  
  
                /// <summary>  
                /// Writes details for the various operation types  
                /// that could be contained in the deployment plan.  
                /// Optionally writes script bodies, depending on  
                /// the value of the IncludeScripts property.  
                /// </summary>  
                private void ReportPlanOperations(XmlWriter xmlw)  
                {  
                }  
  
                /// <summary>  
                /// Returns the category of the specified element  
                /// in the source model  
                /// </summary>  
                private string GetElementCategory(IModelElement element)  
                {  
                }  
  
                /// <summary>  
                /// Returns the name of the specified element  
                /// in the source model  
                /// </summary>  
                private string GetElementName(IModelElement element)  
                {  
                }  
            }  
    ```  
  
-   변경 내용을 클래스 파일에 저장합니다. 도우미 클래스에는 다음과 같은 여러 가지 유용한 유형이 참조됩니다.  
  
    |**코드 영역**|**유용한 유형**|  
    |-----------------|--------------------|  
    |클래스 멤버|[TSqlModel](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlmodel.aspx), [ModelComparisonResult](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.modelcomparisonresult.aspx), [DeploymentStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentstep.aspx)|  
    |WriteReport 메서드|XmlWriter 및 XmlWriterSettings|  
    |ReportPlanOperations 메서드|중요한 유형에는 다음이 포함됩니다. [DeploymentStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentstep.aspx), [SqlRenameStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqlrenamestep.aspx), [SqlMoveSchemaStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqlmoveschemastep.aspx), [SqlTableMigrationStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqltablemigrationstep.aspx), [CreateElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.createelementstep.aspx), [AlterElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.alterelementstep.aspx), [DropElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.dropelementstep.aspx).<br /><br />이외에도 다른 여러 단계가 있습니다. 전체 단계 목록은 API 설명서를 참조하세요.|  
    |GetElementCategory|[TSqlObject](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlobject.aspx)|  
    |GetElementName|[TSqlObject](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlobject.aspx)|  
  
    그런 후 클래스 라이브러리를 빌드합니다.  
  
#### <a name="to-sign-and-build-the-assembly"></a>어셈블리를 서명하고 빌드하려면  
  
1.  **프로젝트** 메뉴에서 **MyDeploymentContributor** 속성을 클릭합니다.  
  
2.  **서명** 탭을 클릭합니다.  
  
3.  **어셈블리 서명**을 클릭합니다.  
  
4.  **강력한 이름 키 파일 선택**에서 **<New>** 를 클릭합니다.  
  
5.  **강력한 이름 키 만들기** 대화 상자의 **키 파일 이름**에 **MyRefKey**를 입력합니다.  
  
6.  (선택 사항) 강력한 이름 키 파일에 대한 암호를 지정할 수 있습니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
9. **빌드** 메뉴에서 **솔루션 빌드**를 클릭합니다.  
  
그런 다음 SQL 프로젝트를 빌드 및 배포할 때 로드되도록 어셈블리를 설치해야 합니다.  
  
## <a name="InstallDeploymentContributor"></a>배포 참가자 설치  
배포 참가자를 설치하려면 어셈블리 및 연관된 .pdb 파일을 Extensions 폴더에 복사해야 합니다.  
  
#### <a name="to-install-the-mydeploymentcontributor-assembly"></a>MyDeploymentContributor 어셈블리를 설치하려면  
  
-   이제 어셈블리 정보를 Extensions 디렉터리에 복사합니다. Visual Studio가 시작되면, %Program Files%\Microsoft SQL Server\110\DAC\Bin\Extensions 및 하위 디렉터리에서 확장을 식별하고 이를 사용할 수 있도록 설정합니다.  
  
-   출력 디렉터리에서 %Program Files%\Microsoft SQL Server\110\DAC\Bin\Extensions 디렉터리로 **MyDeploymentContributor.dll** 어셈블리를 복사합니다. 기본적으로 컴파일된 .dll 파일의 경로는 YourSolutionPath\YourProjectPath\bin\Debug 또는 YourSolutionPath\YourProjectPath\bin\Release입니다.  
  
## <a name="TestDeploymentContributor"></a>배포 참가자 테스트  
배포 참가자를 테스트하려면 다음 작업을 수행해야 합니다.  
  
-   배포하려는 .sqlproj 파일에 속성을 추가합니다.  
  
-   MSBuild를 사용하고 적절한 매개 변수를 제공하여 프로젝트를 배포합니다.  
  
### <a name="add-properties-to-the-sql-project-sqlproj-file"></a>SQL 프로젝트(.sqlproj) 파일에 속성 추가  
실행하려는 참가자의 ID를 지정하려면 항상 SQL 프로젝트 파일을 업데이트해야 합니다. 또한 이 기여자에는 “GenerateUpdateReport” 인수가 필요하기 때문에 이를 기여자 인수로 지정해야 합니다.  
  
이 작업은 다음 두 가지 방법 중 한 가지로 수행할 수 있습니다. .sqlproj 파일을 수동으로 수정해서 필요한 인수를 추가할 수 있습니다. 참가자가 구성에 필요한 검토 인수를 포함하지 않는 경우 또는 대량의 프로젝트에서 참가자를 다시 사용하지 않으려는 경우에는 이 작업을 선택해서 수행할 수 있습니다. 이 옵션을 선택할 경우, .sqlproj 파일에서 파일의 첫 번째 가져오기 노드 다음에 다음 문을 추가합니다.  
  
```  
<PropertyGroup>  
    <DeploymentContributors>$(DeploymentContributors); MyDeploymentContributor.DeploymentUpdateReportContributor</DeploymentContributors>  
<ContributorArguments Condition="'$(Configuration)' == 'Debug'">$(ContributorArguments);DeploymentUpdateReportContributor.GenerateUpdateReport=true;</ContributorArguments>  
  </PropertyGroup>  
```  
  
두 번째 방법은 필요한 참가자 인수가 포함된 대상 파일을 만드는 것입니다. 이 방법은 기본값이 포함되기 때문에 여러 프로젝트에 대해 동일한 참가자를 사용하고, 필요한 참가자 인수가 포함된 경우에 유용합니다. 이 경우에는 MSBuild 확장 경로에 대상 파일을 만듭니다.  
  
1.  %Program Files%\MSBuild로 이동합니다.  
  
2.  대상 파일을 저장할 "MyContributors"라는 새 폴더를 만듭니다.  
  
3.  이 디렉터리 내에 “MyContributors.targets”라는 새 파일을 만들고 다음 텍스트를 추가하여 파일을 저장합니다.  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
  
    <Project xmlns="https://schemas.microsoft.com/developer/msbuild/2003">  
      <PropertyGroup>  
    <DeploymentContributors>$(DeploymentContributors);MyDeploymentContributor.DeploymentUpdateReportContributor</DeploymentContributors>  
    <ContributorArguments Condition="'$(Configuration)' == 'Debug'">$(ContributorArguments); DeploymentUpdateReportContributor.GenerateUpdateReport=true;</ContributorArguments>  
      </PropertyGroup>  
    </Project>  
    ```  
  
4.  참가자를 실행하려는 프로젝트의 .sqlproj 파일 내에서 \<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.SqlTasks.targets" \/> 노드 뒤에 다음 문을 추가하여 대상 파일을 가져옵니다.  
  
    ```  
    <Import Project="$(MSBuildExtensionsPath)\MyContributors\MyContributors.targets " />  
    ```  
  
이러한 방법 중 하나에 따라 작업한 후에는 MSBuild를 사용해서 명령줄 빌드에 대한 매개 변수를 전달할 수 있습니다.  
  
> [!NOTE]  
> 참가자 ID를 지정하려면 항상 "DeploymentContributors" 속성을 업데이트해야 합니다. 이 ID는 기여자 원본 파일에서 “ExportDeploymentPlanExecutor” 특성에 사용된 것과 동일한 ID입니다. 이 ID가 없으면 프로젝트를 빌드할 때 참가자가 실행되지 않습니다. “ContributorArguments” 속성은 기여자가 실행하기 위해 필요한 인수가 있는 경우에만 업데이트해야 합니다.  
  
### <a name="deploy-the-database-project"></a>데이터베이스 프로젝트 배포  
프로젝트는 Visual Studio 내에서 일반적으로 게시 및 배포할 수 있습니다. SQL 프로젝트가 포함된 솔루션을 열고 프로젝트에 대한 오른쪽 마우스 클릭 컨텍스트 메뉴에서 “게시...” 옵션을 선택하거나 LocalDB에 대한 디버그 배포를 위한 F5를 사용하면 됩니다. 이 예에서는 “게시...” 대화 상자를 사용하여 배포 스크립트를 생성합니다.  
  
##### <a name="to-deploy-your-sql-project-and-generate-a-deployment-report"></a>SQL 프로젝트를 배포하고 배포 보고서를 생성하려면  
  
1.  Visual Studio를 열고 SQL 프로젝트가 포함된 솔루션을 엽니다.  
  
2.  프로젝트를 선택하고 “F5”를 눌러서 디버그 배포를 수행합니다. 참고: ContributorArguments 요소는 구성이 “디버그”인 경우에만 포함되도록 설정되었으므로, 현재는 배포 보고서가 디버그 배포용으로만 생성됩니다. 이를 변경하려면 ContributorArguments 정의에서 Condition="'$(Configuration)' == 'Debug'" 문을 제거합니다.  
  
3.  출력 창에 다음과 같은 출력이 표시됩니다.  
  
    ```  
    ------ Deploy started: Project: Database1, Configuration: Debug Any CPU ------  
    Finished verifying cached model in 00:00:00  
    Deployment reports ->  
  
      C:\Users\UserName\Documents\Visual Studio 2012\Projects\MyDatabaseProject\MyDatabaseProject\sql\debug\MyTargetDatabase.summary.xml  
      C:\Users\UserName\Documents\Visual Studio 2012\Projects\MyDatabaseProject\MyDatabaseProject\sql\debug\MyTargetDatabase.details.xml  
  
      Deployment script generated to:  
      C:\Users\UserName\Documents\Visual Studio 2012\Projects\MyDatabaseProject\MyDatabaseProject\sql\debug\MyDatabaseProject.sql  
  
    ```  
  
4.  MyTargetDatabase.summary.xml을 열고 내용을 확인합니다. 이 파일은 새 데이터베이스 배포를 표시하는 다음 예와 비슷합니다.  
  
    ```  
    <?xml version="1.0" encoding="utf-8" standalone="yes"?>  
    <DeploymentReport>  
      <Operations>  
        <DeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <BeginPreDeploymentScriptStep />  
        <DeploymentScriptStep />  
        <EndPreDeploymentScriptStep />  
        <SqlBeginPreservationStep />  
        <SqlEndPreservationStep />  
        <SqlBeginDropsStep />  
        <SqlEndDropsStep />  
        <SqlBeginAltersStep />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales" Category="Schema" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Customer" Category="Table" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.PK_Customer_CustID" Category="Primary Key" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Orders" Category="Table" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.PK_Orders_OrderID" Category="Primary Key" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Def_Customer_YTDOrders" Category="Default Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Def_Customer_YTDSales" Category="Default Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Def_Orders_OrderDate" Category="Default Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Def_Orders_Status" Category="Default Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.FK_Orders_Customer_CustID" Category="Foreign Key" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.CK_Orders_FilledDate" Category="Check Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.CK_Orders_OrderDate" Category="Check Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspCancelOrder" Category="Procedure" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspFillOrder" Category="Procedure" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspNewCustomer" Category="Procedure" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspPlaceNewOrder" Category="Procedure" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspShowOrderDetails" Category="Procedure" />  
        <SqlEndAltersStep />  
        <DeploymentScriptStep />  
        <BeginPostDeploymentScriptStep />  
        <DeploymentScriptStep />  
        <EndPostDeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
      </Operations>  
    </DeploymentReport>  
  
    ```  
  
    > [!NOTE]  
    > 대상 데이터베이스와 동일한 데이터베이스 프로젝트를 배포할 경우 결과 보고서가 큰 의미가 없습니다. 의미 있는 결과를 얻기 위해서는 데이터베이스에 변경 내용을 배포하거나 새 데이터베이스를 배포하십시오.  
  
5.  MyTargetDatabase.details.xml을 열고 내용을 확인합니다. 세부 정보 파일의 작은 섹션에는 Sales 스키마를 만들고, 테이블 만들기에 대한 메시지를 출력하고, 테이블을 만드는 항목 및 스크립트가 표시됩니다.  
  
    ```  
    <CreateElementStep Name="Sales" Category="Schema"><![CDATA[CREATE SCHEMA [Sales]  
        AUTHORIZATION [dbo];  
  
    ]]></CreateElementStep>  
        <SqlPrintStep><![CDATA[PRINT N'Creating [Sales].[Customer]...';  
  
    ]]></SqlPrintStep>  
        <CreateElementStep Name="Sales.Customer" Category="Table"><![CDATA[CREATE TABLE [Sales].[Customer] (  
        [CustomerID]   INT           IDENTITY (1, 1) NOT NULL,  
        [CustomerName] NVARCHAR (40) NOT NULL,  
        [YTDOrders]    INT           NOT NULL,  
        [YTDSales]     INT           NOT NULL  
    );  
  
    ]]></CreateElementStep>  
  
    ```  
  
    배포 계획이 실행될 때 이를 분석하면 배포에 포함된 모든 정보에 대한 보고를 수행하고 해당 계획의 단계를 기반으로 추가 작업을 수행할 수 있습니다.  
  
## <a name="next-steps"></a>Next Steps  
출력 XML 파일의 처리를 수행하기 위한 추가 도구를 만들 수도 있습니다. 이 예는 [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx)의 한 가지 예일 뿐입니다. 또한 배포 계획을 실행하기 전에 변경할 수 있도록 [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx)를 만들 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[연습: 데이터베이스 프로젝트 빌드를 확장하여 모델 통계 생성](https://msdn.microsoft.com/library/ee461508(v=vs.100).aspx)  
[연습: 데이터베이스 프로젝트 배포를 확장하여 배포 계획 수정](https://msdn.microsoft.com/library/ee461507(v=vs.100).aspx)  
[빌드 및 배포 참가자를 사용하여 데이터베이스 빌드 및 배포 사용자 지정](https://msdn.microsoft.com/library/ee461505(v=vs.100).aspx)  
  
