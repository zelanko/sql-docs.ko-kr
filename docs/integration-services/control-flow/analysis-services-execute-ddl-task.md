---
title: Analysis Services DDL 실행 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.asexecuteddltask.f1
- sql13.dts.designer.asexecuteddltask.general.f1
- sql13.dts.designer.asexecuteddltask.ddl.f1
helpviewer_keywords:
- Analysis Services Execute DDL task
- DDL
ms.assetid: 7f25c8c6-b601-41f2-9553-be0a2ee0751a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 760a15ce22421ac1e98c6b14ea661de28bf299a9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904172"
---
# <a name="analysis-services-execute-ddl-task"></a>Analysis Services DDL 실행 태스크

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 실행 태스크는 큐브 및 차원과 같은 다차원 개체와 마이닝 모델을 만들거나 삭제 또는 변경할 수 있는 DDL(데이터 정의 언어) 문을 실행합니다. 예를 들어 DDL 문은 **Adventure Works** 큐브에 파티션을 만들거나 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]에 포함된 예제 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 차원을 삭제할 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 실행 태스크는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 관리자를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 연결합니다. 자세한 내용은 [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md)을 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 분석 개체 처리, 데이터 마이닝 예측 쿼리 실행 등의 비즈니스 인텔리전스 작업을 수행하는 많은 태스크가 있습니다.  
  
 관련 비즈니스 인텔리전스 태스크에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [Analysis Services 처리 태스크](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
-   [데이터 마이닝 쿼리 태스크](../../integration-services/control-flow/data-mining-query-task.md)  
  
## <a name="ddl-statements"></a>DDL 문  
 DDL 문은 ASSL( [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripting Language) 문으로 표현되고 XML for Analysis(XMLA) 명령에 포함됩니다.  
  
-   ASSL은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스와 이 인스턴스에 포함된 데이터베이스 및 데이터베이스 개체를 정의하고 설명하는 데 사용합니다. 자세한 내용은 [Analysis Services Scripting Language&#40;XMLA용 ASSL&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)를 참조하세요.  
  
-   XMLA는 만들기, 변경 또는 처리와 같은 동작 명령을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스로 보내는 데 사용하는 명령 언어입니다. 자세한 내용은 [XMLA&#40;XML for Analysis&#41; 참조](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)를 참조하세요.  
  
 DDL 코드가 별도의 파일에 저장되어 있을 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 실행 태스크는 파일 연결 관리자를 사용하여 해당 파일의 경로를 지정합니다. 자세한 내용은 [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)을 참조하세요.  
  
 DDL 문은 암호와 기타 중요한 정보를 포함할 수 있으므로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 실행 태스크가 하나 이상 포함된 패키지는 패키지 보호 수준 **EncryptAllWithUserKey** 또는 **EncryptAllWithPassword**를 사용해야 합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 패키지](../../integration-services/integration-services-ssis-packages.md)를 참조하세요.  
  
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
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-analysis-services-execute-ddl-task"></a>프로그래밍 방식으로 Analysis Services DDL 실행 태스크 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.ASExecuteDDLTask>  
  
## <a name="analysis-services-execute-ddl-task-editor-general-page"></a>Analysis Services DDL 실행 태스크 편집기(일반 페이지)
  **Analysis Services DDL 실행 태스크 편집기** 대화 상자의 **일반** 페이지를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 실행 태스크를 명명 및 설명할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **이름**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 실행 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **설명**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 실행 태스크에 대한 설명을 입력합니다.  
  
## <a name="analysis-services-execute-ddl-task-editor-ddl-page"></a>Analysis Services DDL 실행 태스크 편집기(DDL 페이지)
  **Analysis Services DDL 실행 태스크 편집기** 대화 상자의 **DDL** 페이지를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 대한 연결을 지정하고 DDL(데이터 정의 언어) 문의 원본에 대한 정보를 제공할 수 있습니다.  
  
### <a name="static-options"></a>정적 옵션  
 **대량 삽입 태스크 편집기**  
 목록에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 관리자를 선택하거나 \<**새 연결...** >을 클릭한 다음 **Analysis Services 연결 관리자 추가** 대화 상자를 사용하여 새 연결을 만듭니다.  
  
 **관련 항목:** [Analysis Services 연결 관리자 추가 대화 상자 UI 참조](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md), [Analysis Services 연결 관리자](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **SourceType**  
 DDL 문의 원본 유형을 지정합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**직접 입력**|원본을 **SourceDirect** 입력란에 저장된 DDL 문으로 설정합니다. 이 값을 선택하면 다음 섹션에 동적 옵션이 표시됩니다.|  
|**파일 연결**|원본을 DDL 문이 포함된 파일로 설정합니다. 이 값을 선택하면 다음 섹션에 동적 옵션이 표시됩니다.|  
|**변수**|원본을 변수로 설정합니다. 이 값을 선택하면 다음 섹션에 동적 옵션이 표시됩니다.|  
  
### <a name="dynamic-options"></a>동적 옵션  
  
#### <a name="sourcetype--direct-input"></a>SourceType = 직접 입력  
 **원본**  
 DDL 문을 입력하거나 줄임표 **(...)** 를 클릭한 다음, **DDL 문** 대화 상자에 명령문을 입력합니다.  
  
#### <a name="sourcetype--file-connection"></a>SourceType = 파일 연결  
 **원본**  
 목록에서 파일 연결을 선택하거나 \<**새 연결...** >을 클릭한 다음 **파일 연결 관리자** 대화 상자를 사용하여 새 연결을 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](../../integration-services/connection-manager/file-connection-manager.md)  
  
#### <a name="sourcetype--variable"></a>SourceType = 변수  
 **원본**  
 목록에서 변수를 선택하거나 \<**새 변수...** >를 클릭한 다음 **변수 추가** 대화 상자를 사용하여 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md)  
  
