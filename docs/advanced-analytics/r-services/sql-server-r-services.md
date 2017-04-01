---
title: "SQL Server R 서비스 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: 38
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 36
---
# SQL Server R 서비스
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]은 새로운 통찰력을 얻는 지능형 응용 프로그램 개발 및 배포를 위한 플랫폼을 제공합니다. 풍부하고 강력한 R 언어와 커뮤니티의 많은 패키지를 활용하여 모델을 만들고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 사용하여 예측을 생성할 수 있습니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]과 R 언어를 통합하므로, 데이터와 밀접하게 분석을 유지하고 데이터 이동과 연관된 비용 및 보안 위험을 제거할 수 있습니다.  
  
 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]은 탁월한 성능, 보안, 신뢰성 및 관리성을 제공하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구 및 기술의 포괄적인 집합으로 오픈 소스 R 언어를 지원합니다. 편안하고 친숙한 도구를 사용하여 R 솔루션을 배포하고 프로덕션 응용 프로그램은 R 런타임을 호출하고 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 예측 및 비주얼을 검색할 수 있습니다. 또한 [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) 라이브러리를 통해 R 솔루션의 규모와 성능을 향상할 수 있습니다.  
  
SQL Server 설치 프로그램을 통해 서버와 클라이언트 구성 요소를 모두 설치할 수 있습니다.  
  
+   **R Services(In-Database):** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설정 중 이 기능을 설치하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에서 R 스크립트의 보안 실행을 지원합니다.  
  
     이 기능을 선택할 경우 확장 프로그램이 데이터베이스 엔진에 설치되어 R 스크립트의 실행을 지원하고 새로운 서비스 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]이(가) 생성되어 R 런타임과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 간 커뮤니케이션을 관리합니다.  
  
+   **Microsoft R Server(독립 실행형):** 병렬 처리 및 기타 성능 향상을 지원하는 소유 패키지와 결합된 오픈 소스 R 배포입니다. R Services(In-Database)와 Microsoft R Server(독립 실행형)에는 모두 향상된 연결 및 성능을 위한 **ScaleR** 라이브러리와 함께 기본 R 런타임과 패키지가 포함됩니다. 
  
+    [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/index#mrc)는 별도의 무료 설치 프로그램으로 사용할 수 있습니다.  Microsoft R Client를 사용하여 SQL Server에서 실행되는 R Services 또는 Windows나 Teradata, Hadoop에서 실행되는 Microsoft R Server로 배포할 수 있는 솔루션을 개발할 수 있습니다. 
     

  > [!NOTE] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 R 코드를 실행해야 하는 경우 [여기](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)에 설명된 것처럼 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]을(를) 설치하세요.
  >  
  > Microsoft R Server\(독립 실행형\)는 SQL Server를 실행하지 않는 Windows 컴퓨터에서 ScaleR 라이브러리 사용을 위해 설계된 별도의 옵션입니다. 
>   
>  그러나 엔터프라이즈 버전을 가지고 있는 경우 R 개발에 사용하는 노트북이나 기타 컴퓨터에 Microsoft R Server\(독립 실행형\)를 설치하여 R Services \(In-Database\)를 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 쉽게 배포할 수 있는 R 솔루션을 만드는 것이 좋습니다.
  
## <a name="additional-resources"></a>추가 리소스  
  
 [SQL Server R Services 시작](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)   
 SQL Server와 함께 R 사용에 대한 일반적인 시나리오를 설명합니다.  
  
[SQL Server R Services In-Database 설치](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
SQL Server 설치의 일부로 R과 관련된 데이터베이스 구성 요소를 설치합니다.  
  
[SQL Server R Services 자습서](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
R 코드에서 SQL Server 데이터 원본을 만드는 방법 및 원격 계산 컨텍스트를 사용하는 방법을 알아봅니다. SQL 개발자를 대상으로 하는 다른 자습서에서는 SQL Server에서 R 모델을 배포하고 교육하는 방법을 보여 줍니다.  
  
## <a name="see-also"></a>관련 항목:  
  
 [Microsoft R Server&#40;독립 실행형&#41; 시작](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
 
 [독립 실행형 R Server 설치)](../../advanced-analytics/r-services/create-a-standalone-r-server.md) 
  