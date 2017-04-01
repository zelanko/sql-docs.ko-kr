---
title: "SQL Server R Services의 새로운 기능 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6aff043a-8b37-4f3f-9827-10a671e1ad1c
caps.latest.revision: 36
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 35
---
# SQL Server R Services의 새로운 기능
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]는 엔터프라이즈급 데이터 과학을 지원하는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 SQL Server vNext의 기능입니다.  R은 고급 분석에 가장 인기 있는 프로그래밍 언어로, 매우 풍부한 패키지와 활발히 활동하면서 빠르게 성장하고 있는 개발자 커뮤니티를 제공합니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]는 매우 인기 있는 오픈 소스 R 언어를 비즈니스에 도입하도록 도와줍니다. 
  
 > [!TIP] SQL Server 2016 R 서비스가 이미 있나요?
 > 이제 2016 인스턴스에 Microsoft R Server 최신 버전을 설치하여 R 구성 요소가 좀 더 자주 업데이트되도록 할 수 있습니다. 자세한 내용은 [Microsoft R Server 9.0.1](https://msdn.microsoft.com/microsoft-r/rserver-whats-new)을 참조하세요.  

## <a name="whats-new-in-sql-server-vnext"></a>SQL Server vNext의 새로운 기능
  
+ **MicrosoftML** 패키지 도입

   MicrosoftML은 Microsoft R Server 및 Microsoft 데이터 과학 팀에서 제공하는 새로운 R용 기계 학습 패키지입니다. MicrosoftML은 몇 줄의 코드만으로 R 모델에서 대량의 텍스트 데이터와 차원 범주 데이터를 처리하기 위한 향상된 속도, 성능 및 확장성을 제공합니다. 또한 Microsoft R Server 고객은 Azure Machine Learning에 포함된&5;개의 신속하고 매우 정확한 학습자에 액세스할 수 있습니다. 
   
   자세한 내용은 [SQL Server R Services에서 MicrosoftML 패키지 사용](../../advanced-analytics/r-services/using-the-microsoftml-package-with-sql-server-r-services.md)을 참조하세요.
   
+ 데이터 과학자를 위한 보다 수월해진 패키지 관리

  이제 데이터베이스 관리자의 도움 없이도 SQL Server에서 필요한 R 패키지를 설치할 수 있습니다. **RevoScaleR**의 새 패키지 설치 및 제거 함수를 사용하면 클라이언트 컴퓨터에서 R Services의 패키지를 쉽게 설치 및 업데이트할 수 있습니다. 
  
  데이터베이스 관리자가 인스턴스 수준 및 데이터베이스 수준 둘 다에서 패키지와 연결된 사용 권한을 관리할 수 있도록 새 역할이 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]에 포함되었습니다. 
  
  자세한 내용은 [SQL Server R Services에 대한 R 패키지 관리](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)를 참조하세요. 
     
+ R 모델 개체를 읽고 쓰기 위한 **RevoScaleR**의 새로운 함수

  이제 모델의 신속한 로드 및 읽기를 위해 새로운 직렬화 함수 및 보다 간단한 모델 저장소 형식이 RevoScaleR에 포함되었습니다. 
  
  자세한 내용은 [ODBC를 사용하여 SQL Server에서 R 개체 저장 및 로드](../../advanced-analytics/r-services/save-and-load-r-objects-from-sql-server-using-odbc.md)를 참조하세요. 

+ 보다 편리한 SQL 통합을 위한 **sqlrutils** 패키지

  이 R 패키지는 R 코드에 대한 SQL 저장 프로시저 호출을 생성하는 데 도움이 됩니다. 그런 다음 생성된 SQL 저장 프로시저를 SQL Server R Services에서 사용할 수 있습니다. 제공된 예제는 SQL 저장 프로시저에서 매개 변수화할 수 있는 함수에 R 코드를 통합하는 데 도움이 됩니다.
  
  자세한 내용은 [sqlrutils를 사용하여 R 코드에 대한 저장 프로시저 생성](../../advanced-analytics/r-services/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)을 참조하세요. 
  

+ 편리한 SSAS 연결을 위한 **olapR** 패키지

   이 새로운 패키지는 R 및 SQL Server Analysis Services의 연결 수준을 높여 R에서 OLAP 데이터를 분석에 쉽게 사용할 수 있게 해줍니다. 기존 MDX 쿼리를 실행하고 R 데이터 프레임을 다시 가져오거나, R 코드에서 큐브 축 및 슬라이서를 정의하여 간단한 MDX 문을 작성할 수 있습니다. 
   
   자세한 내용은 [R에서 OLAP 큐브의 데이터 사용](../../advanced-analytics/r-services/using-data-from-olap-cubes-in-r.md)을 참조하세요.
   

  
## <a name="features-in-sql-server-2016-r-services-and-sql-server-vnext"></a>SQL Server 2016 R Services 및 SQL Server vNext의 기능  
  
- R을 사용한 신속하고 병렬화 가능한 기계 학습용 **RevoScaleR** 패키지.

-   SQL 로그인 및 Windows 통합 인증을 둘 다 지원합니다.  
    
-   R과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 연결하는 SQL Satellite 프로세스의 최적화, 대량 데이터 사용을 위한 데이터 페이징 지원, 수십억 개 행의 빠른 처리를 위한 스트리밍을 비롯한 중요한 성능 개선 기능. 
  
-   SQL Server 리소스 풀을 사용하여 R 프로세스에서 사용되는 메모리를 관리합니다. 자세한 내용은 [CREATE EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)을 참조하세요.  
  

### <a name="tools-and-setup"></a>도구 및 설치

-   모든 구성 요소의 편리한 설치. SQL Server 설치 마법사는 **SQL Server R Services(In-Database)** 또는 **Microsoft R Server(독립 실행형)**를 설치할 수 있습니다.   설치 마법사를 실행하는 경우 SQL Server 인스턴스를 설정할 때 R Services를 선택하고, 데이터 과학 워크스테이션을 설정하는 경우 R 서버(독립 실행형)를 선택합니다.   설치 옵션에 대한 자세한 내용은 [SQL Server R Services&#40;In-Database&#41; 설치](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md) 또는 [독립 실행형 R 서버 만들기](../../advanced-analytics/r-services/create-a-standalone-r-server.md)를 참조하세요.  

-   SQL Server에서 데이터를 사용할 필요가 없는 경우 다양한 플랫폼에서 실행되고 인기 있는 오픈 소스 R 언어에 엔터프라이즈 규모와 성능을 제공하는 [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)]를 고려합니다. [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)]. 자세한 내용은 MSDN에서 [R 서버&#40;독립 실행형&#41;](../../advanced-analytics/r-services/r-server-standalone.md) 또는 [R 서버 소개](https://msdn.microsoft.com/microsoft-r/rserver)를 참조하세요.

- Microsoft R Server 9.0.1을 사용하도록 SQL Server 2016 인스턴스를 업그레이드하려면 [SqlBindR.exe 유틸리티](https://msdn.microsoft.com/library/mt791781.aspx)를 사용하세요.  

- [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-install)는 R Services 또는 R 서버에서 실행되는 R 솔루션을 빌드하는 데 필요한 모든 도구와 라이브러리를 포함하는 무료 R 환경입니다.  

-   R Tools for Visual Studio는 표준 R 대화형 및 변수 창, R 함수의 IntelliSense, 디버깅, R Markdown, Word 및 HTML로 내보내기 등 R에 대한 풍부한 지원을 포함하는 Visual Studio용 무료 플러그 인입니다.  자세한 내용은 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/)를 참조하세요.  

## <a name="learn-more"></a>자세한 정보
  
-  SQL Server 통합에 대해 알아보려는 데이터 과학자와 T-SQL 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 익숙한 환경을 사용해서 R 솔루션을 만들려는 SQL 개발자 둘 다를 위해 리소스가 제공됩니다. 
   + [SQL Server R Services 자습서](https://msdn.microsoft.com/library/mt591993.aspx)
   + [Free ebook: Data Science with SQL Server 2016](https://mva.microsoft.com/ebooks/)(무료 전자책: SQL Server 2016을 사용한 데이터 과학)
 
+ 바로 사용할 수 있는 준비된 솔루션이 필요한 경우 Microsoft 데이터 과학 팀에서 제공하는 이러한 [기계 학습 템플릿](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/)을 사용하는 것이 좋습니다. 이 템플릿은 예측 유지 관리 및 이탈 방지를 비롯한 일반적인 분석 태스크에 대한 실용적인 해결책을 보여 줍니다.
 

  
## <a name="see-also"></a>참고 항목  
[SQL Server vNext의 새로운 기능](../../sql-server/what-s-new-in-sql-server-vnext.md)
  