---
title: "DirectQuery 모드 | Microsoft Docs"
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.bidtoolset.realtime.f1
ms.assetid: 45ad2965-05ec-4fb1-a164-d8060b562ea5
caps.latest.revision: "64"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 9bd8eb8e3bd0f313fec3e2d0228fb04e08cb6199
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="directquery-mode"></a>DirectQuery 모드

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  이 항목에서는 설명 *DirectQuery 모드* 1200 이상 호환성 수준에서 Analysis Services 테이블 형식 모델에 대 한 합니다. SSDT에서 디자인하는 모델에 대해 DirectQuery 모드를 설정하거나 이미 배포된 테이블 형식 모델에 대해 SSMS에서 DirectQuery 모드로 변경할 수 있습니다. DirectQuery 모드를 선택하기 전에 이점과 제한 사항을 이해하는 것이 중요합니다.
  
##  <a name="bkmk_Benefits"></a> 이점
 기본적으로 테이블 형식 모델은 메모리 내 캐시를 사용하여 데이터를 저장하고 쿼리합니다. 테이블 형식 모델이 메모리에 있는 데이터를 쿼리할 경우 복잡한 쿼리도 아주 빨리 처리할 수 있습니다. 그러나 캐시된 데이터를 사용할 경우 몇 가지 제한 사항이 있습니다. 다시 말해, 큰 데이터 집합은 사용 가능한 메모리를 초과할 수 있으며 데이터 새로 고침 요건을 정기적인 프로세싱 일정으로 수행하는 것이 (불가능하지 않다면) 어려울 수 있습니다.  
  
 DirectQuery는 쿼리 실행을 보다 효율적으로 만드는 RDBMS 기능을 활용하는 동시에 이러한 제한 사항을 극복합니다. DirectQuery를 사용하면:  
  
-   데이터가 최신 데이터이며, 메모리 내 캐시에서 별도의 데이터 복사본을 유지 관리해야 하는 추가적인 관리 오버헤드가 없습니다. 기본 원본 데이터를 변경하면 데이터 모델에 대한 쿼리에 바로 반영될 수 있습니다.  
  
-   데이터 집합이 Analysis Services 서버의 메모리 용량보다 클 수 있습니다.  
  
-   DirectQuery는 메모리 최적화 열 인덱스에서 제공 하는 공급자 측 쿼리 가속 기능 활용을 걸릴 수 있습니다.  
  
-   데이터베이스의 행 수준 보안 기능을 사용하여 백 엔드 데이터베이스에서 보안을 적용할 수 있습니다(또는 DAX를 통해 모델에서 행 수준 보안을 사용할 수 있음).  
  
-   모델에 포함되어 있는 복합 수식에 여러 쿼리가 필요할 수 있는 경우 Analysis Services에서는 최적화를 수행하여 벡 엔드 데이터베이스에 대해 실행된 쿼리의 쿼리 계획 효율성을 극대화할 수 있습니다.  
  
##  <a name="bkmk_prereq"></a>제한 사항
DirectQuery 모드의 테이블 형식 모델에는 몇 가지 제한 사항이 있습니다. 모드를 전환하기 전에 기능이 감소되는 것보다 백 엔드 서버에서 쿼리를 실행하는 이점이 더 큰지를 확인해야 합니다.  
  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 기존 모델의 모드를 변경하면, 모델 디자이너는 DirectQuery 모드와 호환이 되지 않은 모델의 기능을 알려줍니다.  
  
 다음 목록에는 유의해야 하는 주요 기능 제한 사항이 요약되어 있습니다.  
  
|||  
|-|-|  
|**기능 영역**|**제한**|  
|**데이터 원본**|DirectQuery 모델은 SQL Server, Azure SQL Database, Oracle 및 Teradata 유형의 단일 관계형 데이터베이스의 데이터만 사용할 수 있습니다.  버전 및 공급자 정보는 이 문서의 뒷부분에 있는 DirectQuery에 대해 지원되는 데이터 원본을 참조하세요.| 
|**SQL 저장 프로시저**|DirectQuery 모델의 경우 데이터 가져오기 마법사를 사용할 때 SQL 문에서 저장 프로시저를 지정하여 테이블을 정의할 수 없습니다. |   
|**계산 테이블**|계산 테이블은 DirectQuery 모델에서 지원되지 않지만, 계산 열은 지원됩니다. 계산 테이블을 포함하는 테이블 형식 모델을 전환하려고 시도하면 붙여넣은 데이터를 모델에 포함할 수 없다고 말하는 오류가 발생합니다.|  
|**쿼리 제한**|기본 행 제한은 백만개의 행이며, msmdsrv.ini 파일에서 **MaxIntermediateRowSize** 를 지정하여 늘릴 수 있습니다. 자세한 내용은 [DAX 속성](../../analysis-services/server-properties/dax-properties.md) 을 참조하세요.
|**DAX 수식**|DirectQuery 모드에서 테이블 형식 모델을 쿼리하는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 DAX 수식과 측정값 정의를 SQL 문으로 변환합니다. SQL 구문으로 변환할 수 없는 요소를 포함하는 DAX 수식은 모델에서 유효성 검사 오류를 반환합니다.<br /><br /> 이러한 제한 사항은 대개 특정 DAX 함수로 제한됩니다. 측정값에 대해, DAX 수식은 관계형 데이터 저장소에 대한 집합 기반 연산으로 변환됩니다. 즉, 암시적으로 생성되는 모든 측정값이 지원됩니다. <br /><br /> 유효성 검사 오류가 발생할 경우 다른 함수로 대체하여 수식을 다시 작성하거나 데이터 원본의 파생 열을 사용하여 문제를 해결해야 합니다.  테이블 형식 모델에 호환되지 않는 함수를 포함하는 수식이 있을 경우 디자이너에서 DirectQuery 모드로 전환하면 보고됩니다. <br /><br />**참고:**  모델을 DirectQuery 모드로 전환하는 경우 모델의 일부 수식이 유효성 검사를 수행할 수 있지만 캐시와 관계형 데이터 저장소에 대해 실행될 때는 다른 결과를 반환합니다. 캐시에 대한 계산은 Excel 동작을 에뮬레이트하는 기능이 포함된 메모리 내 분석 엔진의 의미 체계를 사용하는 반면 관계형 데이터 원본에 저장된 데이터에 대한 쿼리는 반드시 SQL Server의 의미 체계를 사용하기 때문에 이러한 결과가 발생합니다.<br /><br /> SQL 저장  <br /><br /> 자세한 내용은 [DirectQuery 모드에서의 DAX 수식 호환성](../../analysis-services/tabular-models/dax-formula-compatibility-in-directquery-mode-ssas-2016.md)을 참조하세요.|  
|**수식 일관성**|특정 경우에 동일한 수식에서 관계형 데이터 저장소만 사용하는 DirectQuery 모델과 비교했을 때 캐시된 모델의 경우 다른 결과를 반환할 수 있습니다. 메모리 내 분석 엔진과 SQL Server 간의 의미 체계 차이점 때문에 이러한 차이가 발생합니다.<br /><br /> 모델이 실시간으로 배포될 때 다른 결과를 반환할 수 있는 함수를 포함하는 호환성 문제에 대한 전체 목록은 [DirectQuery 모드에서의 DAX 수식 호환성(SQL Server Analysis Services)](http://msdn.microsoft.com/en-us/981b6a68-434d-4db6-964e-d92f8eb3ee3e)을 참조하세요.|  
|**MDX 제한 사항**|상대적인 개체 이름이 없습니다. 모든 개체 이름은 정규화된 이름이어야 합니다.<br /><br /> 세션 범위 MDX 문(명명된 집합, 계산 멤버, 계산 셀, 보이는 합계, 기본 멤버 등)이 없지만 'WITH' 절과 같은 쿼리 범위 구문을 사용할 수 있습니다.<br /><br /> MDX subselect 절에 있는 다양한 수준의 멤버가 포함된 튜플이 없습니다.<br /><br /> 사용자 정의 계층이 없습니다.<br /><br /> 네이티브 SQL 쿼리가 없습니다.(일반적으로 Analysis Services는 T-SQL 하위 집합을 지원하지만, DirectQuery 모델의 하위 집합은 지원하지 않습니다.)|  

## <a name="data-sources-supported-for-directquery"></a>DirectQuery에 대해 지원되는 데이터 원본
호환성 수준 1200 이상에서 테이블 형식 모델을 DirectQuery는 다음과 같은 데이터 원본 및 공급자와 호환 됩니다.

데이터 원본   |버전  |공급자
---------|---------|---------
Microsoft SQL Server    |  2008 이상      |       OLE DB Provider for SQL Server, SQL Server Native Client OLE DB 공급자, .NET Framework Data Provider for SQL Client  
Microsoft Azure SQL Database    |   모두      |  OLE DB Provider for SQL Server, SQL Server Native Client OLE DB 공급자, .NET Framework Data Provider for SQL Client            
Microsoft Azure SQL Data Warehouse     |   모두     |  .NET Framework Data Provider for SQL Client       
Microsoft SQL APS(분석 플랫폼 시스템)     |   모두      |  OLE DB Provider for SQL Server, SQL Server Native Client OLE DB 공급자, .NET Framework Data Provider for SQL Client       
Oracle 관계형 데이터베이스     |  Oracle 9i 이상       |  Oracle OLE DB 공급자       
Teradata 관계형 데이터베이스    |  Teradata V2R6 이상     | .Net Data Provider for Teradata        

## <a name="connecting-to-a-data-source"></a>데이터 원본에 연결
SSDT에서 DirectQuery 모델을 디자인하는 경우 데이터 원본에 연결하고 모델에 포함할 테이블 및 필드를 선택하는 작업은 메모리 내 모델의 경우와 거의 동일합니다. 

DirectQuery를 설정했지만 아직 데이터 원본에 연결하지 않은 경우 테이블 가져오기 마법사를 사용하여 데이터 원본에 연결하고, 테이블 및 필드를 선택하고, SQL 쿼리를 지정할 수 있습니다. 차이점은 작업을 마쳤을 때 실제로 데이터를 메모리 내 캐시로 가져오지 않는다는 것입니다. 

![DirectQuery 가져오기 성공](../../analysis-services/tabular-models/media/directquery-import-success.png)

테이블 가져오기 마법사를 사용하여 데이터를 가져왔지만 DirectQuery 모드를 아직 설정하지 않은 경우 설정하면 메모리 내 캐시가 지워집니다.

  
## <a name="additional-topics-in-this-section"></a>이 섹션의 추가 항목
[SSDT에서 DirectQuery 모드를 사용하도록 설정](../../analysis-services/tabular-models/enable-directquery-mode-in-ssdt.md)

[SSMS에서 DirectQuery 모드를 사용하도록 설정](../../analysis-services/tabular-models/enable-directquery-mode-in-ssms.md)

[디자인 모드에서 DirectQuery 모델에 샘플 데이터 추가](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md)

[DirectQuery 모델에서 파티션 정의](../../analysis-services/tabular-models/define-partitions-in-directquery-models-ssas-tabular.md)
  
[DirectQuery 모드에서 모델 테스트](../../analysis-services/tabular-models/test-a-model-in-directquery-mode.md)

[DirectQuery 모드에서의 DAX 수식 호환성](../../analysis-services/tabular-models/dax-formula-compatibility-in-directquery-mode-ssas-2016.md)
  
