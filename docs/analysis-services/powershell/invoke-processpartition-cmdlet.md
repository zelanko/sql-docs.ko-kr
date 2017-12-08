---
title: "호출 ProcessPartition cmdlet | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 516fab44-734e-425b-9bd0-b4aee1fd338f
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 552bd130a7182a3993c9e6742e7fcb1d1ecfd50c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="invoke-processpartition-cmdlet"></a>Invoke-ProcessPartition cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  특정 처리 유형 변수를 사용하여 파티션을 처리합니다.  

>[!NOTE] 
>이 문서는 오래 된 내용 및 예제에 포함 될 수 있습니다. 최신에 대 한 Get-help cmdlet을 사용 합니다.
  
## <a name="syntax"></a>구문  
 `Invoke-ProcessPartition [-Name] <System.String> [-Database] <System.String> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [-CubeName] <System.String> [-MeasureGroupName] <System.String> [<CommonParameters>]`  
  
 `Invoke-ProcessPartition –DatabasePartition <Microsoft.AnalysisServices.Partition> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Invoke-ProcessParition cmdlet은 지정된 큐브 및 측정값 그룹에 대해 Analysis Services 데이터베이스의 특정 파티션을 처리합니다. ProcessType 값은 작업의 범위를 결정합니다. 파티션을 처리할 때는 처리 유형을 지정해야 합니다. 자세한 내용은 [처리 옵션 및 설정&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)을 참조하세요.  
  
## <a name="parameters"></a>매개 변수  
  
### <a name="-name-string"></a>-이름 \<문자열 >  
 처리할 파티션을 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|0|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-database-string"></a>-데이터베이스 \<문자열 >  
 큐브가 속한 데이터베이스를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|1.|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-cubename-string"></a>-CubeName \<문자열 >  
 측정값 그룹이 속한 큐브를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|2|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-measuregroupname-string"></a>-MeasureGroupName \<문자열 >  
 파티션이 속한 측정값 그룹을 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|2|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-databasepartition-microsoftanalysisservicespartition"></a>-DatabasePartition \<Microsoft.AnalysisServices.Partition >  
 처리할 파티션을 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|2|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-processtype-microsoftanalysisservicesprocesstype"></a>-ProcessType \<Microsoft.AnalysisServices.ProcessType >  
 ProcessFull, ProcessAdd, ProcessUpdate, ProcessIndexes, ProcessData, ProcessDefault, ProcessClear, ProcessStructure, ProcessCelarStructureOnly, ProcessScriptCache, ProcessRecalc 등 처리 유형을 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="commonparameters"></a>\<일반 매개 변수 >  
 이 cmdlet은 공통 매개 변수 -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer 및 -OutVariable을 지원합니다. 자세한 내용은 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)를 참조하세요.  
  
## <a name="inputs-and-outputs"></a>입/출력  
 입력 유형은 cmdlet에 파이프할 수 있는 개체 유형입니다. 반환 유형은 cmdlet에서 반환하는 개체 유형입니다.  
  
|||  
|-|-|  
|입력|InclusionThresholdSetting|  
|출력|InclusionThresholdSetting|  
  
## <a name="example-1"></a>예제 1  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups\Sales Orders\Partitions\Total_Orders_2004 > Get-Item .| Invoke-ProcessPartition –ProcessType:ProcessDefault`  
  
 이 명령은 처리할 파티션의 ID를 파이프합니다.  
  
## <a name="example-2"></a>예제 2  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups> Invoke-ProcessPartition –Name “Total_Orders_2003” –MeasureGroupname “Sales Order” –CubeName “Adventure Works” –database “AWTEST” –ProcessType “ProcessFull”`  
  
 이 명령은 AWTEST 데이터베이스의 Sales Orders 측정값 그룹에 있는 Total_Orders_2003 파티션을 처리합니다.  
  
  
  
