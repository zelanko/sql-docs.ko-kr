---
title: "SQL Server R Services 자습서 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 5ccc75f6-6703-47d9-b879-9a740569b45e
caps.latest.revision: 31
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 27
---
# SQL Server R Services 자습서
이 자습서를 사용하여 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 및 다음과 같은 지원되는 데이터 과학 시나리오에 대해 알아보세요.

+ R에서 모델을 개발하여 SQL Server에 배포
+ 데이터 과학자가 개발한 R 솔루션을 서버 또는 다른 프로덕션 환경에 배포하여 R 코드 운영화
+ R과 SQL Server 간 데이터 이동
+ 원격 및 로컬 계산 컨텍스트를 사용하는 방법
  

## <a name="a-namebkmkend-to-endadeveloping-an-end-to-end-advanced-analytics-solution"></a><a name="bkmk_end-to-end"></a>종단 간 고급 분석 솔루션 개발  

[데이터 과학 종단 간 연습](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md) 

데이터 취득 및 분석에서 점수 매기기에 이르기까지 종단 간 데이터 과학 프로세스를 경험하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터를 사용하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장하여 모델을 운영화하는 방법을 알아봅니다.  
PowerShell을 사용하여 뉴욕 시 택시 데이터 집합을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 가져와 R을 사용하여 데이터를 탐색합니다. 

그런 다음 예측 모델을 작성하고 일괄 처리 및 단일 예측 모드에서 점수 매기기를 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 R 모델을 배포합니다. 

  
이 자습서는 PowerShell 및 SQL Server Management Studio와 같은 개발자 도구뿐만 아니라 R에 대해 잘 알고 있는 사용자를 위한 것입니다. R 개발 환경에 액세스할 수 있어야 하고 R 명령을 잘 알고 있어야 합니다. 
  
## <a name="a-namebkmkdatascienceadata-science-deep-dive"></a><a name="bkmk_dataScience"></a>데이터 과학 심층 분석  

[RevoScaleR 및 SQL Server 시작](http://go.microsoft.com/fwlink/?LinkID=691640&clcid=0x809)  

이 연습은 이미 R 언어를 잘 알고 있고 Revolution Analytics에서 제공하는 Microsoft R의 향상된 R 패키지 및 함수에 대해 알아보려는 데이터 과학자나 개발자를 위해 작성되었습니다. 

ScaleR 패키지의 함수를 사용하여 R과 SQL 간에 데이터를 이동하고 특정 태스크에 맞게 계산 컨텍스를 전환하는 방법을 알아봅니다. 몇 가지 모델 및 그림을 만들어 개발 환경과 SQL Server 간에 이동합니다.  
  
이 자습서는 이전부터 R을 사용해 왔으며 RevoScaleR 및 SQL Server가 R 환경을 향상하는 방법에 대해 자세히 알아보려는 사용자를 위해 작성되었습니다.

## <a name="in-database-advanced-analytics-for-the-sql-developer"></a>SQL 개발자를 위한 데이터베이스 내 고급 분석  
  
[SQL 개발자를 위한 데이터베이스 내 고급 분석&#40;자습서&#41;](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)

[!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 전체 고급 분석 솔루션을 빌드 및 배포합니다. 이 예제에서는 오픈 소스 R 언어를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진과 통합하는 방법에 중점을 둡니다. R 코드를 저장 프로시저에 래핑하고, R 모델을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장하고, 예측을 위해 매개 변수가 있는 R 모델 호출을 수행하는 방법을 알아봅니다. 
  
이 자습서는 R 솔루션을 지원하고 SQL Server에 R 모델을 배포하는 방법을 알아보려는 SQL 개발자, 응용 프로그램 개발자 또는 SQL DBA를 위해 작성되었습니다.  R 환경은 필요하지 않습니다. 모든 R 코드가 제공되며 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 친숙한 비즈니스 인텔리전스 및 SQL 개발 도구만 사용하여 전체 솔루션을 빌드할 수 있습니다.   

## <a name="use-r-services-in-an-application"></a>응용 프로그램에서 R 서비스 사용

[Build an intelligent app with SQL Server and R](https://www.microsoft.com/sql-server/developer-get-started/r)(SQL Server 및 R을 사용하여 지능형 앱 구축)

이 자습서에서는 스키 대여 사업에서 기계 학습을 이용하여 향후 대여 상황을 예측함으로써 향후 수요에 맞도록 효과적으로 사업 계획을 준비하고 직원이 대비할 수 있는 방법을 알아봅니다.


## <a name="using-r-code-in-t-sql"></a>T-SQL에서 R 코드 사용  

[Transact-SQL에서 R 코드 사용&#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)  

[!INCLUDE[tsql](../../includes/tsql-md.md)]에서 R을 사용하는 기본 구문을 보여 주는 매우 짧은 독립 실행형 예제 시리즈입니다. 

SQL에서 R 런타임을 호출하고, R과 SQL 간 데이터 형식의 주요 차이점을 확인하고, SQL 코드에서 R 함수를 래핑하고, R 출력을 SQL 테이블에 저장하는 저장 프로시저를 실행하는 방법을 알아봅니다.
  
이 자습서는 R Services를 처음 사용하고 T-SQL을 사용하여 R을 호출하는 방법의 기본 사항을 알아보려는 사용자를 위해 작성되었습니다. R을 사용해 본 경험은 없어도 되지만, SQL Server Management Studio 또는 데이터베이스에 연결하고 간단한 T-SQL 쿼리를 실행할 수 있는 다른 도구를 사용하는 방법을 알아야 합니다.

  
## <a name="a-namebkmkprerequisitesaprerequisites"></a><a name="bkmk_Prerequisites"></a>필수 구성 요소
  
이러한 자습서를 실행하려면 [ 설치](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)에 설명된 대로 **R Services(In-Database)**를 다운로드하고 설치해야 합니다.

SQL Server 설치 프로그램을 실행한 후 다음 추가 단계를 수행해야 합니다.
+ *sp_configure*를 실행하여 R Services 사용 설정
+ 서버 다시 시작
+ R 런타임을 호출하는 서비스에 필요한 권한이 있는지 확인
+ R 코드에 사용할 SQL 로그인 또는 Windows 사용자 계정에 서버 및 해당 데이터베이스에 연결하는 데 필요한 권한이 있는지 확인

문제가 발생할 경우 몇 가지 일반적인 문제에 대해서는 [SQL Server R Services의 업그레이드 및 설치](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md) 문서를 참조하세요.

아직 선호하는 R 개발 환경이 없는 경우 다음 도구 중 하나를 설치하여 시작할 수 있습니다.

+ [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-get-started)
+ [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/)

표준 R 라이브러리만으로는 이러한 자습서를 사용하기에 부족합니다. R 개발 환경과 R을 실행하는 SQL Server 컴퓨터 둘 다에 Microsoft의 ScaleR 패키지가 있어야 합니다. Microsoft R의 기능에 대한 자세한 내용은 [Microsoft R Products](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started#compare-prods)(Microsoft R 제품) 문서를 참조하세요.

## <a name="additional-resources"></a>추가 리소스

이러한 자습서를 마쳤으면 다음 링크를 사용하여 고급 시나리오 및 샘플을 확인하세요.
  
### <a name="end-to-end-solution-templates-for-key-machine-learning-tasks"></a>주요 Machine Learning 작업을 위한 종단 간 솔루션 템플릿  

[Machine Learning Templates with SQL Server 2016 R Services](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/)(SQL Server 2016 R Services를 사용한 Machine Learning 템플릿)  

Microsoft Machine Learning 팀은 다음과 같은 주요 Machine Learning 작업을 위한 Machine Learning 솔루션을 빠르게 시작할 수 있도록 사용자 지정 가능한 템플릿 집합을 제공했습니다.  
* 사기 검색  
* 사용자 지정 이탈 예측  
* 예측 유지 관리  
  
SQL Server 저장 프로시저를 사용하여 점수 매기기 모델을 학습하고 배포하는 방법에 대한 지침과 함께 모든 T-SQL 및 R 코드가 제공됩니다. 

### <a name="sample-data-and-sample-scripts"></a>샘플 데이터 및 샘플 스크립트  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에 대한 Product 샘플은 Microsoft 다운로드 센터에서 사용할 수 있습니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에 대한 샘플만 가져오려면 zip 파일을 선택한 다음 **Advanced Analytics**폴더를 엽니다.  일부 지침은 이전 릴리스에 대한 것이지만, 벤포드 법칙을 기반으로 한 보험 사기 감지 데모가 있으며 데모에 유용할 수 있는 매우 작은 데이터 집합(Iris 데이터 집합)에 대한 예측 모델의 간단한 연습도 있습니다.
  
[SQL Server 2016 Product 샘플](https://www.microsoft.com/en-us/download/details.aspx?id=49502)  
### <a name="learn-more-about-r"></a>R에 대한 자세한 정보  
R에 대한 일반적인 내용을 알아보려면 [R 언어 리소스](http://revolutionanalytics.com/r-language-resources)에 나열된 여러 유용한 리소스 중 하나를 참조하세요.  
  
[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서 제공되는 R 패키지에 대한 자세한 내용은  [Revolution Analytics 사이트](http://go.microsoft.com/fwlink/?LinkId=691541)를 참조하세요.  
  
이 블로그 게시물에서는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 에서 제공하는 R 패키지 및 함수를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하는 프로세스를 간략하게 설명하고, 샘플 코드 [SQL Server 내에서 R 사용](http://blog.revolutionanalytics.com/2015/10/previewing-using-revolution-r-enterprise-inside-sql-server.html)을 포함합니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server R Services 시작](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
[SQL Server R Services 기능 및 태스크](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)  
  
