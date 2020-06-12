---
title: 데이터 마이닝 서비스 및 데이터 원본 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b26fd6e3-7d87-4f66-ab47-5303b51b87da
author: minewiskan
ms.author: owend
ms.openlocfilehash: afba038563ec5934a874811c804dd7a4aa9fff1e
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84523099"
---
# <a name="data-mining-services-and-data-sources"></a>데이터 마이닝 서비스 및 데이터 원본
  데이터 마이닝을 사용하려면 SQL Server Analysis Services 인스턴스에 대한 연결이 필요합니다. 큐브의 데이터는 데이터 마이닝에 필요하지 않으며 관계형 원본을 사용하는 것이 권장되지만 데이터 마이닝에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 엔진에서 제공하는 구성 요소를 사용합니다.  
  
 이 항목에서는 데이터 마이닝 모델을 생성, 처리, 배포 또는 쿼리하기 위해 SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 연결할 때 필요한 정보를 제공합니다.  
  
## <a name="data-mining-services"></a>데이터 마이닝 서비스  
 의 서버 구성 요소는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 일반적으로 Windows 서비스로 실행 되는 msmdsrv.exe 응용 프로그램입니다. 이 애플리케이션은 보안 구성 요소, XMLA(XML for Analysis) 수신기 구성 요소, 쿼리 프로세서 구성 요소 및 다음 기능을 수행하는 다른 많은 내부 구성 요소로 이루어집니다.  
  
-   클라이언트로부터 수신한 문 구문 분석  
  
-   메타데이터 관리  
  
-   트랜잭션 처리  
  
-   계산 처리  
  
-   차원 및 셀 데이터 저장  
  
-   집계 생성  
  
-   쿼리 일정 예약  
  
-   개체 캐싱  
  
-   서버 리소스 관리  
  
### <a name="xmla-listener"></a>XMLA 수신기  
 XMLA 수신기 구성 요소는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 와 클라이언트 간의 모든 XMLA 통신을 처리합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] `Port` msmdsrv.ini 파일의 구성 설정을 사용 하 여 인스턴스가 수신 하는 포트를 지정할 수 있습니다 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . 이 파일의 값이 0이면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 기본 포트에서 수신합니다. 달리 지정하지 않는 한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 다음 기본 TCP 포트를 사용합니다.  
  
|포트|Description|  
|----------|-----------------|  
|2383|의 기본 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|  
|2382|의 다른 인스턴스에 대 한 리디렉터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|  
|서버 시작 시 동적으로 할당됩니다.|의 명명 된 인스턴스입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
  
 이 서비스에서 사용된 포트를 제어하는 방법은 [Analysis Services 액세스를 허용하도록 Windows 방화벽 구성](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)을 참조하세요.  
  
## <a name="connecting-to-data-sources"></a>데이터 원본에 연결  
 데이터 마이닝 구조 또는 모델을 만들거나 업데이트할 때마다 데이터 원본에 의해 정의된 데이터를 사용하게 됩니다. 데이터 원본은 Excel 통합 문서, 텍스트 파일, SQL Server 데이터베이스 등의 데이터를 포함하지 않으며 연결 정보만 정의합니다.  DSV(데이터 원본 뷰)는 해당 원본 위의 추상화 계층 역할을 하며 원본에서 가져온 데이터를 수정하거나 매핑합니다.  
  
 이러한 각 원본의 연결 요구 사항에 대한 설명은 이 항목에서 다루지 않습니다. 자세한 내용은 공급자에 대한 설명서를 참조하십시오. 그러나 일반적으로 공급자와 상호 작용할 때 Analysis Services에 대한 다음 요구 사항을 알아야 합니다.  
  
-   데이터 마이닝은 서버에서 제공하는 서비스이므로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 데이터 원본에 대한 액세스 권한이 있어야 합니다.  위치 및 ID 두 측면에 액세스합니다.  
  
     **위치** 는 사용자 컴퓨터에만 저장된 데이터를 사용하여 모델을 작성한 후 서버에 배포할 경우 데이터 원본을 찾을 수 없으므로 모델을 처리하지 못함을 의미합니다. 이 문제를 해결하려면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 실행되는 동일한 SQL Server 인스턴스로 데이터를 전송하거나 파일을 공유 위치로 이동해야 할 수 있습니다.  
  
     **ID** 는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 서비스가 적절한 자격 증명으로 데이터 파일 또는 데이터 원본을 열 수 있어야 함을 의미합니다. 예를 들어 모델을 작성할 때 작성자 본인에게는 데이터를 볼 수 있는 무제한적인 권한이 있는 반면, 서버에서 모델을 처리하고 업데이트하는 사용자에게는 데이터에 대한 액세스 권한이 없거나 제한적인 경우에는 모델을 처리하지 못하거나 모델의 콘텐츠가 영향을 받을 수 있습니다. 원격 데이터 원본에 연결하는 데 사용되는 계정에는 최소한 데이터에 대한 읽기 권한이 있어야 합니다.  
  
-   모델을 이동할 때도 동일한 요구 사항이 적용됩니다. 즉, 이전 데이터 원본의 위치에 액세스하거나 데이터 원본을 복사하거나 새 데이터 원본을 구성할 수 있는 적절한 액세스 권한을 설정해야 합니다. 또한 로그인 및 역할을 전송하거나 새 위치에서 데이터 마이닝 개체를 처리하고 업데이트할 수 있는 권한을 설정해야 합니다.  
  
## <a name="configuring-permissions-and-server-properties"></a>사용 권한 및 서버 속성 구성  
 데이터 마이닝에는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 대한 추가 권한이 필요합니다. 대부분의 데이터 마이닝 속성은 [Analysis Server 속성 대화 상자&#40;Analysis Services&#41;](../analysis-server-properties-dialog-box-analysis-services.md)를 사용하여 설정할 수 있습니다.  
  
 구성할 수 있는 속성에 대 한 자세한 내용은 [Analysis Services에서 서버 속성 구성](../server-properties/server-properties-in-analysis-services.md)을 참조 하세요.  
  
 다음 서버 속성은 데이터 마이닝과 특별히 관련된 속성입니다.  
  
-   `AllowAdHocOpenRowsetQueries`서버 메모리 공간에 직접 로드 되는 OLE DB 공급자에 대 한 임시 액세스를 제어 합니다.  
  
    > [!IMPORTANT]  
    >  보안을 강화하려면 이 속성을 `false`로 설정하는 것이 좋습니다. 기본값은 `false`입니다. 단, 이 속성이 `false`로 설정되는 경우에도 사용자는 계속 단일 쿼리를 만들고 허용된 데이터 원본에 대해 OPENQUERY를 사용할 수 있습니다.  
  
-   **AllowedProvidersInOpenRowset** 임시 액세스가 설정된 경우 공급자를 지정합니다. 쉼표로 구분된 ProgID 목록을 입력하여 여러 공급자를 지정할 수 있습니다.  
  
-   **MaxConcurrentPredictionQueries** 예측에 의해 발생하는 서버의 부하를 제어합니다. 기본값인 0은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise에 대해 무제한, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard에 대해 최대 5개의 동시 쿼리를 허용합니다. 제한 값 이후의 쿼리는 직렬화되어 제한 시간을 초과하게 됩니다.  
  
 서버는 모든 데이터 마이닝 서비스에 대한 기본값, 그리고 알고리즘에 대한 제한 사항을 포함하여 사용할 수 있는 데이터 마이닝 알고리즘을 제어하는 추가 속성을 제공합니다. 단, 데이터 마이닝 저장 프로시저에 대한 액세스를 특정적으로 제어하도록 허용하는 설정은 없습니다. 자세한 내용은 [Data Mining Properties](../server-properties/data-mining-properties.md)을 참조하세요.  
  
 서버를 튜닝하고 클라이언트 사용에 대한 보안을 제어하는 속성도 설정할 수 있습니다. 자세한 내용은 [Feature Properties](../server-properties/feature-properties.md)을 참조하세요.  
  
> [!NOTE]  
>  버전의 플러그 인 알고리즘 지원에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [SQL Server 2012 버전에서 지 원하는 기능](https://go.microsoft.com/fwlink/?linkid=232473) 을 참조 하세요 https://go.microsoft.com/fwlink/?linkid=232473) .  
  
## <a name="programmatic-access-to-data-mining-objects"></a>데이터 마이닝 개체에 대한 프로그래밍 방식 액세스  
 다음 개체 모델을 사용하여 Analysis Services 데이터베이스에 대한 연결을 만들고 데이터 마이닝 개체 작업을 수행할 수 있습니다.  
  
 **ADO** OLE DB를 사용하여 Analysis Services 서버에 연결합니다. ADO를 사용하는 경우 클라이언트는 스키마 행 집합 쿼리와 DMX 문으로 제한됩니다.  
  
 **ADO.NET** 다른 공급자보다 SQL Server 공급자와 더 원활하게 상호 작용합니다. 데이터 어댑터를 사용하여 동적 행 집합을 저장합니다. 업데이트하거나 XML로 저장할 수 있는 데이터 테이블로 저장된 서버 데이터의 캐시인 데이터 세트 개체를 사용합니다.  
  
 **ADOMD.NET** 데이터 마이닝 및 OLAP과의 작업에 최적화된 관리 데이터 공급자입니다. ADOMD.NET은 ADO.NET보다 더 빠르고 메모리 효율적입니다. ADOMD.NET을 사용하면 서버 개체에 대한 메타데이터를 검색할 수도 있습니다. .NET을 사용할 수 없는 경우를 제외하고 클라이언트 애플리케이션에 권장되는 개체 모델입니다.  
  
 **서버 ADOMD** 서버에서 직접 Analysis Services 개체에 액세스하기 위한 개체 모델입니다. Analysis Services 저장 프로시저에서 사용되며 클라이언트용이 아닙니다.  
  
 **AMO** DSO(의사 결정 지원 개체)를 대체하는 Analysis Services용 관리 인터페이스입니다. AMO를 사용할 때는 개체 반복과 같은 작업에서 다른 인터페이스에 비해 더 높은 사용 권한이 필요합니다. 이는 ADOMD.NET 및 기타 인터페이스가 데이터베이스 스키마에만 액세스하는 반면 AMO는 메타데이터에 직접 액세스하기 때문입니다.  
  
### <a name="browse-and-query-access-to-servers"></a>서버에 대한 액세스 찾아보기 및 쿼리  
 OLAP/데이터 마이닝 모드에서 Analysis Services 인스턴스를 사용하여 모든 종류의 예측을 수행할 수 있습니다. 단, 다음과 같은 제한 사항이 있습니다.  
  
-   서버 ADOMD를 사용하는 경우 DMX를 사용하면 연결 없이 서버에 액세스할 수 있습니다. 그런 다음 결과를 데이터 테이블에 바로 복사해 넣을 수 있습니다. 그러나 원격 인스턴스에서는 서버 ADOMD를 사용할 수 없습니다. 로컬 서버만 쿼리할 수 있습니다.  
  
-   ADO.NET은 데이터 마이닝에 대해 명명된 매개 변수를 지원하지 않습니다. ADOMD.NET을 사용해야 합니다.  
  
-   ADOMD.NET을 사용하면 매개 변수로 사용할 전체 테이블을 전달할 수 있으므로 클라이언트의 데이터 또는 서버에서 사용할 수 없는 데이터를 사용할 수 있습니다. 모양이 지정된 테이블을 예측 입력으로 사용할 수도 있습니다.  
  
### <a name="using-data-mining-stored-procedures"></a>데이터 마이닝 저장 프로시저 사용  
 일반적으로 저장 프로시저는 재사용을 위해 쿼리를 캡슐화하는 데 사용됩니다. 클라이언트는 CALL을 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 시스템 저장 프로시저를 비롯한 저장 프로시저를 실행할 수 있습니다.  
  
 프로시저가 데이터 세트를 반환하면 클라이언트는 데이터 세트 또는 행이 포함된 중첩된 테이블이 있는 데이터 테이블을 받게 됩니다. 예를 들어 모델에 대한 쿼리를 만들 경우 쿼리는 전체 모델을 반환합니다. 너무 많은 행을 가져오지 않도록 하려면 ADOMD+ 개체 모델을 사용하여 저장 프로시저를 작성하면 됩니다.  
  
 서버 저장 프로시저를 작성하려면 Microsoft.AnalysisServices.AdomdServer 네임스페이스를 참조해야 합니다. 저장 프로시저를 만들고 사용하는 방법은 [User Defined Functions and Stored Procedures](https://docs.microsoft.com/analysis-services/adomd/multidimensional-models-adomd-net-server/user-defined-functions-and-stored-procedures)를 참조하십시오.  
  
> [!NOTE]  
>  저장 프로시저는 데이터 서버 개체의 보안을 변경하는 데 사용할 수 없습니다. 저장 프로시저를 실행하면 모든 서버 개체에 대한 액세스를 확인하기 위해 사용자의 현재 컨텍스트가 사용됩니다. 따라서 사용자에게는 액세스하는 데이터베이스 개체에 대해 적절한 사용 권한이 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [실제 아키텍처 &#40;Analysis Services 다차원 데이터&#41;](../multidimensional-models/olap-physical/understanding-microsoft-olap-physical-architecture.md)   
 [물리적 아키텍처 &#40;Analysis Services 데이터 마이닝&#41;](physical-architecture-analysis-services-data-mining.md)   
 [데이터 마이닝 솔루션 및 개체 관리](management-of-data-mining-solutions-and-objects.md)  
  
  
