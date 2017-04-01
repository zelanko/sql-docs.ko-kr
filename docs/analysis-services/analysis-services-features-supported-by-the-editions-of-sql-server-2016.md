---
title: "SQL Server 2016 버전에서 지원하는 Analysis Services 기능 | Microsoft Docs"
ms.custom: ""
ms.date: "09/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
  - "analysis-services/multidimensional-tabular"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f09d7be1-bd63-43f8-b91c-bf19166b4457
caps.latest.revision: 4
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 3
---
# SQL Server 2016 버전에서 지원하는 Analysis Services 기능
이 항목은 다른 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]버전에서 지원되는 기능의 세부 정보를 제공합니다.  
  
 SQL Server 평가 버전은 180일 동안 시험용으로 사용할 수 있습니다.  
  
 최신 릴리스 정보는 [SQL Server 2016 Release Notes](../sql-server/sql-server-2016-release-notes.md)를 참조하세요. 새로운 기능에 대한 최신 정보는 [Analysis Services의 새로운 기능](../analysis-services/what-s-new-in-analysis-services.md)을 참조하세요.
    
 **SQL Server 2016을 사용해 보세요.**    
    
 > [![평가 센터에서 다운로드](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[평가 센터에서 SQL Server 2016 다운로드](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Azure 가상 컴퓨터 소형](../analysis-services/media/azure-virtual-machine-small.png) **[이미 설치된SQL Server 2016으로 가상 컴퓨터를 스핀업](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)**    
    
  
 Evaluation 및 Developer 버전에서 지원하는 기능은 SQL Server Enterprise Edition을 참조하세요.
  
 SQL Server 기술에 대한 표로 이동하려면 해당 링크를 클릭합니다. 
 
 -  [Analysis Services](#SSAS)  
  
-   [BI 의미 체계 모델(다차원)](#BIMD)  
  
-   [BI 의미 체계 모델(테이블 형식)](#BIT)  
  
-   [SharePoint용 PowerPivot](#PPSP)  
  
-   [데이터 마이닝](#DM)  
  
-   [Business Intelligence 클라이언트](#BIC)  

##  <a name="SSAS"></a> Analysis Services  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|확장 가능 공유 데이터베이스|예||||||예|  
|데이터베이스 백업/복원 및 연결/분리|예|예|||||예|  
|데이터베이스 동기화|예||||||예|  
|Always On 장애 조치(failover) 클러스터 인스턴스|예<br /><br /> 운영 체제가 지원하는 최대 크기의 노드 수|예<br /><br /> 노드 2개 지원|||||예<br /><br /> 운영 체제가 지원하는 최대 크기의 노드 수|  
|프로그래밍 기능(AMO, ADOMD.Net, OLEDB, XML/A, ASSL, TMSL)|예|예|||||예|  
  
##  <a name="BIMD"></a> BI 의미 체계 모델(다차원)  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|반가산적 측정값|예|아니오 <sup>1</sup>|||||예|  
|계층 구조|예|예|||||예|  
|KPI|예|예|||||예|  
|큐브 뷰|예||||||예|  
|작업|예|예|||||예|  
|계정 인텔리전스|예|예|||||예|  
|시간 인텔리전스|예|예|||||예|  
|사용자 지정 롤업|예|예|||||예|  
|큐브 쓰기 저장(writeback)|예|예|||||예|  
|차원 쓰기 저장(Writeback)|예||||||예|  
|셀 쓰기 저장(writeback)|예|예|||||예|  
|드릴스루|예|예|||||예|  
|고급 계층 유형(부모-자식 및 비정형 계층 구조)|예|예|||||예|  
|고급 차원(참조 차원, 다 대 다 차원)|예|예|||||예|  
|연결된 측정값 및 차원|예|예 <sup>2</sup> |||||예|  
|번역|예|예|||||예|  
|Aggregations|예|예|||||예|  
|여러 파티션|예|예, 최대 3|||||예|  
|자동 관리 캐싱|예||||||예|  
|사용자 지정 어셈블리(저장 프로시저)|예|예|||||예|  
|MDX 쿼리 및 스크립트|예|예|||||예|  
|DAX 쿼리|예|예|||||예|  
|역할 기반 보안 모델|예|예|||||예|  
|차원 및 셀 수준 보안|예|예|||||예|  
|확장 가능 문자열 저장소|예|예|||||예|  
|MOLAP, ROLAP 및 HOLAP 저장소 모델|예|예|||||예|  
|이진 및 압축 XML 전송|예|예|||||예|  
|밀어넣기 모드 처리|예||||||예|  
|직접 쓰기 저장|예||||||예|  
|측정값 식|예||||||예|  
  
 <sup>1</sup> Standard Edition에서 LastChild 반가산적 측정값은 지원되지만 None, FirstChild, FirstNonEmpty, LastNonEmpty, AverageOfChildren 및 ByAccount와 같은 다른 반가산적 측정값은 지원되지 않습니다. Sum, Count, Min, Max와 같은 가산적 측정값과 비가산적 측정값(DistinctCount)은 모든 버전에서 지원됩니다.  
  <sup>2</sup> Standard Edition에서는 동일한 데이터베이스 내에서 측정값 및 차원 연결이 지원되지만 다른 데이터베이스 또는 인스턴스에서는 지원되지 않습니다.
   
##  <a name="BIT"></a> BI 의미 체계 모델(테이블 형식)  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|계층 구조|예|예|||||예|  
|KPI|예|예|||||예|  
|큐브 뷰|예||||||예|  
|번역|예|예|||||예|  
|DAX 계산, DAX 쿼리, MDX 쿼리|예|예|||||예|  
|행 수준 보안|예|예|||||예|  
|여러 파티션|예||||||예|  
|메모리 내 저장소 모드|예|예|||||예|  
|DirectQuery 저장소 모드|예||||||예|  
  
##  <a name="PPSP"></a> SharePoint용 PowerPivot  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|공유 서비스 아키텍처를 기반으로 하는 SharePoint 팜 통합|예||||||예|  
|사용 보고|예||||||예|  
|상태 모니터링 규칙|예||||||예|  
|파워 피벗 갤러리|예||||||예|  
|파워 피벗 데이터 새로 고침|예||||||예|  
|파워 피벗 데이터 피드|예||||||예|  
  
##  <a name="DM"></a> 데이터 마이닝  
  
|기능 이름|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|표준 알고리즘|예|예|||||예|  
|데이터 마이닝 도구(마법사, 편집기, 쿼리 작성기)|예|예|||||예|  
|교차 유효성 검사|예||||||예|  
|마이닝 구조 데이터의 필터링된 하위 집합에 대한 모델|예||||||예|  
|시계열: ARTXP 및 ARIMA 방식 간의 사용자 지정 혼합|예||||||예|  
|시계열: 새 데이터를 사용한 예측|예||||||예|  
|무제한 동시 DM 쿼리|예||||||예|  
|데이터 마이닝 알고리즘용 고급 구성 및 튜닝 옵션|예||||||예|  
|플러그 인 알고리즘 지원|예||||||예|  
|병렬 모델 처리|예||||||예|  
|시계열: 계열 간 예측|예||||||예|  
|연결 규칙에 대한 무제한 특성|예||||||예|  
|시퀀스 예측|예||||||예|  
|naïve Bayes, 신경망, 로지스틱 회귀 분석을 위한 다중 예측 대상|예||||||예|  
  
##  <a name="BIC"></a> Business Intelligence 클라이언트  
 Microsoft 다운로드 센터에서 제공하는 다음 소프트웨어 클라이언트 응용 프로그램을 사용하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에서 실행되는 비즈니스 인텔리전스 문서를 손쉽게 만들 수 있습니다. 이러한 문서를 서버 환경에서 호스트하려는 경우 해당 문서 유형을 지원하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전을 사용하세요. 다음 표에서는 이러한 클라이언트 응용 프로그램에서 만든 문서를 호스팅하는 데 필요한 서버 기능이 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전을 보여 줍니다.  
  
|도구 이름|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|---------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Excel 및 Visio 2010용 데이터 마이닝 추가 기능(.xlsx, .vsdx)|예|예|||||예|  
|[!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 2010 및 2013(.xlsx)|예||||||예|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] (.xlsx)|예||||||예|  
  
> [!NOTE]  
>  1.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 은 데이터 모델을 사용하여 통합 문서를 만들기 위한 Excel 추가 기능입니다.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 종속되지 않지만 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)]는 SharePoint의 데이터 모델을 사용하여 Excel 통합 문서를 공유하고 공동 작업하는 데 필요합니다. 이 기능은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition의 일부로 사용할 수 있습니다.  
>   
>      Excel 2016에는 파워 피벗 기능이 내장되어 있어 더 이상 파워 피벗 추가 기능은 필요하지 않습니다.  
> 2.  위의 표는 이러한 클라이언트 도구를 활성화하는 데 필요한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전을 식별하지만 이러한 도구는 모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전에서 호스트되는 데이터에 액세스할 수 있습니다.  
  
 ## 관련 항목:  
 [SQL Server 2016 버전에서 지원하는 기능](Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
 [SQL Server 2016 제품 사양](../Topic/Product%20Specifications%20for%20SQL%20Server%202016.md)   
 [SQL Server 2016 설치](../database-engine/install-windows/installation-for-sql-server-2016.md)  

