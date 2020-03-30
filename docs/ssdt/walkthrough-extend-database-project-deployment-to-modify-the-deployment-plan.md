---
title: 데이터베이스 프로젝트 배포를 확장하여 배포 계획 수정
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 22b077b1-fa25-49ff-94f6-6d0d196d870a
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 1f4c73d02d131a0399fd8dde7698592629ef2726
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75242669"
---
# <a name="walkthrough-extend-database-project-deployment-to-modify-the-deployment-plan"></a>연습: 데이터베이스 프로젝트 배포를 확장하여 배포 계획 수정

배포 참가자를 만들어서 SQL 프로젝트를 배포할 때 사용자 지정 작업을 수행할 수 있습니다. 배포 참가자는 [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) 또는 [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx) 중에서 만들 수 있습니다. [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx)를 사용하면 계획을 실행하기 전에 항목을 변경할 수 있고 [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx)를 사용하면 계획을 실행하는 동안 작업을 수행할 수 있습니다. 이 연습에서는 SqlRestartableScriptContributor라는 [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx)를 만듭니다. 이 배포 참가자는 배포 스크립트의 일괄 처리에 IF 문을 추가해서 실행 중 오류가 발생할 경우 완료될 때까지 스크립트를 다시 실행할 수 있게 합니다.  
  
이 연습에서 수행하는 주요 작업은 다음과 같습니다.  
  
-   [DeploymentPlanModifier 유형의 배포 참가자 만들기](#CreateDeploymentContributor)  
  
-   [배포 참가자 설치](#InstallDeploymentContributor)  
  
-   [배포 참가자 실행 또는 테스트](#TestDeploymentContributor)  
  
## <a name="prerequisites"></a>사전 요구 사항  
이 연습을 완료하려면 다음과 같은 구성 요소가 필요합니다.  
  
-   SQL Server Data Tools가 포함되고 C# 또는 VB 개발이 지원되는 Visual Studio 버전이 설치되어 있어야 합니다.  
  
-   SQL 개체가 포함된 SQL 프로젝트가 있어야 합니다.  
  
-   데이터베이스 프로젝트를 배포할 수 있는 SQL Server 인스턴스가 필요합니다.  
  
> [!NOTE]  
> 이 연습은 SQL Server Data Tools의 SQL 기능에 익숙한 사용자를 대상으로 합니다. 또한 코드 클래스를 만드는 방법 및 코드 편집기를 사용해서 클래스에 코드를 추가하는 방법과 같은 기본적인 Visual Studio 개념에 대해서도 익숙해야 합니다.  
  
## <a name="create-a-deployment-contributor"></a><a name="CreateDeploymentContributor"></a>배포 참가자 만들기  
배포 참가자를 만들려면 다음 작업을 수행해야 합니다.  
  
-   클래스 라이브러리 프로젝트를 만들고 필요한 참조를 추가합니다.  
  
-   [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx)에서 상속하는 SqlRestartableScriptContributor라는 클래스를 정의합니다.  
  
-   [OnExecute](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributor.onexecute.aspx) 메서드를 재정의합니다.  
  
-   프라이빗 도우미 메서드를 추가합니다.  
  
-   결과 어셈블리를 빌드합니다.  
  
#### <a name="to-create-a-class-library-project"></a>클래스 라이브러리 프로젝트를 만들려면  
  
1.  MyOtherDeploymentContributor라는 이름의 Visual C# 또는 Visual Basic 클래스 라이브러리 프로젝트를 만듭니다.  
  
2.  "Class1.cs" 파일 이름을 "SqlRestartableScriptContributor.cs"로 바꿉니다.  
  
3.  솔루션 탐색기에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭한 후 **참조 추가**를 클릭합니다.  
  
4.  [프레임워크] 탭에서 **System.ComponentModel.Composition**을 선택합니다.  
  
5.  **찾아보기**를 클릭하고 **C:\Program Files (x86)\Microsoft SQL Server\110\SDK\Assemblies** 디렉터리로 이동하고 **Microsoft.SqlServer.TransactSql.ScriptDom.dll**을 선택한 후 **확인**을 클릭합니다.  
  
6.  필요한 SQL 참조 추가: 프로젝트 노드를 마우스 오른쪽 단추로 클릭한 후 **참조 추가**를 클릭합니다. **찾아보기**를 클릭하고 **C:\Program Files (x86)\Microsoft SQL Server\110\DAC\Bin** 폴더로 이동합니다. **Microsoft.SqlServer.Dac.dll**, **Microsoft.SqlServer.Dac.Extensions.dll** 및 **Microsoft.Data.Tools.Schema.Sql.dll** 항목을 선택하고 **추가**를 클릭한 후 **확인**을 클릭합니다.  
  
그런 후 클래스에 코드 추가를 시작합니다.  
  
#### <a name="to-define-the-sqlrestartablescriptcontributor-class"></a>SqlRestartableScriptContributor 클래스를 정의하려면  
  
1.  코드 편집기에서 다음 **using** 문과 일치하도록 class1.cs 파일을 업데이트합니다.  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.Globalization;  
    using System.Text;  
    using Microsoft.SqlServer.Dac.Deployment;  
    using Microsoft.SqlServer.Dac.Model;  
    using Microsoft.SqlServer.TransactSql.ScriptDom;  
    ```  
  
2.  다음 예제와 일치하도록 클래스 정의를 업데이트합니다.  
  
    ```csharp  
        /// <summary>  
    /// This deployment contributor modifies a deployment plan by adding if statements  
    /// to the existing batches in order to make a deployment script able to be rerun to completion  
    /// if an error is encountered during execution  
    /// </summary>  
    [ExportDeploymentPlanModifier("MyOtherDeploymentContributor.RestartableScriptContributor", "1.0.0.0")]  
    public class SqlRestartableScriptContributor : DeploymentPlanModifier  
    {  
    }  
  
    ```  
  
    이제 [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx)로부터 상속되는 배포 참가자가 정의되었습니다. 빌드 및 배포 프로세스 중에 사용자 지정 참가자가 표준 확장 디렉터리에서 로드됩니다. 배포 계획 수정 참가자는 [ExportDeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.exportdeploymentplanmodifierattribute.aspx) 특성으로 식별됩니다. 이 특성은 참가자를 검색하는 데 필요합니다. 이 특성은 다음과 비슷합니다.  
  
    ```csharp  
    [ExportDeploymentPlanModifier("MyOtherDeploymentContributor.RestartableScriptContributor", "1.0.0.0")]  
  
    ```  
  
3.  다음 멤버 선언을 추가합니다.  
  
    ```vb  
         private const string BatchIdColumnName = "BatchId";  
            private const string DescriptionColumnName = "Description";  
  
            private const string CompletedBatchesVariableName = "CompletedBatches";  
            private const string CompletedBatchesVariable = "$(CompletedBatches)";  
            private const string CompletedBatchesSqlCmd = @":setvar " + CompletedBatchesVariableName + " __completedBatches_{0}_{1}";  
            private const string TotalBatchCountSqlCmd = @":setvar TotalBatchCount {0}";  
            private const string CreateCompletedBatchesTable = @"  
    if OBJECT_ID(N'tempdb.dbo." + CompletedBatchesVariable + @"', N'U') is null  
    begin  
    use tempdb  
    create table [dbo].[$(CompletedBatches)]  
    (  
    BatchId int primary key,  
    Description nvarchar(300)  
    )  
    use [$(DatabaseName)]  
    end  
    ";  
  
    ```  
  
    그런 다음 데이터베이스 프로젝트를 배포할 때 실행할 코드를 추가하도록 OnExecute 메서드를 재정의합니다.  
  
#### <a name="to-override-onexecute"></a>OnExecute를 재정의하려면  
  
1.  SqlRestartableScriptContributor 클래스에 다음 메서드를 추가합니다.  
  
    ```csharp  
    /// <summary>  
    /// You override the OnExecute method to do the real work of the contributor.  
    /// </summary>  
    /// <param name="context"></param>  
    protected override void OnExecute(DeploymentPlanContributorContext context)  
    {  
         // Replace this with the method body  
    }  
  
    ```  
  
    [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributor.onexecute.aspx) 및 [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributor.aspx)의 기본 클래스인 [DeploymentPlanContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) 기본 클래스로부터 [OnExecute](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx) 메서드를 재정의합니다. OnExecute 메서드에는 지정된 모든 인수, 원본 및 대상 데이터베이스 모델, 배포 계획 및 배포 옵션에 대한 액세스를 제공하는 [DeploymentPlanContributorContext](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributorcontext.aspx) 개체가 전달됩니다. 이 예에서는 배포 계획 및 대상 데이터베이스 이름을 가져옵니다.  
  
2.  이제 본문의 처음 부분을 OnExecute 메서드에 추가합니다.  
  
    ```vb  
    // Obtain the first step in the Plan from the provided context  
    DeploymentStep nextStep = context.PlanHandle.Head;  
    int batchId = 0;  
    BeginPreDeploymentScriptStep beforePreDeploy = null;  
  
    // Loop through all steps in the deployment plan  
    while (nextStep != null)  
    {  
        // Increment the step pointer, saving both the current and next steps  
        DeploymentStep currentStep = nextStep;  
        nextStep = currentStep.Next;  
  
        // Add additional step processing here  
    }  
  
    // if we found steps that required processing, set up a temporary table to track the work that you are doing  
    if (beforePreDeploy != null)  
    {  
        // Add additional post-processing here  
    }  
  
    // Cleanup and drop the table   
    DeploymentScriptStep dropStep = new DeploymentScriptStep(DropCompletedBatchesTable);  
    base.AddAfter(context.PlanHandle, context.PlanHandle.Tail, dropStep);  
  
    ```  
  
    이 코드에서는 몇 가지 지역 변수를 정의하고, 배포 계획의 모든 단계 처리를 수행하는 루프를 설정합니다. 루프가 완료된 뒤에는 일부 사후 처리를 수행해야 하며, 계획 실행 중 진행 상황을 추적하기 위해 배포 중에 생성된 임시 테이블을 삭제합니다. 여기서 핵심 유형은 [DeploymentStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentstep.aspx) 및 [DeploymentScriptStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentscriptstep.aspx)입니다. 핵심 메서드는 AddAfter입니다.  
  
3.  이제 추가 단계 처리를 추가해서 "Add additional step processing here" 주석과 바꿉니다.  
  
    ```csharp  
    // Look for steps that mark the pre/post deployment scripts  
    // These steps will always be in the deployment plan even if the  
    // user's project does not have a pre/post deployment script  
    if (currentStep is BeginPreDeploymentScriptStep)  
    {  
        // This step marks the beginning of the predeployment script.  
        // Save the step and move on.  
        beforePreDeploy = (BeginPreDeploymentScriptStep)currentStep;  
        continue;  
    }  
    if (currentStep is BeginPostDeploymentScriptStep)  
    {  
        // This is the step that marks the beginning of the post deployment script.    
        // We do not continue processing after this point.  
        break;  
    }  
    if (currentStep is SqlPrintStep)  
    {  
        // We do not need to put if statements around these  
        continue;  
    }  
  
    // if we have not yet found the beginning of the pre-deployment script steps,   
    // skip to the next step.  
    if (beforePreDeploy == null)  
    {  
        // We only surround the "main" statement block with conditional  
        // statements  
        continue;  
    }  
  
    // Determine if this is a step that we need to surround with a conditional statement  
    DeploymentScriptDomStep domStep = currentStep as DeploymentScriptDomStep;  
    if (domStep == null)  
    {  
        // This step is not a step that we know how to modify,  
        // so skip to the next step.  
        continue;  
    }  
  
    TSqlScript script = domStep.Script as TSqlScript;  
    if (script == null)  
    {  
        // The script dom step does not have a script with batches - skip  
        continue;  
    }  
  
        // Loop through all the batches in the script for this step.  All the statements  
        // in the batch will be enclosed in an if statement that will check the  
        // table to ensure that the batch has not already been executed  
        TSqlObject sqlObject;  
        string stepDescription;  
        GetStepInfo(domStep, out stepDescription, out sqlObject);  
        int batchCount = script.Batches.Count;  
  
    for (int batchIndex = 0; batchIndex < batchCount; batchIndex++)  
    {  
        // Add batch processing here  
    }  
  
    ```  
  
    코드 주석은 해당 처리에 대한 설명을 제공합니다. 간단하게 말해서 이 코드는 다른 것을 건너뛰고 사후 배포 단계의 시작 지점에 도달할 때 실행을 중지하여 사용자가 설정한 단계를 찾아 봅니다. 단계에 조건문으로 둘러싸야 하는 문이 포함된 경우 추가 처리를 수행합니다. 핵심 유형, 메서드 및 속성에는 [BeginPreDeploymentScriptStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.beginpredeploymentscriptstep.aspx), [BeginPostDeploymentScriptStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.beginpostdeploymentscriptstep.aspx), [TSqlObject](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlobject.aspx), [TSqlScript](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.tsqlscript.aspx), Script, [DeploymentScriptDomStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentscriptdomstep.aspx) 및 [SqlPrintStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqlprintstep.aspx)이 포함됩니다.  
  
4.  이제 일괄 처리 코드를 추가하여 "Add batch processing here" 주석과 바꿉니다.  
  
    ```csharp  
        // Create the if statement that will contain the batch's contents  
        IfStatement ifBatchNotExecutedStatement = CreateIfNotExecutedStatement(batchId);  
        BeginEndBlockStatement statementBlock = new BeginEndBlockStatement();  
        ifBatchNotExecutedStatement.ThenStatement = statementBlock;  
        statementBlock.StatementList = new StatementList();  
  
        TSqlBatch batch = script.Batches[batchIndex];  
        int statementCount = batch.Statements.Count;  
  
        // Loop through all statements in the batch, embedding those in an sp_execsql  
        // statement that must be handled this way (schemas, stored procedures,   
        // views, functions, and triggers).  
        for (int statementIndex = 0; statementIndex < statementCount; statementIndex++)  
        {  
            // Add additional statement processing here  
        }  
  
        // Add an insert statement to track that all the statements in this  
        // batch were executed.  Turn on nocount to improve performance by  
        // avoiding row inserted messages from the server  
        string batchDescription = string.Format(CultureInfo.InvariantCulture,  
            "{0} batch {1}", stepDescription, batchIndex);  
  
        PredicateSetStatement noCountOff = new PredicateSetStatement();  
        noCountOff.IsOn = false;  
        noCountOff.Options = SetOptions.NoCount;  
  
        PredicateSetStatement noCountOn = new PredicateSetStatement();  
        noCountOn.IsOn = true;  
        noCountOn.Options = SetOptions.NoCount;   
        InsertStatement batchCompleteInsert = CreateBatchCompleteInsert(batchId, batchDescription);  
        statementBlock.StatementList.Statements.Add(noCountOn);  
    statementBlock.StatementList.Statements.Add(batchCompleteInsert);  
        statementBlock.StatementList.Statements.Add(noCountOff);  
  
        // Remove all the statements from the batch (they are now in the if block) and add the if statement  
        // as the sole statement in the batch  
        batch.Statements.Clear();  
        batch.Statements.Add(ifBatchNotExecutedStatement);  
  
        // Next batch  
        batchId++;  
  
    ```  
  
    이 코드는 BEGIN/END 블록이 포함된 IF 문을 만듭니다. 그런 후 일괄 처리의 문에서 추가 처리를 수행합니다. 처리가 완료되면 스크립트 실행의 진행 상태를 추적하는 정보를 임시 테이블에 추가하기 위해 INSERT 문을 추가합니다. 마지막으로 일괄 처리를 업데이트해서 해당 문을 포함하는 새로운 IF 문으로 이전에 사용된 문을 바꿉니다. 핵심 유형, 메서드 및 속성에는 [IfStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.ifstatement.aspx), [BeginEndBlockStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.beginendblockstatement.aspx), [StatementList](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.statementlist.aspx), [TSqlBatch](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.tsqlbatch.aspx), [PredicateSetStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.predicatesetstatement.aspx), [SetOptions](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.setoptions.aspx) 및 [InsertStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.insertstatement.aspx)가 포함됩니다.  
  
5.  이제 문 처리 루프의 본문을 추가합니다. "Add additional statement processing here" 주석과 바꿉니다.  
  
    ```csharp  
    TSqlStatement smnt = batch.Statements[statementIndex];  
  
    if (IsStatementEscaped(sqlObject))  
    {  
        // "escape" this statement by embedding it in a sp_executesql statement  
        string statementScript;  
        domStep.ScriptGenerator.GenerateScript(smnt, out statementScript);  
        ExecuteStatement spExecuteSql = CreateExecuteSql(statementScript);  
        smnt = spExecuteSql;  
    }  
  
    statementBlock.StatementList.Statements.Add(smnt);  
  
    ```  
  
    일괄 처리의 각 문에 대해 해당 문이 sp_executesql 문으로 래핑되어야 하는 유형인 경우, 그에 맞게 문을 수정합니다. 그런 다음 사용자가 만든 BEGIN/END 블록의 문 목록에 이 문을 추가합니다. 핵심 유형, 메서드 및 속성에는 [TSqlStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.tsqlstatement.aspx) 및 [ExecuteStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.executestatement.aspx)가 포함됩니다.  
  
6.  마지막으로 "Add additional post-processing here" 주석 위치에 사후 처리 섹션을 추가합니다.  
  
    ```csharp  
    // Declare a SqlCmd variables.  
    //  
    // CompletedBatches variable - defines the name of the table in tempdb that will track  
    // all the completed batches.  The temporary table's name has the target database name and  
    // a guid embedded in it so that:  
    // * Multiple deployment scripts targeting different DBs on the same server  
    // * Failed deployments with old tables do not conflict with more recent deployments  
    //  
    // TotalBatchCount variable - the total number of batches surrounded by if statements.  Using this  
    // variable pre/post deployment scripts can also use the CompletedBatches table to make their  
    // script rerunnable if there is an error during execution  
    StringBuilder sqlcmdVars = new StringBuilder();  
    sqlcmdVars.AppendFormat(CultureInfo.InvariantCulture, CompletedBatchesSqlCmd,  
        context.Options.TargetDatabaseName, Guid.NewGuid().ToString("D"));  
    sqlcmdVars.AppendLine();  
    sqlcmdVars.AppendFormat(CultureInfo.InvariantCulture, TotalBatchCountSqlCmd, batchId);  
  
    DeploymentScriptStep completedBatchesSetVarStep = new DeploymentScriptStep(sqlcmdVars.ToString());  
    base.AddBefore(context.PlanHandle, beforePreDeploy, completedBatchesSetVarStep);  
  
    // Create the temporary table we will use to track the work that we are doing  
    DeploymentScriptStep createStatusTableStep = new DeploymentScriptStep(CreateCompletedBatchesTable);  
    base.AddBefore(context.PlanHandle, beforePreDeploy, createStatusTableStep);  
  
    ```  
  
    처리 중에 조건 문으로 둘러싼 하나 이상의 단계가 발견되면, SQLCMD 변수를 정의하는 문을 배포 스크립트에 추가해야 합니다. 첫 번째 변수인 CompletedBatches에는 스크립트가 실행될 때 성공적으로 완료된 일괄 처리를 추적하기 위해 배포 스크립트에서 사용되는 임시 테이블의 고유 이름이 포함됩니다. 두 번째 변수인 TotalBatchCount에는 배포 스크립트에 있는 총 일괄 처리 수가 포함됩니다.  
  
    이외에도 중요한 추가 유형, 속성 및 메서드는 다음과 같습니다.  
  
    StringBuilder, [DeploymentScriptStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentscriptstep.aspx) 및 AddBefore.  
  
    그런 다음 이 메서드로 호출되는 도우미 메서드를 정의합니다.  
  
#### <a name="to-add-the-helper-methods"></a>도우미 메서드를 추가하려면  
  
-   여러 가지 도우미 메서드를 정의해야 합니다. 중요한 메서드는 다음과 같습니다.  
  
    |**메서드**|**설명**|  
    |--------------|-------------------|  
    |CreateExecuteSQL|제공된 문에 EXEC sp_executesql 문을 포함하기 위한 CreateExecuteSQL 메서드를 정의합니다. 핵심 유형, 메서드 및 속성에는 [ExecuteStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.executestatement.aspx), [ExecutableProcedureReference](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.executableprocedurereference.aspx), [SchemaObjectName](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.schemaobjectname.aspx), [ProcedureReference](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.procedurereference.aspx) 및 [ExecuteParameter](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.executeparameter.aspx)가 포함됩니다.|  
    |CreateCompletedBatchesName|CreateCompletedBatchesName 메서드를 정의합니다. 이 메서드는 일괄 처리에 대한 임시 테이블에 삽입할 이름을 만듭니다. 핵심 유형, 메서드 및 속성에는 [SchemaObjectName](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.schemaobjectname.aspx)이 포함됩니다.|  
    |IsStatementEscaped|IsStatementEscaped 메서드를 정의합니다. 이 메서드는 해당 모델 요소 유형에 대해 IF 문 내에 포함하기 전에 해당 문에 EXEC sp_executesql 문을 래핑해야 하는지 여부를 결정합니다. 핵심 유형, 메서드 및 속성에는 TSqlObject.ObjectType, ModelTypeClass 및 모델 유형 Schema, Procedure, View,  TableValuedFunction, ScalarFunction, DatabaseDdlTrigger, DmlTrigger, ServerDdlTrigger의 TypeClass 속성이 포함됩니다.|  
    |CreateBatchCompleteInsert|CreateBatchCompleteInsert 메서드를 정의합니다. 이 메서드는 스크립트 실행의 진행 상태를 추적하기 위해 배포 스크립트에 추가할 INSERT 문을 만듭니다. 핵심 유형, 메서드 및 속성에는 InsertStatement, NamedTableReference, ColumnReferenceExpression, ValuesInsertSource 및 RowValue가 포함됩니다.|  
    |CreateIfNotExecutedStatement|CreateIfNotExecutedStatement 메서드를 정의합니다. 이 메서드는 임시 일괄 처리가 테이블을 실행하는지 여부를 확인하는 IF 문을 생성하여 이 일괄 처리가 이미 실행되었음을 나타냅니다. 핵심 유형, 메서드 및 속성에는 IfStatement, ExistsPredicate, ScalarSubquery, NamedTableReference, WhereClause, ColumnReferenceExpression, IntegerLiteral, BooleanComparisonExpression 및 BooleanNotExpression이 포함됩니다.|  
    |GetStepInfo|GetStepInfo 메서드를 정의합니다. 이 메서드는 단계 이름 외에도 단계의 스크립트를 만드는 데 사용된 모델 요소에 대한 정보를 추출합니다. 중요한 유형 및 메서드에는 [DeploymentPlanContributorContext](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributorcontext.aspx), [DeploymentScriptDomStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentscriptdomstep.aspx), [TSqlObject](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlobject.aspx), [CreateElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.createelementstep.aspx), [AlterElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.alterelementstep.aspx) 및 [DropElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.dropelementstep.aspx)이 포함됩니다.|  
    |GetElementName|TSqlObject에 대한 형식 이름을 만듭니다.|  
  
1.  도우미 메서드를 정의하기 위해 다음 코드를 추가합니다.  
  
    ```csharp  
  
    /// <summary>  
    /// The CreateExecuteSql method "wraps" the provided statement script in an "sp_executesql" statement  
    /// Examples of statements that must be so wrapped include: stored procedures, views, and functions  
    /// </summary>  
    private static ExecuteStatement CreateExecuteSql(string statementScript)  
    {  
        // define a new Exec statement  
        ExecuteStatement executeSp = new ExecuteStatement();  
        ExecutableProcedureReference spExecute = new ExecutableProcedureReference();  
        executeSp.ExecuteSpecification = new ExecuteSpecification { ExecutableEntity = spExecute };  
  
        // define the name of the procedure that you want to execute, in this case sp_executesql  
        SchemaObjectName procName = new SchemaObjectName();  
        procName.Identifiers.Add(CreateIdentifier("sp_executesql", QuoteType.NotQuoted));  
        ProcedureReference procRef = new ProcedureReference { Name = procName };  
  
        spExecute.ProcedureReference = new ProcedureReferenceName { ProcedureReference = procRef };  
  
        // add the script parameter, constructed from the provided statement script  
        ExecuteParameter scriptParam = new ExecuteParameter();  
        spExecute.Parameters.Add(scriptParam);  
        scriptParam.ParameterValue = new StringLiteral { Value = statementScript };  
        scriptParam.Variable = new VariableReference { Name = "@stmt" };  
        return executeSp;  
    }  
  
    /// <summary>  
    /// The CreateIdentifier method returns a Identifier with the specified value and quoting type  
    /// </summary>  
    private static Identifier CreateIdentifier(string value, QuoteType quoteType)  
    {  
        return new Identifier { Value = value, QuoteType = quoteType };  
    }  
  
    /// <summary>  
    /// The CreateCompletedBatchesName method creates the name that will be inserted  
    /// into the temporary table for a batch.  
    /// </summary>  
    private static SchemaObjectName CreateCompletedBatchesName()  
    {  
        SchemaObjectName name = new SchemaObjectName();  
        name.Identifiers.Add(CreateIdentifier("tempdb", QuoteType.SquareBracket));  
        name.Identifiers.Add(CreateIdentifier("dbo", QuoteType.SquareBracket));  
        name.Identifiers.Add(CreateIdentifier(CompletedBatchesVariable, QuoteType.SquareBracket));  
        return name;  
    }  
  
    /// <summary>  
    /// Helper method that determins whether the specified statement needs to  
    /// be escaped  
    /// </summary>  
    /// <param name="sqlObject"></param>  
    /// <returns></returns>  
    private static bool IsStatementEscaped(TSqlObject sqlObject)  
    {  
        HashSet<ModelTypeClass> escapedTypes = new HashSet<ModelTypeClass>  
        {  
            Schema.TypeClass,  
            Procedure.TypeClass,  
            View.TypeClass,  
            TableValuedFunction.TypeClass,  
            ScalarFunction.TypeClass,  
            DatabaseDdlTrigger.TypeClass,  
            DmlTrigger.TypeClass,  
            ServerDdlTrigger.TypeClass  
        };  
        return escapedTypes.Contains(sqlObject.ObjectType);  
    }  
  
    /// <summary>  
    /// Helper method that creates an INSERT statement to track a batch being completed  
    /// </summary>  
    /// <param name="batchId"></param>  
    /// <param name="batchDescription"></param>  
    /// <returns></returns>  
    private static InsertStatement CreateBatchCompleteInsert(int batchId, string batchDescription)  
    {  
        InsertStatement insert = new InsertStatement();  
        NamedTableReference batchesCompleted = new NamedTableReference();  
        insert.InsertSpecification = new InsertSpecification();  
        insert.InsertSpecification.Target = batchesCompleted;  
        batchesCompleted.SchemaObject = CreateCompletedBatchesName();  
  
        // Build the columns inserted into  
        ColumnReferenceExpression batchIdColumn = new ColumnReferenceExpression();  
        batchIdColumn.MultiPartIdentifier = new MultiPartIdentifier();  
        batchIdColumn.MultiPartIdentifier.Identifiers.Add(CreateIdentifier(BatchIdColumnName, QuoteType.NotQuoted));  
  
        ColumnReferenceExpression descriptionColumn = new ColumnReferenceExpression();  
        descriptionColumn.MultiPartIdentifier = new MultiPartIdentifier();  
        descriptionColumn.MultiPartIdentifier.Identifiers.Add(CreateIdentifier(DescriptionColumnName, QuoteType.NotQuoted));  
  
        insert.InsertSpecification.Columns.Add(batchIdColumn);  
        insert.InsertSpecification.Columns.Add(descriptionColumn);  
  
        // Build the values inserted  
        ValuesInsertSource valueSource = new ValuesInsertSource();  
        insert.InsertSpecification.InsertSource = valueSource;  
  
        RowValue values = new RowValue();  
        values.ColumnValues.Add(new IntegerLiteral { Value = batchId.ToString() });  
        values.ColumnValues.Add(new StringLiteral { Value = batchDescription });  
        valueSource.RowValues.Add(values);  
  
        return insert;  
    }  
  
    /// <summary>  
    /// This is a helper method that generates an if statement that checks the batches executed  
    /// table to see if the current batch has been executed.  The if statement will look like this  
    ///   
    /// if not exists(select 1 from [tempdb].[dbo].[$(CompletedBatches)]   
    ///                where BatchId = batchId)  
    /// begin  
    /// end  
    /// </summary>  
    /// <param name="batchId"></param>  
    /// <returns></returns>  
    private static IfStatement CreateIfNotExecutedStatement(int batchId)  
    {  
        // Create the exists/select statement  
        ExistsPredicate existsExp = new ExistsPredicate();  
        ScalarSubquery subQuery = new ScalarSubquery();  
        existsExp.Subquery = subQuery;  
  
        subQuery.QueryExpression = new QuerySpecification  
        {  
            SelectElements =  
            {  
                new SelectScalarExpression  { Expression = new IntegerLiteral { Value ="1" } }  
            },  
            FromClause = new FromClause  
            {  
                TableReferences =  
                    {  
                        new NamedTableReference() { SchemaObject = CreateCompletedBatchesName() }  
                    }  
            },  
            WhereClause = new WhereClause  
            {  
                SearchCondition = new BooleanComparisonExpression  
                {  
                    ComparisonType = BooleanComparisonType.Equals,  
                    FirstExpression = new ColumnReferenceExpression  
                    {  
                        MultiPartIdentifier = new MultiPartIdentifier  
                        {  
                            Identifiers = { CreateIdentifier(BatchIdColumnName, QuoteType.SquareBracket) }  
                        }  
                    },  
                    SecondExpression = new IntegerLiteral { Value = batchId.ToString() }  
                }  
            }  
        };  
  
        // Put together the rest of the statement  
        IfStatement ifNotExists = new IfStatement  
        {  
            Predicate = new BooleanNotExpression  
            {  
                Expression = existsExp  
            }  
        };  
  
        return ifNotExists;  
    }  
  
    /// <summary>  
    /// Helper method that generates a useful description of the step.  
    /// </summary>  
    private static void GetStepInfo(  
        DeploymentScriptDomStep domStep,  
        out string stepDescription,  
        out TSqlObject element)  
    {  
        element = null;  
  
        // figure out what type of step we've got, and retrieve  
        // either the source or target element.  
        if (domStep is CreateElementStep)  
        {  
            element = ((CreateElementStep)domStep).SourceElement;  
        }  
        else if (domStep is AlterElementStep)  
        {  
            element = ((AlterElementStep)domStep).SourceElement;  
        }  
        else if (domStep is DropElementStep)  
        {  
            element = ((DropElementStep)domStep).TargetElement;  
        }  
  
        // construct the step description by concatenating the type and the fully qualified  
        // name of the associated element.  
        string stepTypeName = domStep.GetType().Name;  
        if (element != null)  
        {  
            string elementName = GetElementName(element);  
  
            stepDescription = string.Format(CultureInfo.InvariantCulture, "{0} {1}",  
                stepTypeName, elementName);  
        }  
        else  
        {  
            // if the step has no associated element, just use the step type as the description  
            stepDescription = stepTypeName;  
        }  
    }  
  
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
  
    ```  
  
2.  SqlRestartableScriptContributor.cs에 대한 변경 내용을 저장합니다.  
  
그런 후 클래스 라이브러리를 빌드합니다.  
  
#### <a name="to-sign-and-build-the-assembly"></a>어셈블리를 서명하고 빌드하려면  
  
1.  **프로젝트** 메뉴에서 **MyOtherDeploymentContributor 속성**을 클릭합니다.  
  
2.  **서명** 탭을 클릭합니다.  
  
3.  **어셈블리 서명**을 클릭합니다.  
  
4.  **강력한 이름 키 파일 선택**에서 **<New>** 를 클릭합니다.  
  
5.  **강력한 이름 키 만들기** 대화 상자의 **키 파일 이름**에 **MyRefKey**를 입력합니다.  
  
6.  (선택 사항) 강력한 이름 키 파일에 대한 암호를 지정할 수 있습니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
9. **빌드** 메뉴에서 **솔루션 빌드**를 클릭합니다.  
  
    그런 다음 SQL 프로젝트를 배포할 때 로드되도록 어셈블리를 설치해야 합니다.  
  
## <a name="install-a-deployment-contributor"></a><a name="InstallDeploymentContributor"></a>배포 참가자 설치  
배포 참가자를 설치하려면 어셈블리 및 연관된 .pdb 파일을 Extensions 폴더에 복사해야 합니다.  
  
#### <a name="to-install-the-myotherdeploymentcontributor-assembly"></a>MyOtherDeploymentContributor 어셈블리를 설치하려면  
  
1.  이제 어셈블리 정보를 Extensions 디렉터리에 복사합니다. Visual Studio가 시작되면, %Program Files%\Microsoft SQL Server\110\DAC\Bin\Extensions 및 하위 디렉터리에서 확장을 식별하고 이를 사용할 수 있도록 설정합니다.  
  
2.  출력 디렉터리에서 %Program Files%\Microsoft SQL Server\110\DAC\Bin\Extensions 디렉터리로 **MyOtherDeploymentContributor.dll** 어셈블리를 복사합니다. 기본적으로 컴파일된 .dll 파일의 경로는 YourSolutionPath\YourProjectPath\bin\Debug 또는 YourSolutionPath\YourProjectPath\bin\Release입니다.  
  
## <a name="run-or-test-your-deployment-contributor"></a><a name="TestDeploymentContributor"></a>배포 참가자 실행 또는 테스트  
배포 참가자를 실행 또는 테스트하려면 다음 작업을 수행해야 합니다.  
  
-   빌드하려는 .sqlproj 파일에 속성을 추가합니다.  
  
-   MSBuild를 사용하고 적절한 매개 변수를 제공하여 데이터베이스 프로젝트를 배포합니다.  
  
### <a name="add-properties-to-the-sql-project-sqlproj-file"></a>SQL 프로젝트(.sqlproj) 파일에 속성 추가  
실행하려는 참가자의 ID를 지정하려면 항상 SQL 프로젝트 파일을 업데이트해야 합니다. 이 작업은 다음 두 가지 방법 중 한 가지로 수행할 수 있습니다.  
  
1.  .sqlproj 파일을 수동으로 수정해서 필요한 인수를 추가할 수 있습니다. 참가자가 구성에 필요한 검토 인수를 포함하지 않는 경우 또는 대량의 프로젝트에서 빌드 참가자를 다시 사용하지 않으려는 경우에는 이 작업을 선택해서 수행할 수 있습니다. 이 옵션을 선택할 경우, .sqlproj 파일에서 파일의 첫 번째 가져오기 노드 다음에 다음 문을 추가합니다.  
  
    ```  
    <PropertyGroup>  
      <DeploymentContributors>  
        $(DeploymentContributors); MyOtherDeploymentContributor.RestartableScriptContributor  
      </DeploymentContributors>  
    </PropertyGroup>  
    ```  
  
2.  두 번째 방법은 필요한 참가자 인수가 포함된 대상 파일을 만드는 것입니다. 이 방법은 기본값이 포함되기 때문에 여러 프로젝트에 대해 동일한 참가자를 사용하고, 필요한 참가자 인수가 포함된 경우에 유용합니다. 이 경우에는 MSBuild 확장 경로에 대상 파일을 만듭니다.  
  
    1.  %Program Files%\MSBuild로 이동합니다.  
  
    2.  대상 파일을 저장할 "MyContributors"라는 새 폴더를 만듭니다.  
  
    3.  이 디렉터리 내에 “MyContributors.targets”라는 새 파일을 만들고 다음 텍스트를 추가하여 파일을 저장합니다.  
  
        ```  
        <?xml version="1.0" encoding="utf-8"?>  
  
        <Project xmlns="https://schemas.microsoft.com/developer/msbuild/2003">  
          <PropertyGroup>  
            <DeploymentContributors>$(DeploymentContributors);MyOtherDeploymentContributor.RestartableScriptContributor</DeploymentContributors>  
          </PropertyGroup>  
        </Project>  
  
        ```  
  
    4.  참가자를 실행하려는 프로젝트의 .sqlproj 파일 내에서 \<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.SqlTasks.targets" \/> 노드 뒤에 다음 문을 추가하여 대상 파일을 가져옵니다.  
  
        ```  
        <Import Project="$(MSBuildExtensionsPath)\MyContributors\MyContributors.targets " />  
  
        ```  
  
이러한 방법 중 하나에 따라 작업한 후에는 MSBuild를 사용해서 명령줄 빌드에 대한 매개 변수를 전달할 수 있습니다.  
  
> [!NOTE]  
> 참가자 ID를 지정하려면 항상 "DeploymentContributors" 속성을 업데이트해야 합니다. 이 ID는 기여자 원본 파일의 "ExportDeploymentPlanModifier" 특성에 사용된 것과 동일한 ID입니다. 이 ID가 없으면 프로젝트를 빌드할 때 참가자가 실행되지 않습니다. “ContributorArguments” 속성은 기여자가 실행하기 위해 필요한 인수가 있는 경우에만 업데이트해야 합니다.  
  
## <a name="deploy-the-database-project"></a>데이터베이스 프로젝트 배포  
  
#### <a name="to-deploy-your-sql-project-and-generate-a-deployment-report"></a>SQL 프로젝트를 배포하고 배포 보고서를 생성하려면  
  
-   프로젝트는 Visual Studio 내에서 일반적으로 게시 및 배포할 수 있습니다. 단순히 SQL 프로젝트가 포함된 솔루션을 열고 프로젝트에 대한 오른쪽 마우스 클릭 컨텍스트 메뉴에서 [게시...] 옵션을 선택하거나 LocalDB에 대한 디버그 배포에 대해 F5를 사용하면 됩니다. 이 예에서는 “게시...” 대화 상자를 사용하여 배포 스크립트를 생성합니다.  
  
    1.  Visual Studio를 열고 SQL 프로젝트가 포함된 솔루션을 엽니다.  
  
    2.  솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시...** 옵션을 선택합니다.  
  
    3.  게시할 서버 이름 및 데이터베이스 이름을 설정합니다.  
  
    4.  대화 상자 아래쪽에 있는 옵션 중에서 **스크립트 생성**을 선택합니다. 그러면 배포에 사용할 수 있는 스크립트가 생성됩니다. 이제 이 스크립트를 조사해서 스크립트를 다시 시작할 수 있도록 IF 문이 추가되었는지 확인합니다.  
  
    5.  생성된 배포 스크립트를 조사합니다. "Pre-Deployment Script Template" 섹션 바로 앞에 다음과 비슷한 Transact-SQL 구문이 표시되어야 합니다.  
  
        ```  
        :setvar CompletedBatches __completedBatches_CompareProjectDB_cd1e348a-8f92-44e0-9a96-d25d65900fca  
        :setvar TotalBatchCount 17  
        GO  
  
        if OBJECT_ID(N'tempdb.dbo.$(CompletedBatches)', N'U') is null  
        begin  
        use tempdb  
        create table [dbo].[$(CompletedBatches)]  
        (  
        BatchId int primary key,  
        Description nvarchar(300)  
        )  
        use [$(DatabaseName)]  
        end  
  
        ```  
  
        각 일괄 처리 주위의 배포 스크립트 뒷부분에는 원래 문을 둘러싸는 IF 문이 있습니다. 예를 들어 CREATE SCHEMA 문의 경우 다음과 같이 표시될 수 있습니다.  
  
        ```  
        IF NOT EXISTS (SELECT 1  
                       FROM   [tempdb].[dbo].[$(CompletedBatches)]  
                       WHERE  [BatchId] = 0)  
            BEGIN  
                EXECUTE sp_executesql @stmt = N'CREATE SCHEMA [Sales]  
            AUTHORIZATION [dbo]';  
                SET NOCOUNT ON;  
                INSERT  [tempdb].[dbo].[$(CompletedBatches)] (BatchId, Description)  
                VALUES                                      (0, N'CreateElementStep Sales batch 0');  
                SET NOCOUNT OFF;  
            END  
  
        ```  
  
        CREATE SCHEMA는 IF 문 내에서 EXECUTE sp_executesql 문 내에 포함되어야 하는 문 중 하나입니다. CREATE TABLE과 같은 문에는 EXECUTE sp_executesql 문이 필요하지 않으며 다음 예와 비슷하게 표시됩니다.  
  
        ```  
        IF NOT EXISTS (SELECT 1  
                       FROM   [tempdb].[dbo].[$(CompletedBatches)]  
                       WHERE  [BatchId] = 1)  
            BEGIN  
                CREATE TABLE [Sales].[Customer] (  
                    [CustomerID]   INT           IDENTITY (1, 1) NOT NULL,  
                    [CustomerName] NVARCHAR (40) NOT NULL,  
                    [YTDOrders]    INT           NOT NULL,  
                    [YTDSales]     INT           NOT NULL  
                );  
                SET NOCOUNT ON;  
                INSERT  [tempdb].[dbo].[$(CompletedBatches)] (BatchId, Description)  
                VALUES                                      (1, N'CreateElementStep Sales.Customer batch 0');  
                SET NOCOUNT OFF;  
            END  
  
        ```  
  
        > [!NOTE]  
        > 대상 데이터베이스와 동일한 데이터베이스 프로젝트를 배포할 경우 결과 보고서가 큰 의미가 없습니다. 의미 있는 결과를 얻기 위해서는 데이터베이스에 변경 내용을 배포하거나 새 데이터베이스를 배포하십시오.  
  
## <a name="command-line-deployment-using-generated-dacpac-file"></a>생성된 dacpac 파일을 사용해서 명령줄 배포  
SQL 프로젝트가 빌드된 다음에는 명령줄에서 스키마를 배포하는 데 사용할 수 있는 dacpac 파일이 생성되어, 빌드 시스템과 같은 다른 시스템에서 배포를 수행할 수 있습니다. SqlPackage는 다른 여러 작업 중에서도 dacpac를 배포하거나 배포 스크립트를 생성하는 등 다양한 옵션이 포함된 dacpac 배포를 지원하는 명령줄 유틸리티입니다. 자세한 내용은 [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080(v=VS.103).aspx)를 참조하세요.  
  
> [!NOTE]  
> DeploymentContributors 속성이 정의된 프로젝트로부터 빌드된 dacpac를 성공적으로 배포할 수 있으려면 배포 참가자가 포함된 DLL이 사용 중인 컴퓨터에 설치되어 있어야 합니다. 배포를 성공적으로 완료하기 위해서는 필수로 표시되어 있기 때문입니다.  
>   
> 이러한 요구 사항을 방지하려면 .sqlproj 파일에서 배포 참가자를 제외하십시오. 대신 **AdditionalDeploymentContributors** 매개 변수를 사용해서 SqlPackage를 사용하는 배포 작업 중 실행할 참가자를 지정합니다. 이 방법은 특정 서버에 배포를 수행하는 등 특별한 경우에만 참가자를 사용하려는 경우에 유용합니다.  
  
## <a name="next-steps"></a>다음 단계  
배포 계획을 실행하기 전에 다른 방식으로 배포 계획을 수정해서 결과를 실험해볼 수 있습니다. 이렇게 수정해볼 수 있는 항목은 다음과 같습니다.  
  
-   특정 버전 번호와 연결된 모든 데이터베이스 프로젝트에 대한 확장 속성 추가  
  
-   배포 스크립트에서 추가 진단 인쇄 문 또는 주석의 추가 또는 제거  
  
## <a name="see-also"></a>참고 항목  
[빌드 및 배포 참가자를 사용하여 데이터베이스 빌드 및 배포 사용자 지정](../ssdt/use-deployment-contributors-to-customize-database-build-and-deployment.md)  
[연습: 데이터베이스 프로젝트 빌드를 확장하여 모델 통계 생성](../ssdt/walkthrough-extend-database-project-build-to-generate-model-statistics.md)  
[연습: 데이터베이스 프로젝트 배포를 확장하여 배포 계획 분석](../ssdt/walkthrough-extend-database-project-deployment-to-analyze-the-deployment-plan.md)  
  
