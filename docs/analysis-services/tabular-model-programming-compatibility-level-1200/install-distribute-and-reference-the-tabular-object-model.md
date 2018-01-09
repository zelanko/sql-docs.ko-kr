---
title: "설치 및 배포 하 고 테이블 형식 개체 모델 참조 | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e51769f7-aac7-4835-a5ae-91aac04aa476
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4992c9a621964f8125178f114a930b1f4e007179
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="install-distribute-and-reference-the-tabular-object-model"></a>설치 및 배포 하 고 테이블 형식 개체 모델 참조
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]이 문서를 다운로드, 참조 및 Analysis Services 테이블 형식 개체 모델 (TOM) 만들기 및 관리 코드에서 데이터베이스 및 테이블 형식 모델 관리에 대 한 C# 라이브러리를 재배포 하는 방법을 설명 합니다.  
  
TOM에 SQL Server 2016와 함께 제공 되는 AMO 클라이언트 라이브러리 (Microsoft.AnalysisServices.dll)의 확장입니다. SQL Server 2016 버전에서 테이블 형식 메타 데이터 엔진을 대상으로 하는 테이블 형식 모델과 함께 작동 합니다. TOM를 사용 하려면 해당 모델과 데이터베이스는 호환성 수준 1200 이상 이어야 합니다.  

## <a name="amo-tom-assemblies"></a>AMO TOM 어셈블리

SQL Server 2016 리팩터링와 AMO Core, 테이블 형식 및 JSON에 대 한 새 어셈블리를 포함 하도록 확장 됩니다. 원래 AMO 어셈블리의 첫 번째 릴리스 이후 Analysis Services의 일부 였던 Microsoft.AnalysisServices.dll 포함 됩니다. 재구성된 AMO 하나의 어셈블리에 대 한 일반 클래스를 오프 로드 하 고 추가 어셈블리를 통해 테이블 형식 및 다차원 Api 간의 논리적인 분할 부분을 제공 합니다. 

다음 표에서 각 어셈블리에 설명 합니다.
  
어셈블리  |기능  |중요 한 클래스 |
---------|---------|--------------  |
핵심 <br/>Microsoft.AnalysisServices.Core.dll | 테이블 형식 및 다차원 데이터베이스를 모두에 공통 됩니다. <br/><br/>예외 처리, Analysis Services 인스턴스 및 데이터베이스에 대 한 일반 연결 및 서버 및 데이터베이스 개체에 대 한 공용 메서드와 속성에 대 한 액세스를 제공 합니다. <br/><br/>SQL Server 2016을 대상으로 하는 모든 AMO 솔루션에 대 한 필요 합니다. | 코어&nbsp;서버<br/>코어&nbsp;데이터베이스<br/>AmoException
TOM<br/> Microsoft.AnalysisServices.Tabular.dll, 13.0.1601.5 버전 이상.| 페이지를 만들고 테이블 형식 메타 데이터 개체를 관리 합니다. | TOM&nbsp;서버 <br/>TOM&nbsp;데이터베이스<br /> Model<br /> Table<br /> Column<br /> 관계
  AMO<br /> Microsoft.AnalysisServices.dll| 만들고, 테이블 형식 1050-1103 데이터베이스를 포함 한 다차원 메타 데이터 개체를 관리 합니다. | AMO&nbsp;서버 <br />AMO&nbsp;데이터베이스 <br /> Cube <br /> 차원 <br /> Partition 
Json<br/>Microsoft.AnalysisServices.Tabular.Json.dll | 도우미 DLL 업데이트를 제어 하는 NewtonSoftJson.dll (JSON.NET)을 래핑하는 Analysis Services 작업에서 JSON serialization 기능 변경의 위험을 제거 합니다. <br /> <br />이 DLL의 TOM 종속성 있고 코드에서 직접 사용할 수 없습니다. | 없음  
  
 ### <a name="understanding-assembly-dependencies"></a>어셈블리 종속성 이해
  
AMO에 대 한 프로그래밍, 솔루션 종속 Dll에 대 한 참조를 포함 해야 합니다. AMO와 TOM 모두 기본 클래스를 제공 하기 때문에 코어에 따라 다릅니다.

AMO의 일부 클래스에 AMO TOM에서 클래스를 참조 하기 때문에 TOM에 따라 달라 집니다. 예를 들어 AMO 데이터베이스 개체에 속성이 TOM dll에 구현 된 형식 모델의 모델입니다. 

![AMO TOM 종속성](../../analysis-services/tabular-model-programming-compatibility-level-1200/media/amo-tom-dependencies.png)

Microsoft.AnalysisServices.dll Microsoft.AnalysisServices.Tabular.dll, 하지 않고 배포할 수 없습니다 하지만 다른 없이 해당 네임 스페이스를 참조할 수 있습니다.

### <a name="choosing-which-namespace-to-use-in-code"></a>코드에서 사용 하는 네임 스페이스를 선택 합니다.

에 [개체 계층](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md) , 데이터베이스 아래의 개체 모두에 모델 개체를 통해 테이블 형식 메타 데이터 생성 또는 큐브, 차원 또는 측정값 그룹 개체를 통해 다차원 메타 데이터 생성입니다. 서버, 데이터베이스, 역할 또는 추적 수준에서 상위 수준 작업에 대 한 선택 참조 하는 네임 스페이스에 따라 달라 집니다 작업 코드를 지원 해야 합니다.

* 사용 하는 데이터베이스 개체 모델, 테이블, 열 및 테이블 형식 메타 데이터 생성으로 표시 되는 다른 개체에 대 한 액세스를 제공 해야 하 고 솔루션은 호환성 수준이 1200 이상일 경우 Tabular.Server 또는 Tabular.Database를 사용 합니다.
* 큐브, 데이터 원본, DataSourceViews, 및 차원과 같은 다차원 개체를 참조 하는 다운스트림 코드가 경우 AnalysisServices.Server 또는 AnalysisServices.Database를 사용 합니다.

도구 및 다양 한 데이터베이스 및 모델 유형이 지 원하는 응용 프로그램에 대 한 네임 스페이스 모두 필요 합니다. 

코드의 코어 네임 스페이스를 참조 하는 필요 하지 않습니다. 핵심 클래스는 공용 속성, 이름 및 설명와 같은 주요 개체에 대 한 제공할 목적으로 만든 기본 클래스입니다.  
  
## <a name="determine-whether-amo-and-tom-installation-is-required"></a>TOM 및 AMO 설치에 필요한 지 여부를 결정 합니다.  
   
 TOM 및 AMO 클라이언트 라이브러리에 함께 제공 됩니다. SQL Server 2016 Analysis Services 인스턴스, 클라이언트 라이브러리 또는 SQL server 2016 인스턴스를 대상으로 하는 SQL Server Data Tools의 버전을 이미 설치한 경우 Microsoft.AnalysisServices.dll 이미 설치 되었습니다.  
  
 어셈블리 이미 설치 되어 있는지 여부를 확인 하려면이 위치를 확인 합니다.
* C:\Windows\Microsoft.NET\assembly\GAC_MSIL
* C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies
* C:\Program Files\Microsoft SQL Server\130\DTS\Tasks
* C:\Program Files\Microsoft SQL Server\MSAS13 합니다. MSSQLSERVER\OLAP\bin
 
 다음 어셈블리 존재를 확인 합니다.
*  Microsoft.AnalysisServices.Core.dll
*  Microsoft.AnalysisServices.dll
*  Microsoft.AnalysisServices.Tabular.dll
*  Microsoft.AnalysisServices.Tabular.Json.dll   
   
## <a name="download-sqlasamo"></a>SQL_AS_AMO 다운로드  
 
 참고 Microsoft.AnalysisServices.dll는 NuGet 관리자를 통해 사용할 수 없습니다.
  
1. 로 이동 [의 SQL Server 2016 기능 팩 다운로드 페이지](https://www.microsoft.com/download/details.aspx?id=52676)합니다.  
  
2. **다운로드**를 클릭합니다.  
  
3. 선택 **\X64\SQL_AS_AMO.msi** 또는 **\X86\SQL_AS_AMO.msi**합니다. 둘 중 하나를 선택할 수 있습니다: TOM 및 AMO 어셈블리는 플랫폼 중립적입니다.
  
4. 클릭 **다음** 다운로드를 진행할 수 있습니다. .Msi 파일에 있습니다 프로그램 **다운로드** 폴더입니다.  
  
## <a name="install-sqlasamo"></a>SQL_AS_AMO 설치  
  
1. 두 번 클릭 **SQL_AS_AMO.msi** 단계별로 설치 합니다.  
  
2. 로 이동 **C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies** Microsoft.AnalysisServices.Core.dll, Microsoft.AnalysisServices.dll, Microsoft.AnalysisServices.Tabular.dll, 배치 되었는지 확인 하 고 Microsoft.AnalysisServices.Tabular.Json.dll 합니다.   
  
## <a name="add-references"></a>참조 추가  
  
1. **솔루션 탐색기** > **참조 추가** > **찾아보기**합니다.  
2. 로 이동 **C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies** 선택:  
   * Microsoft.AnalysisServices.Core  
   * Microsoft.AnalysisServices.Tabular  
   * Microsoft.AnalysisSerivces.Tabular.Json  
  
3. **확인**을 클릭합니다.  **솔루션 탐색기**, 어셈블리 참조 폴더에 없는지 확인 합니다.
  
4. 코드 페이지에서 데이터베이스 및 모델은 테이블 형식 1200 또는 호환성 수준이 더 높은 경우 Microsoft.AnalysisServces.Tabular 네임 스페이스를 추가 합니다. 
  
   ```   
   using Microsoft.AnalysisServices; 
   using Microsoft.AnalysisServices.Tabular;
   ```  
    필요에 따라 보다 광범위 한 집합의 테이블 형식 서버 모드에서 특히 SQL Server 2016 되지 않는 Analysis Services 인스턴스에 대 한 연결을 지원 하기 위해 Microsoft.AnalysisServces를 추가 합니다. 
 
    서버, 데이터베이스, 역할 및 추적 개체에 대 한 공통 클래스를 갖고 있는 네임 스페이스를 포함 하는 데 사용할 네임 스페이스는 정규화 하 여 참조가 모호해 지지 않도록 (예를 들어 Microsoft.AnalysisServices.Tabular.Server 인스턴스화하는 서버 개체는 테이블 형식 네임 스페이스를 사용 하 여)입니다.

## <a name="redistribute-amo-and-tom-with-your-application"></a>TOM 및 AMO 응용 프로그램과 함께 재배포합니다  
  
TOM 및 AMO는 재배포를 통해는 **sql_as_amo.msi** 설치 패키지입니다. AMO 또는 TOM으로 호출 하는 클라이언트 응용 프로그램에 대 한 설치 프로그램을 작성 하는 경우 추가 **sql_as_amo.msi** 실행 파일에 있습니다. TOM 및 AMO 클라이언트 라이브러리를 재배포 하기 위한 유일한 지원 되는 메커니즘입니다.  
  
패키지 자체 포함 하며 사용자 코드에서 TOM 및 AMO를 호출 하는 데 필요한 모든 어셈블리를 제공 합니다. SQL_AS_OLEDB.msi SQL_AS_ADOMD.msi를 등의 다른 패키지 TOM 프로그래밍 시나리오에 특히 필요 하지 않습니다.
