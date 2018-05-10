---
title: 개체 처리 (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 58150b6b74fd3a58fb09f44818b724214a64b8b6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="processing-objects-xmla"></a>개체 처리(XMLA)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], 처리 하는 단계는 또는 일련의 단계를 변환 하는 데이터를 비즈니스 분석용 정보로 합니다. 처리 방법은 개체 유형에 따라 달라지지만 처리는 항상 데이터를 정보로 변환하는 과정의 일부입니다.  
  
 프로세스에는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체를 사용할 수 있습니다는 [프로세스](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) 명령입니다. **프로세스** 명령에서 다음과 같은 개체를 처리할 수 있습니다는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스:  
  
-   큐브  
  
-   데이터베이스  
  
-   차원  
  
-   측정값 그룹  
  
-   마이닝 모델  
  
-   마이닝 구조  
  
-   파티션  
  
 개체의 처리를 제어 하는 **프로세스** 명령에 설정 될 수 있는 다양 한 속성이 있습니다. **프로세스** 명령에는 제어 하는 속성: 얼마나 많은 처리량, 개체를 처리할지, 아웃오브 라인 바인딩 사용 여부, 오류를 처리 하는 방법 및 쓰기 저장 테이블 관리 방법이 있습니다.  
  
## <a name="specifying-processing-options"></a>처리 옵션 지정  
 [형식](../../analysis-services/xmla/xml-elements-properties/type-element-xmla.md) 의 속성은 **프로세스** 명령 개체를 처리할 때 사용할 처리 옵션을 지정 합니다. 처리 옵션에 대한 자세한 내용은 [처리 옵션 및 설정&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)을 참조하세요.  
  
 다음 표에서에 대 한 상수는 **형식** 속성 및 각 상수를 사용 하 여 처리할 수 있는 다양 한 개체입니다.  
  
|**형식** 값|적용 가능한 개체|  
|--------------------|------------------------|  
|*ProcessFull*|큐브, 데이터베이스, 차원, 측정값 그룹, 마이닝 모델, 마이닝 구조, 파티션|  
|*ProcessAdd*|차원, 파티션|  
|*ProcessUpdate*|차원|  
|*ProcessIndexes*|차원, 큐브, 측정값 그룹, 파티션|  
|*ProcessData*|차원, 큐브, 측정값 그룹, 파티션|  
|*ProcessDefault*|큐브, 데이터베이스, 차원, 측정값 그룹, 마이닝 모델, 마이닝 구조, 파티션|  
|*ProcessClear*|큐브, 데이터베이스, 차원, 측정값 그룹, 마이닝 모델, 마이닝 구조, 파티션|  
|*ProcessStructure*|큐브, 마이닝 구조|  
|*ProcessClearStructureOnly*|마이닝 구조|  
|*ProcessScriptCache*|Cube|  
  
 처리에 대 한 자세한 내용은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체 참조 [다차원 모델 처리 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)합니다.  
  
## <a name="specifying-objects-to-be-processed"></a>처리할 개체 지정  
 [개체](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) 의 속성은 **프로세스** 명령을 처리할 개체의 개체 식별자를 포함 합니다. 에 지정할 수 하나의 개체만 **프로세스** 명령을 했으나 개체를 처리 하 고 모든 자식 개체도 처리 합니다. 예를 들어 큐브의 측정값 그룹을 처리하면 해당 측정 그룹의 모든 파티션이 처리되고, 데이터베이스를 처리하면 데이터베이스에 포함된 큐브, 차원 및 마이닝 구조 등의 모든 개체가 처리됩니다.  
  
 설정 하는 경우는 **ProcessAffectedObjects** 특성에는 **프로세스** 명령을 true로 지정된 된 개체를 처리 하 여 영향을 받는 개체도 처리 관련 합니다. 예를 들어, 사용 하 여 차원이 증분 업데이트 되는 *ProcessUpdate* 처리 옵션에는 **프로세스** 명령의 멤버로 인해 집계가 무효화 된 되 고 추가 또는 삭제 하 여 처리 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 경우 **ProcessAffectedObjects** 설정 되어 true로 합니다. 이 경우 단일에서 **프로세스** 명령에서 여러 개체를 처리할 수는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 있지만 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 지정 된 단일 개체 이외에 추가로 결정는 **프로세스** 명령 처리 되어야 합니다.  
  
 그러나 여러 개 사용 하 여 동시에 차원, 등 여러 개체를 처리할 수 **프로세스** 명령 내에서 **일괄 처리** 명령입니다. 일괄 처리 작업의 개체의 순차 및 병렬 처리에 대해 보다 세부적인 수준의 제어를 제공는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스를 사용 하 여 보다는 **ProcessAffectedObjects** 특성을 사용 하면에 대 한 처리 방법을 조정할 수 큰 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스. 일괄 처리 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 [일괄 처리 작업 수행 &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md)합니다.  
  
## <a name="specifying-out-of-line-bindings"></a>아웃오브 라인 바인딩 지정  
 경우는 **프로세스** 명령에 들어 있지 않은 한 **일괄 처리** 명령을 있습니다에서 아웃오브 라인 바인딩을 선택적으로 지정할 수는 [바인딩](../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md), [데이터원본](../../analysis-services/xmla/xml-elements-properties/datasource-element-xmla.md), 및 [DataSourceView](../../analysis-services/xmla/xml-elements-properties/datasourceview-element-xmla.md) 의 속성은 **프로세스** 처리할 개체에 대 한 명령을 합니다. 아웃오브 라인 바인딩은 데이터 원본, 데이터 원본 뷰 및 실행 하는 동안에 바인딩이 존재 하는 다른 개체에 대 한 참조는 **프로세스** 명령 및 연결 된 기존 바인딩을 모두 재정의 하는 처리 중인 개체입니다. 아웃오브 라인 바인딩을 지정하지 않으면 처리할 개체에 현재 연결되어 있는 바인딩이 사용됩니다.  
  
 아웃오브 라인 바인딩은 다음과 같은 경우에 사용됩니다.  
  
-   행이 두 번 계산되지 않도록 기존 팩트 테이블에 대한 필터나 대체 팩트 테이블을 지정해야 하는 파티션을 증분 처리하는 경우  
  
-   데이터 흐름 태스크를 사용 하 여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 차원, 마이닝 모델 또는 파티션을 처리 하는 동안 데이터를 제공 하도록 합니다.  
  
 아웃오브 라인 바인딩은 ASSL(Analysis Services Scripting Language)의 일부로 설명됩니다. ASSL의 아웃오브 라인 바인딩에 대 한 자세한 내용은 참조 하십시오. [데이터 원본 및 바인딩 &#40;SSAS 다차원&#41;](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)합니다.  
  
### <a name="incrementally-updating-partitions"></a>파티션 증분 업데이트  
 파티션에 대해 지정된 바인딩은 파티션 내에서 이미 집계된 팩트 테이블 데이터를 참조하기 때문에 이미 처리된 파티션을 증분 업데이트하려면 아웃오브 라인 바인딩이 필요합니다. 사용 하 여 이미 처리 된 파티션을 증분 업데이트 하는 경우는 **프로세스** 명령을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 다음 작업을 수행 합니다.  
  
-   증분 업데이트할 파티션과 동일한 구조의 임시 파티션을 만듭니다.  
  
-   에 지정 된 아웃오브 라인 바인딩을 사용 하 여 임시 파티션을 처리는 **프로세스** 명령입니다.  
  
-   임시 파티션을 선택된 기존 파티션과 병합합니다.  
  
 XML for Analysis (XMLA) 사용 하 여 파티션을 병합 하는 방법에 대 한 자세한 내용은 참조 [병합 파티션을 &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/merging-partitions-xmla.md)합니다.  
  
## <a name="handling-processing-errors"></a>처리 오류 해결  
 [ErrorConfiguration](../../analysis-services/xmla/xml-elements-properties/errorconfiguration-element-xmla.md) 의 속성은 **프로세스** 명령을 사용 하면 개체를 처리 하는 동안 발생 한 오류를 처리 하는 방법을 지정할 수 있습니다. 예를 들어 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 차원을 처리하는 동안 키 특성의 키 열에 중복 값이 있는 경우 특성 키는 고유해야 하므로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 중복 레코드를 삭제합니다. 에 따라는 [KeyDuplicate](../../analysis-services/scripting/properties/keyduplicate-element-assl.md) 속성 **ErrorConfiguration**, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 수 없습니다.  
  
-   오류를 무시하고 차원을 계속 처리합니다.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 중복 키가 있음을 알리는 메시지를 반환하고 처리를 계속합니다.  
  
 유사한 경우가 많이 가지가 **ErrorConfiguration** 하는 동안 옵션을 제공는 **프로세스** 명령입니다.  
  
## <a name="managing-writeback-tables"></a>쓰기 저장(writeback) 테이블 관리  
 경우는 **프로세스** 쓰기 가능 파티션 또는 그러한 파티션에 이미 완전히 처리 되지에 대 한 큐브 또는 측정값 그룹에서 발생 하는 명령, 해당 파티션에 대 한 쓰기 저장 테이블이 이미 존재 하지 않을 수 있습니다. [WritebackTableCreation](../../analysis-services/xmla/xml-elements-properties/writebacktablecreation-element-xmla.md) 의 속성은 **프로세스** 명령은 확인 여부를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 쓰기 저장 테이블을 만들어야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="description"></a>Description  
 다음 예제에서는 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 예제 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 완전히 처리합니다.  
  
### <a name="code"></a>코드  
  
```  
<Process xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
  </Object>  
  <Type>ProcessFull</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
### <a name="description"></a>Description  
 다음 예제에서는 증분 처리는 **Internet_Sales_2004** 파티션에 **인터넷 판매** 의 측정값 그룹은 **Adventure Works DW** 는 에서큐브[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 샘플 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스입니다. **프로세스** 명령을 추가 하는 것 주문에 대 한 집계 2006 년 12 월 31 일 이후의 날짜를 파티션에에서 아웃오브 라인 쿼리 바인딩을 사용 하 여는 **바인딩** 의 속성은 **프로세스**  파티션에 추가할 집계를 생성할 팩트 테이블 행을 검색 하는 명령입니다.  
  
### <a name="code"></a>코드  
  
```  
<Process ProcessAffectedObjects="true" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    <CubeID>Adventure Works DW</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2006</PartitionID>  
  </Object>  
  <Bindings>  
    <Binding>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2006</PartitionID>  
      <Source xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="QueryBinding">  
        <DataSourceID>Adventure Works DW</DataSourceID>  
        <QueryDefinition>  
          SELECT  
            [dbo].[FactInternetSales].[ProductKey],  
            [dbo].[FactInternetSales].[OrderDateKey],  
            [dbo].[FactInternetSales].[DueDateKey],  
            [dbo].[FactInternetSales].[ShipDateKey],   
            [dbo].[FactInternetSales].[CustomerKey],   
            [dbo].[FactInternetSales].[PromotionKey],  
            [dbo].[FactInternetSales].[CurrencyKey],  
            [dbo].[FactInternetSales].[SalesTerritoryKey],  
            [dbo].[FactInternetSales].[SalesOrderNumber],  
            [dbo].[FactInternetSales].[SalesOrderLineNumber],  
            [dbo].[FactInternetSales].[RevisionNumber],  
            [dbo].[FactInternetSales].[OrderQuantity],  
            [dbo].[FactInternetSales].[UnitPrice],  
            [dbo].[FactInternetSales].[ExtendedAmount],  
            [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
            [dbo].[FactInternetSales].[DiscountAmount],  
            [dbo].[FactInternetSales].[ProductStandardCost],  
            [dbo].[FactInternetSales].[TotalProductCost],  
            [dbo].[FactInternetSales].[SalesAmount],  
            [dbo].[FactInternetSales].[TaxAmt],  
            [dbo].[FactInternetSales].[Freight],  
            [dbo].[FactInternetSales].[CarrierTrackingNumber],  
            [dbo].[FactInternetSales].[CustomerPONumber]  
          FROM [dbo].[FactInternetSales]  
          WHERE OrderDateKey > '1280'  
        </QueryDefinition>  
      </Source>  
    </Binding>  
  </Bindings>  
  <Type>ProcessAdd</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
  
