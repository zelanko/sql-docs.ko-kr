---
title: 기존 Analysis Services 테이블 형식 서버 및 데이터베이스에 연결 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 13900e4aaad52d39a2691fb40d0e419f55f660fc
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38033393"
---
# <a name="connect-to-existing-analysis-services-tabular-server-and-database"></a>기존 Analysis Services 테이블 형식 서버 및 데이터베이스에 연결
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
SQL Server 2016 Analysis Services Management Objects (AMO) 서버 연결을 설정 하는 데 사용할 수 있는 여러 네임 스페이스를 포함 합니다. 이 문서에는 모델 및 1200에서 생성 된 데이터베이스에 대 한 Microsoft.AnalysisServices.Tabular 네임 스페이스를 사용 하 여 서버 연결을 설정 하는 방법 또는 더 높은 호환성 수준을 설명 합니다. 

Analysis Services 서버에 연결 하려면 코드는 서버 개체를 인스턴스화할 하 고에 Connect 메서드를 호출 해야 합니다. 연결 되 면 설정을 현재 Analysis Services 인스턴스의 서버 개체의 속성에 반영 됩니다. 

최상위 연결에 대 한 다음 클래스를 사용할 수 있습니다. 

* Microsoft.AnalysisServices.Server 
* Microsoft.AnalysisServices.Database 
* Microsoft.AnalysisServices.Tabular.Server 
* Microsoft.AnalysisServices.Tabular.Database 

두 네임 스페이스 서버 및 데이터베이스 개체에 대 한 연결을 제공에서 볼 수 있습니다: amo의 경우 원래 Microsoft.AnalysisServices namespace 및 TOM 새 Microsoft.AnalysisServices.Tabular 네임 스페이스입니다.

이유는 동일한 작업에 대 한 두 개의 네임 스페이스? 답은 개체 계층이 모드별 않았고 모델 트리는 다차원 또는 테이블 형식 메타 데이터 구성 데이터베이스 및 모델 수준에서 다운스트림을 합니다. 모델 트리에서 호출을 위해 서버 또는 데이터베이스 개체는 두 모델 유형에 대해 제공 됩니다.

> [!NOTE]  
>  모델 정 및 작업에 사용 되는 메타 데이터는 두 가지 모드에 대 한 완전히 다릅니다. 두 개의 별도 네임 스페이스에는 DDL (데이터 정의 언어)를 분리 하 여 개발 환경에 특정 모델 유형에 필요한 API만 표시를 통해 간소화 됩니다. 

DDL 다른 있지만 서버에 대 한 연결에서 동일 모든 모드, 버전 및 버전입니다. 서버와 네임 스페이스 중 하나를 통해 데이터베이스 연결을 지 원하는 일반 도구 또는 모든 Analysis Services 인스턴스에 연결 하는 스크립트를 작성할 수 있습니다 또는 데이터베이스 모델의 유형을 알 필요 없이 서버에서 호스트 되는 합니다.  

이러한 유연성을이 통해 어셈블리 간의 종속성을 설명합니다. 데이터베이스 수준 (예를 들어, 테이블 형식 1200 데이터베이스에서 모델 또는 큐브, 차원 또는 측정값 그룹 다차원 또는 테이블 형식 1050-1103 데이터베이스 내에서) 다음 호출을 실행 하려면 AMO의 TOM 종속성을 갖습니다. 

반면, TOM AMO에 종속성이 있는 하지 않습니다. TOM 다차원 메타 데이터 (Cubes) 탐색을 사용할 수 없습니다, 있지만 AMO 다차원 및 테이블 형식 메타 데이터를 탐색에 사용할 수 있습니다. 

이러한 이유로 모든 AMO 어셈블리에 대 한 참조를 추가 합니다. 프로젝트를 설정 하는 첫 번째 단계는 필요 합니다. 참조 [설치를 참조 하 고 TOM 클라이언트 라이브러리를 분산](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md) 세부 정보에 대 한 합니다. 

> [!NOTE]  
>  서버 및 데이터베이스 연결 MajorObject에서 상속 되는 레거시 AMO 클래스를 기반으로 합니다. 주요 및 보조 개체는 테이블 형식 모델 트리에서 사용 되지 않습니다, 하지만 MajorObject 클래스는 연결을 설정 하려면 사용할 API에 관계 없이 서버 및 데이터베이스 개체에 대 한 기본 클래스로 표시 됩니다.  

## <a name="code-example-server-connection"></a>코드 예제: 서버 연결 

다음은 C# 코드 샘플을 로컬 Analysis Services 인스턴스에 연결 하 고 콘솔 창에서 해당 속성을 나열 하는 방법을 보여주는입니다. 

이 예제에서는 서버 개체의 속성 중 일부만 표시 있지만 ServerMode 및 DefaultCompatibilityLevel를 비롯 하 여 더 많은 속성이 있습니다.  

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
이 프로그램을 실행 하면 출력 콘솔 창에서 서버 개체에 한 속성을 보여 줍니다. 

## <a name="authentication-and-authorization"></a>인증 및 권한 부여 

서버 또는 Analysis Services 데이터베이스 연결을 사용 하는 읽기 / 쓰기 작업에 대 한 가장된 연결 요청을 통과 한 관리 권한 필요 합니다.  

최근 몇 년 동안 매우 특정 조건에서 사용자 지정 인증을 허용 하도록 Analysis Services 보안 인프라가 확장 하지만 지원 되는 외부 인증 방법은 Windows 통합된 보안. 보안 주체는 유효한 Windows 도메인 사용자 또는 그룹 계정으로 간주 됩니다.  

Windows 2012 이상에서는 위임 도메인 간에 전달할 수 있습니다. Analysis Services에서 위임이 DirectQuery 모델에만 사용 됩니다. 그렇지 않은 경우 연결은 직접 또는 가장 합니다. 

## <a name="next-steps"></a>다음 단계 

연결을 설정한 후 논리적인 다음 단계를 두 데이터베이스를 나열 하려면 기존 서버에서 이미 되었거나 아마도 비어 있는 새 데이터베이스를 만듭니다. 다음 링크는 다음과 같습니다.이 두 가지 기본 작업을 보여 주는 코드 샘플을 

- [빈 데이터베이스 만들기 및 배포](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-and-deploy-an-empty-database-analysis-services-amo-tom.md)
- [기존 데이터베이스 목록](../../analysis-services/tabular-model-programming-compatibility-level-1200/list-existing-databases-on-a-tabular-server-analysis-services-amo-tom.md)
