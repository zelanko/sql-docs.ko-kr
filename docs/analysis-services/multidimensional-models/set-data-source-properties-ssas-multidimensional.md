---
title: "데이터 원본 속성 (SSAS 다차원) 설정 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.sqlserverstudio.datasourceproperties.f1
helpviewer_keywords:
- Data Source Properties dialog box
ms.assetid: bf8b600f-5b99-4f7d-908b-8a391721e9dd
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d406f4743c47ded117bf93a62bb4eefadb093058
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="set-data-source-properties-ssas-multidimensional"></a>데이터 원본 속성 설정(SSAS 다차원)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 데이터 원본 개체는 외부 데이터 웨어하우스 또는 다차원 모델에 데이터를 제공하는 관계형 데이터베이스에 대한 연결을 지정합니다. 데이터 원본의 속성에 따라 연결 문자열, 제한 시간 간격, 최대 연결 수 및 트랜잭션 격리 수준이 결정됩니다.  
  
## <a name="set-data-source-properties-in-sql-server-data-tools"></a>SQL Server Data Tools에서 데이터 원본 속성 설정  
  
1.  솔루션 탐색기에서 데이터 원본을 두 번 클릭하여 데이터 원본 디자이너를 엽니다.  
  
2.  데이터 원본 디자이너에서 **가장 정보** 탭을 클릭합니다. 데이터 원본 만들기에 대한 자세한 내용은 [데이터 원본 만들기&#40;SSAS 다차원&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)를 참조하세요.  
  
## <a name="set-data-source-properties-in-management-studio"></a>Management Studio에서 데이터 원본 속성 설정  
  
1.  데이터베이스 폴더를 확장하고, 데이터베이스 이름 아래의 **데이터 원본** 폴더를 열고, **개체 탐색기** 에서 데이터 원본을 마우스 오른쪽 단추로 클릭한 후 **속성**을 선택합니다.  
  
2.  선택적으로 이름, 설명 또는 가장 옵션을 수정합니다. 자세한 내용은 [가장 옵션 설정&#40;SSAS - 다차원&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md)을 참조하세요.  
  
## <a name="data-source-properties"></a>데이터 원본 속성  
  
|용어|정의|  
|----------|----------------|  
|**이름, ID, 설명**|이름, ID 및 설명은 다차원 모델에서 데이터 원본 개체를 식별하고 설명하는 데 사용됩니다.<br /><br /> 이름 및 설명은 솔루션을 배포하거나 처리한 후 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 또는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서 지정할 수 있습니다.<br /><br /> 개체를 만들 때 ID가 생성됩니다. 이름과 설명을 쉽게 수정할 수 있지만 ID는 읽기 전용이며 변경해서는 안 됩니다. 정해진 개체 ID는 모델 전체에서 개체 종속성 및 참조를 유지합니다.|  
|**생성된 타임스탬프**|이 읽기 전용 속성은 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에 표시됩니다. 데이터 원본을 만든 날짜 및 시간을 표시합니다.|  
|**최종 스키마 업데이트**|이 읽기 전용 속성은 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에 표시됩니다. 데이터 원본에 대한 메타데이터가 마지막으로 업데이트된 날짜 및 시간을 표시합니다. 이 값은 솔루션을 배포할 때 업데이트됩니다.|  
|**쿼리 제한 시간**|연결 요청이 중단되기 전에 시도하는 시간을 지정합니다.<br /><br /> 다음 형식으로 쿼리 제한 시간을 입력합니다.<br /><br /> *\<시간 >*:*\<분 >*:*\<시간 (초) >*<br /><br /> 이 속성은 **DatabaseConnectionPoolTimeoutConnection** 서버 속성에서 수정할 수 있습니다. 서버 속성이 더 작으면 **쿼리 제한 시간**대신 사용됩니다.<br /><br /> 에 대 한 자세한 내용은 **쿼리 제한 시간** 속성 참조 <xref:Microsoft.AnalysisServices.DataSource.Timeout%2A>합니다. 서버 속성에 대한 자세한 내용은 [OLAP Properties](../../analysis-services/server-properties/olap-properties.md)을 참조하십시오.|  
|**연결 문자열**|다차원 모델에 데이터를 제공하는 데이터베이스의 물리적 위치와 연결에 사용되는 데이터 공급자를 지정합니다. 이 정보는 연결 요청을 수행하는 클라이언트 라이브러리에 제공됩니다. 공급자에 따라 연결 문자열에서 설정할 수 있는 속성이 결정됩니다.<br /><br /> 연결 문자열은 **연결 관리자** 대화 상자에 제공한 정보를 사용하여 만들어집니다. 데이터 원본 속성 페이지에서도 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 의 연결 문자열을 보고 편집할 수 있습니다.<br /><br /> SQL Server 데이터베이스의 경우 **user ID** 를 포함하는 연결 문자열은 데이터베이스 인증을 나타내고 **Integrated Security=SSPI** 를 포함하는 연결은 Windows 인증을 나타냅니다.<br /><br /> 데이터베이스를 새로운 위치로 이동했으면 서버 또는 데이터베이스 이름을 변경할 수 있습니다. 현재 연결에 지정된 자격 증명이 데이터베이스 로그인에 매핑되어 있는지 확인하십시오.|  
|**최대 연결 수**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 데이터 원본에 연결하는 데 허용되는 최대 연결 수를 지정합니다. 추가로 연결해야 하는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 연결을 사용할 수 있을 때까지 대기합니다. 기본값은 10입니다. 연결 수를 제한하면 외부 데이터 원본이 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 요청으로 오버로드되지 않습니다.|  
|**격리성**|관계형 데이터베이스에 연결하여 실행되는 SQL 문의 잠금 및 행 버전 관리 기능을 지정합니다. 유효한 값은 ReadCommitted 또는 Snapshot입니다. 기본값은 ReadCommitted이며, 데이터를 읽기 전에 먼저 커밋하도록 지정합니다. 이렇게 하면 더티 읽기가 방지됩니다. 스냅숏은 이전에 커밋된 데이터의 스냅숏에서 읽기가 수행됨을 지정합니다. SQL Server의 격리 수준에 대한 자세한 내용은 [SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)을 참조하세요.|  
|**관리 공급자**|데이터 원본에서 관리 공급자를 사용하는 경우 System.Data.SqlClient 또는 System.Data.OracleClient와 같은 관리 공급자의 이름을 표시합니다.<br /><br /> 데이터 원본에서 관리 공급자를 사용하지 않는 경우 이 속성은 빈 문자열을 표시합니다.<br /><br /> 이 속성은 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 읽기 전용입니다. 연결에 사용되는 공급자를 변경하려면 연결 문자열을 편집합니다.|  
|**가장 정보**|Windows 인증을 사용하는 데이터 원본에 연결할 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 실행하는 Windows ID를 지정합니다. 옵션에는 미리 정의된 Windows 자격 증명의 집합, 서비스 계정, 현재 사용자의 ID를 사용하는 방법 또는 모델에 여러 데이터 원본 개체가 포함되어 있는 경우에 유용할 수 있는 상속 옵션이 포함됩니다. 자세한 내용은 [가장 옵션 설정&#40;SSAS - 다차원&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md)을 참조하세요.<br /><br /> [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 유효한 값 목록에는 다음 값이 포함됩니다.<br /><br /> **ImpersonateAccount** (특정 Windows 사용자 이름 및 암호를 사용하여 데이터 원본에 연결)<br /><br /> **ImpersonateServiceAccount** (서비스 계정의 보안 ID를 사용하여 데이터 원본). 이 값은 기본값입니다.<br /><br /> **ImpersonateCurrentUser** (현재 사용자의 보안 ID를 사용하여 데이터 원본에 연결). 이 옵션은 외부 데이터 웨어하우스 또는 데이터베이스에서 데이터를 검색하는 데이터 마이닝 쿼리에만 유효합니다. 다차원 데이터베이스에서 처리, 로드 또는 쓰기 저장에 사용되는 데이터 연결에는 이 옵션을 선택하지 마십시오.<br /><br /> **상속** 또는 **기본값** (이 데이터 원본 개체가 포함된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스의 가장 설정 사용). 데이터베이스 속성에는 가장 옵션이 포함되어 있습니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 모델의 데이터 원본](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [데이터 원본 만들기&#40;SSAS 다차원&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  
  
