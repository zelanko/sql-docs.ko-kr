---
title: "호출 ProcessASDatabase | Microsoft Docs"
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
ms.assetid: 66d5d154-88ce-4c2e-b1ef-e2d2f6fb1c44
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 72c96cddc1d505906164aa3d634871ba0ae30072
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="invoke-processasdatabase"></a>Invoke-ProcessASDatabase

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  기본 메타데이터 유형에 따라 특정 **ProcessType** 또는 **RefreshType** 으로 지정된 **Database** 에서 **Process** 연산을 수행합니다.  
  
 다차원 메타데이터를 데이터베이스의 **ProcessType** 에 사용합니다.(여기에는 호환성 수준이 1050, 1100 또는 1103인 테이블 형식 데이터베이스가 포함됩니다.)  
  
 호환성 수준 1200 이상의 테이블 형식 데이터베이스에 **RefreshType** 을(를) 사용합니다.  

>[!NOTE] 
>이 문서는 오래 된 내용 및 예제에 포함 될 수 있습니다. 최신에 대 한 Get-help cmdlet을 사용 합니다.
  
## <a name="syntax"></a>구문  
 `Invoke-ProcessASDatabase [-DatabaseName] <string> [-RefreshType] <RefreshType> {Full | ClearValues | Calculate |     DataOnly | Automatic | Add | Defragment} [-Server <string>] [-Credential <pscredential>] [-WhatIf] [-Confirm]     [<CommonParameters>]`  
  
 `Invoke-ProcessASDatabase [-DatabaseName] <string> [-ProcessType] <ProcessType> {ProcessFull | ProcessAdd |     ProcessUpdate | ProcessIndexes | ProcessData | ProcessDefault | ProcessClear | ProcessStructure |     ProcessClearStructureOnly | ProcessScriptCache | ProcessRecalc | ProcessDefrag} [-Server <string>] [-Credential     <pscredential>] [-WhatIf] [-Confirm]  [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 **Invoke-ProcessASDatabase** cmdlet은 사용자가 지정한 수준으로 데이터베이스를 처리합니다. 예를 들어, 호환성 수준이 1200인 테이블 형식 데이터베이스에 대해 **RefreshType** 을 **Full** 로 설정하여 기존 데이터를 모두 새로운 데이터로 덮어씁니다.  
  
 처리 유형(다차원) 또는 새로 고침 유형(테이블 형식)이 필요하며, 데이터베이스 또는 서버 매개 변수 앞 또는 뒤에 지정할 수 있습니다.  
  
-   다차원의 경우 [처리 옵션 및 설정&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)을 참조하세요.  
  
-   테이블 형식의 경우 [데이터베이스, 테이블 또는 파티션 처리&#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)를 참조하세요.  
  
## <a name="parameters"></a>매개 변수  
  
### <a name="-databasename-string"></a>-DatabaseName \<문자열 >  
 테이블 형식 또는 다차원 데이터베이스가 처리되도록 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|0|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-servermicrosoftanalysissevicesserver"></a>-서버\<Microsoft.AnalysisSevices.Server >  
 컨텍스트에 **SQLAS** 공급자 디렉터리를 사용하지 않는 경우에는 연결한 서버 인스턴스를 선택적으로 지정합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-refreshtype-microsoftanalysisservicesrefreshtype"></a>-RefreshType \<Microsoft.AnalysisServices.RefreshType >  
 테이블 형식 데이터베이스에 대 한 프로세스 유형을 지정합니다.  유효한 값은 Full, ClearValues, Calculate, DataOnly, Automatic, Add, 및 Defragment입니다. 설명 및 지침은 [데이터베이스, 테이블 또는 파티션 처리&#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)를 참조하세요.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|1.|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-processtype-microsoftanalysisservicesprocesstype"></a>-ProcessType \<Microsoft.AnalysisServices.ProcessType >  
 호환성 수준 1050-1103에서 다차원 데이터베이스 또는 테이블 형식 데이터베이스의 처리 유형을 지정합니다. 유효한 값에는 ProcessFull, ProcessAdd, ProcessUpdate, ProcessIndexes, ProcessData, ProcessDefault, ProcessClear, ProcessStructure, ProcessCelarStructureOnly, ProcessScriptCache, 또는 ProcessRecalc가 포함됩니다. 설명 및 지침은 [처리 옵션 및 설정&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)을 참조하세요.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|1.|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-credential"></a>-Credential  
 이 매개 변수를 지정하면 전달된 사용자 이름 및 암호를 사용하여 Analysis Server 인스턴스에 연결합니다. 자격 증명을 지정하지 않으면 스크립트를 실행하는 사용자의 기본 Windows 계정으로 간주됩니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
## <a name="-whatif"></a>-Whatif  
 연산을 실행하기 전에 연산의 영향에 대한 정보를 가져오려면 이 매개 변수를 포함합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
## <a name="-confirm"></a>-Confirm  
 연산을 실행하기 전에 예 또는 아니오 응답으로 연산을 확인하려면 이 매개 변수를 포함합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치||  
|기본값||  
|파이프라인 입력 허용||  
|와일드카드 문자 허용|false|  
  
## <a name="example-1-sqlas-provider"></a>예제 1(SQLAS 공급자)  
 이 예제는 **SQLAS** 공급자를 사용하여 기본 인스턴스에서 데이터베이스 목록으로 컨텍스트를 설정합니다.  데이터베이스 디렉터리의 콘텐츠를 나열하는 경우 모든 데이터베이스가 해당 프로세스 상태 및 읽기/쓰기 모드와 함께 표시됩니다.  
  
 데이터베이스 폴더에서 데이터베이스 이름만 지정하여 **Invoke-ProcessASDatabase** 를 실행할 수 있습니다.  
  
```  
PS > import-module SQLPS -DisableNameChecking  
PS  SQL Server > cd sqlas\ssas-srv-01\default\databases  
PS SQLSERVER:\sqlas\ssas-srv-01\default\databases> dir  
. . . .  
PS SQLSERVER:\sqlas\ssas-srv-01\default\databases> Invoke-ProcessASDatabase "adventureworks"  
  
```  
  
 데이터베이스 유형에 따라 **RefreshType** 또는 **ProcessType**을 지정하라는 메시지가 표시됩니다.  
  
 처리 증명은 return 문에서 영향 개체 Microsoft.AnalysisServices.Tabular.ObjectImpact의 현재 상태입니다.  
  
 개체 상태 정보가 경우에 따라 캐시되기 때문에, 처리가 완료된 후에 디렉터리의 콘텐츠를 나열하면, 데이터베이스 상태에 ‘처리되지 않은’ 원래 설명자가 남아 있습니다. objectimact이 반환되었다면 데이터베이스가 실제 처리된 것이므로, 오해의 소지가 있습니다.  
  
 Management Studio에서 데이터베이스 속성 페이지를 확인하거나, 새 세션을 시작하거나, 데이터베이스 개체에서 처리 상태를 반환하여( [Microsoft.AnalysisServices.ProcessableMajorObject.LastProcessed](https://msdn.microsoft.com/library/microsoft.analysisservices.processablemajorobject.lastprocessed.aspx)를 통해) 프로세스가 완료되었다는 것을 확인할 수 있습니다.  
  
## <a name="example-2"></a>예제 2  
 이 예제는 공급자 없이 cmdlet을 사용하는 동일한 연산을 보여줍니다. 서버 및 처리 유형을 지정하려면 추가적인 매개 변수가 필요합니다.  
  
```  
PS > import-module SQLPS -DisableNameChecking  
PS  SQL Server >  Invoke-ProcessASDatabase -databasename "AdventureWorks" -server '\\server-name\instancename' –ProcessType "ProcessFull"  
  
```  
  
  
  
