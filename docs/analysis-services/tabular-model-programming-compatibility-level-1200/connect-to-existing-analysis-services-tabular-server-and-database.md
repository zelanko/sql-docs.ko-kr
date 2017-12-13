---
title: "기존 Analysis Services 테이블 형식 서버 및 데이터베이스에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 05be704e-4ee4-4101-b5ce-96fdda18c639
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e34cc306126acc431048fd93b7eab99049bc2414
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="connect-to-existing-analysis-services-tabular-server-and-database"></a>기존 Analysis Services 테이블 형식 서버 및 데이터베이스에 연결
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]SQL Server 2016 Analysis Services Management Objects (AMO) 서버 연결을 설정 하는 데 사용할 수 있는 몇 가지 네임 스페이스를 포함 합니다. 이 문서에서는 모델 및 1200에서 생성 된 데이터베이스에 대 한 Microsoft.AnalysisServices.Tabular 네임 스페이스를 사용 하 여 서버 연결을 설정 하는 방법 또는 더 높은 호환성 수준을 설명 합니다. 

Analysis Services 서버에 연결할 코드는 서버 개체를 인스턴스화할 하 고에 Connect 메서드를 호출 해야 합니다. 연결 되 면 서버 개체의 속성에는 현재 Analysis Services 인스턴스의 설정이 반영 됩니다. 

다음 클래스는 최상위 연결에 사용할 수 있습니다. 

* Microsoft.AnalysisServices.Server 
* Microsoft.AnalysisServices.Database 
* Microsoft.AnalysisServices.Tabular.Server 
* Microsoft.AnalysisServices.Tabular.Database 

두 개의 네임 스페이스 서버 및 데이터베이스 개체에 대 한 연결을 제공 볼 수 있듯이: AMO에 대 한 원래 Microsoft.AnalysisServices 네임 스페이스 및 TOM에 대 한 새 Microsoft.AnalysisServices.Tabular 네임 스페이스입니다.

이유는 동일한 작업에 대 한 두 개의 네임 스페이스? 그 답은 여기서 개체 계층 구조 모드별 되며 모델 트리는 다차원 또는 테이블 형식 메타 데이터 구성 데이터베이스 및 모델 수준에서 다운스트림, 합니다. 모델 트리에서 호출 하는 서버 또는 데이터베이스 개체 두 모델 유형에 제공 됩니다.

> [!NOTE]  
>  모델 정 및 작업에 사용 되는 메타 데이터는 두 가지 모드에 대 한 완전히 다릅니다. 두 개의 별도 네임 스페이스에 데이터 정의 언어 (DDL)를 분리 하 여 특정 모델 유형에 필요한 API만 표시를 통해 개발 환경은 간소화 됩니다. 

DDL 달라 집니다 하지만 서버에 대 한 연결 전반에서 모두 동일 모드, 버전 및 버전입니다. 네임 스페이스 중 하나를 통해 데이터베이스 연결 및 서버를 지 원하는 일반 도구 또는 Analysis Services 인스턴스에 연결 하는 스크립트를 작성할 수 있습니다 또는 데이터베이스 모델의 유형을 알 필요 없이 서버에서 호스트 되는 합니다.  

이러한 유연성 어셈블리 간의 종속성을 설명합니다. 데이터베이스 수준 (예를 들어 테이블 형식 1200 데이터베이스 내에서 모델 또는 큐브, 차원 또는 측정값 그룹 다차원 또는 테이블 형식 1050-1103 데이터베이스 내에서)에서 호출을 수행 하기 위해 AMO가 TOM에 종속 됩니다. 

반면, TOM AMO에 종속성이 있는 되지 않습니다. TOM (큐브) 다차원 메타 데이터를 탐색에 사용할 수 없습니다, 있지만 AMO 다차원 및 테이블 형식 메타 데이터를 탐색 하 사용할 수 있습니다. 

이러한 이유로 프로젝트 설정 하는 첫 번째 단계는 모든 AMO 어셈블리에 대 한 참조를 추가 해야 합니다. 참조 [설치 참조 하 고, TOM 클라이언트 라이브러리를 분산](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md) 대 한 자세한 내용은 합니다. 

> [!NOTE]  
>  서버 및 데이터베이스 연결 MajorObject에서 상속 하는 레거시 AMO 클래스를 기반으로 합니다. 주요 및 보조 개체는 테이블 형식 모델 트리를 사용 되지 않습니다 되지만 MajorObject 클래스는 연결을 설정 하려면 사용 하는 API에 관계 없이 서버 및 데이터베이스 개체에 대 한 기본 클래스로 표시 됩니다.  

## <a name="code-example-server-connection"></a>코드 예제에서는: 서버 연결 

다음은 C# 코드 예제는 로컬 Analysis Services 인스턴스에 연결 하 고 콘솔 창에서 해당 속성을 나열 하는 방법을 보여 주는입니다. 

서버 개체의 속성 중 일부만 보여 주는이 예제 있지만 ServerMode 및 DefaultCompatibilityLevel 포함 하 여 사용할 수 있는 더 많은 속성이 있습니다.  

```
using System; 
using Microsoft.AnalysisServices.Tabular; 

namespace TOMSamples 
{ 
    class Program 
    { 
        static void Main(string[] args) 
        { 
            // 
            // Connect to the local default instance of Analysis Services 
            // 
            string ConnectionString = "DataSource=localhost"; 


            // 
            // The using syntax ensures the correct use of the 
            // Microsoft.AnalysisServices.Tabular.Server object. 
            // 
            using (Server server = new Server()) 
            { 
                server.Connect(ConnectionString); 

 
                Console.WriteLine("Connection established successfully."); 
                Console.WriteLine(); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.WriteLine("Server name:\t\t{0}", server.Name); 
                Console.WriteLine("Server product name:\t{0}", server.ProductName); 
                Console.WriteLine("Server product level:\t{0}", server.ProductLevel); 
                Console.WriteLine("Server version:\t\t{0}", server.Version); 
                Console.ResetColor(); 
                Console.WriteLine(); 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```
이 프로그램을 실행 하는 경우 출력이 콘솔 창에서 서버 개체에 속성이 표시 됩니다. 

## <a name="authentication-and-authorization"></a>인증 및 권한 부여 

서버 또는 Analysis Services 데이터베이스 연결을 읽기 / 쓰기 작업에 대 한 가장된 연결 요청을 통해 전달 하기 위해 사용 하는 관리 권한이 필요 합니다.  

있지만 최근 몇 년 동안 매우 특정 조건에서 사용자 지정 인증을 허용 하도록에 Analysis Services 보안 인프라가 확장만 지원 되는 외부 인증 방법은 Windows 통합된 보안 합니다. 보안 주체는 유효한 Windows 도메인 사용자 또는 그룹 계정을 것으로 간주 됩니다.  

Windows 2012 이상에서는 위임 도메인 간에 전달할 수 있습니다. Analysis Services에서 위임이; DirectQuery 모델에 대해서만 사용 되는 그렇지 않으면 연결은 직접 또는 가장 됩니다. 

## <a name="next-steps"></a>다음 단계 

연결을 만든 다음 논리는 다음 단계는 서버에 이미 목록 기존 데이터베이스 중 하나에 되었거나 아마도 비어 있는 새 데이터베이스를 만듭니다. 다음 링크는 두 가지 기본적인 작업을 보여 주는 코드 예제가 포함: 

- [만들기 및 빈 데이터베이스를 배포 합니다.](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-and-deploy-an-empty-database-analysis-services-amo-tom.md)
- [기존 데이터베이스를 나열](../../analysis-services/tabular-model-programming-compatibility-level-1200/list-existing-databases-on-a-tabular-server-analysis-services-amo-tom.md)
