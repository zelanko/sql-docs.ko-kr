---
title: Analysis Services DDL 실행 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asexecuteddltask.f1
helpviewer_keywords:
- Analysis Services Execute DDL task
- DDL
ms.assetid: 7f25c8c6-b601-41f2-9553-be0a2ee0751a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a74ab896e974410e8357a22546cb63ed7365a149
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833158"
---
# <a name="analysis-services-execute-ddl-task"></a>Analysis Services DDL 실행 태스크
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 실행 태스크는 큐브 및 차원과 같은 다차원 개체와 마이닝 모델을 만들거나 삭제 또는 변경할 수 있는 DDL(데이터 정의 언어) 문을 실행합니다. 예를 들어 DDL 문은 **Adventure Works** 큐브에 파티션을 만들거나 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]에 포함된 예제 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 차원을 삭제할 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 실행 태스크는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 관리자를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 연결합니다. 자세한 내용은 [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md)을 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 분석 개체 처리, 데이터 마이닝 예측 쿼리 실행 등의 비즈니스 인텔리전스 작업을 수행하는 많은 태스크가 있습니다.  
  
 관련 비즈니스 인텔리전스 태스크에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [Analysis Services 처리 태스크](analysis-services-processing-task.md)  
  
-   [데이터 마이닝 쿼리 태스크](data-mining-query-task.md)  
  
## <a name="ddl-statements"></a>DDL 문  
 DDL 문은 ASSL( [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripting Language) 문으로 표현되고 XML for Analysis(XMLA) 명령에 포함됩니다.  
  
-   ASSL은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스와 이 인스턴스에 포함된 데이터베이스 및 데이터베이스 개체를 정의하고 설명하는 데 사용합니다. 자세한 내용은 [Analysis Services Scripting Language &#40;ASSL&#41; 참조](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)합니다.  
  
-   XMLA는 만들기, 변경 또는 처리와 같은 동작 명령을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스로 보내는 데 사용하는 명령 언어입니다. 자세한 내용은 [XMLA&#40;XML for Analysis&#41; 참조](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference)를 참조하세요.  
  
 DDL 코드가 별도의 파일에 저장되어 있을 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 실행 태스크는 파일 연결 관리자를 사용하여 해당 파일의 경로를 지정합니다. 자세한 내용은 [File Connection Manager](../connection-manager/file-connection-manager.md)를 참조하세요.  
  
 DDL 문은 암호와 기타 중요한 정보를 포함할 수 있으므로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 실행 태스크가 하나 이상 포함된 패키지는 패키지 보호 수준 `EncryptAllWithUserKey` 또는 `EncryptAllWithPassword`를 사용해야 합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 패키지](../integration-services-ssis-packages.md)를 참조하세요.  
  
### <a name="ddl-examples"></a>DDL 예  
 다음 3개의 DDL 문은 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]에 포함된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 스크립팅 개체에 의해 생성되었습니다.  
  
 다음 DDL 문은 **Promotion** 차원을 삭제합니다.  
  
```  
<Delete xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DimensionID>Dim Promotion</DimensionID>  
    </Object>  
</Delete>  
  
```  
  
 다음 DDL 문은 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 큐브를 처리합니다.  
  
```  
<Batch xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
  <Parallel>  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
      <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      </Object>  
      <Type>ProcessFull</Type>  
      <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
    </Process>  
  </Parallel>  
</Batch>  
  
```  
  
 다음 DDL 문은 **Forecasting** 마이닝 모델을 만듭니다.  
  
```  
<Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <MiningStructureID>Forecasting</MiningStructureID>  
    </ParentObject>  
    <ObjectDefinition>  
        <MiningModel xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
            <ID>Forecasting</ID>  
            <Name>Forecasting</Name>  
            <Algorithm>Microsoft_Time_Series</Algorithm>  
            <AlgorithmParameters>  
                <AlgorithmParameter>  
                    <Name>PERIODICITY_HINT</Name>  
                    <Value xsi:type="xsd:string">{12}</Value>  
                </AlgorithmParameter>  
            </AlgorithmParameters>  
            <Columns>  
                <Column>  
                    <ID>Amount</ID>  
                    <Name>Amount</Name>  
                    <SourceColumnID>Amount</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Model Region</ID>  
                    <Name>Model Region</Name>  
                    <SourceColumnID>Model Region</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
                <Column>  
                    <ID>Quantity</ID>  
                    <Name>Quantity</Name>  
                    <SourceColumnID>Quantity</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Time Index</ID>  
                    <Name>Time Index</Name>  
                    <SourceColumnID>Time Index</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
            </Columns>  
            <Collation>Latin1_General_CS_AS_KS</Collation>  
        </MiningModel>  
    </ObjectDefinition>  
</Create>  
  
```  
  
 다음 3개의 DDL 문은 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]에 포함된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 스크립팅 개체에 의해 생성되었습니다.  
  
 다음 DDL 문은 **Promotion** 차원을 삭제합니다.  
  
```  
<Delete xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DimensionID>Dim Promotion</DimensionID>  
    </Object>  
</Delete>  
  
```  
  
 다음 DDL 문은 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 큐브를 처리합니다.  
  
```  
<Batch xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
  <Parallel>  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
      <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      </Object>  
      <Type>ProcessFull</Type>  
      <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
    </Process>  
  </Parallel>  
</Batch>  
  
```  
  
 다음 DDL 문은 **Forecasting** 마이닝 모델을 만듭니다.  
  
```  
<Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <MiningStructureID>Forecasting</MiningStructureID>  
    </ParentObject>  
    <ObjectDefinition>  
        <MiningModel xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
            <ID>Forecasting</ID>  
            <Name>Forecasting</Name>  
            <Algorithm>Microsoft_Time_Series</Algorithm>  
            <AlgorithmParameters>  
                <AlgorithmParameter>  
                    <Name>PERIODICITY_HINT</Name>  
                    <Value xsi:type="xsd:string">{12}</Value>  
                </AlgorithmParameter>  
            </AlgorithmParameters>  
            <Columns>  
                <Column>  
                    <ID>Amount</ID>  
                    <Name>Amount</Name>  
                    <SourceColumnID>Amount</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Model Region</ID>  
                    <Name>Model Region</Name>  
                    <SourceColumnID>Model Region</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
                <Column>  
                    <ID>Quantity</ID>  
                    <Name>Quantity</Name>  
                    <SourceColumnID>Quantity</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Time Index</ID>  
                    <Name>Time Index</Name>  
                    <SourceColumnID>Time Index</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
            </Columns>  
            <Collation>Latin1_General_CS_AS_KS</Collation>  
        </MiningModel>  
    </ObjectDefinition>  
</Create>  
  
```  
  
## <a name="configuration-of-the-analysis-services-execute-ddl-task"></a>Analysis Services DDL 실행 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [Analysis Services DDL 실행 태스크 편집기&#40;일반 페이지&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Analysis Services DDL 실행 태스크 편집기&#40;DDL 페이지&#41;](../analysis-services-execute-ddl-task-editor-ddl-page.md)  
  
-   [식 페이지](../expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-analysis-services-execute-ddl-task"></a>프로그래밍 방식으로 Analysis Services DDL 실행 태스크 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.ASExecuteDDLTask>  
  
  
