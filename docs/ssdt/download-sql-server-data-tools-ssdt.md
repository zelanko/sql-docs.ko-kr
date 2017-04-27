---
title: "SSDT(SQL Server Data Tools) 다운로드 | Microsoft 문서"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "ssdt 설치, ssdt 다운로드, 최신 ssdt"
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 681ad2f6d7aeb88db45dde3f2e695db672b97dbd
ms.lasthandoff: 04/11/2017

---
# <a name="download-sql-server-data-tools-ssdt"></a>SSDT(SQL Server Data Tools) 다운로드

**[SQL Server Data Tools](https://msdn.microsoft.com/mt186501)**는 SQL Server 관계형 데이터베이스, Azure SQL 데이터베이스, Integration Services 패키지, Analysis Services 데이터 모델 및 Reporting Services 보고서를 빌드할 수 있는 최신형 개발 도구로, 무료로 다운로드할 수 있습니다. SSDT를 사용하면 Visual Studio에서 응용 프로그램을 개발할 때처럼 쉽게 SQL Server 콘텐츠 형식을 디자인 및 배포할 수 있습니다. 이 릴리스에서는 SQL Server 2016에서 SQL Server 2005까지 지원하며 SQL Server 2016의 새로운 기능을 추가하기 위한 디자인 환경을 제공합니다.  
    
    
| ![다운로드로 사용 가능한 제품 설명서에서 데이터 공급자 설치 섹션을 참조하세요](../ssdt/media/download.png) Visual Studio 2015용 SQL Server Data Tools 다운로드  | 데이터 계층 응용 프로그램 프레임워크(DacFx) 다운로드 ||
|:---|:---|:---|
|**[SQL Server Data Tools(16.5) 다운로드](https://msdn.microsoft.com/mt186501)**|[**DacFx 및 SqlPackage.exe(16.5) 다운로드**](https://www.microsoft.com/download/details.aspx?id=54106) |프로덕션 사용에 대한 현재 GA 릴리스.|
|[**SQL Server Data Tools - 릴리스 후보 다운로드**](../ssdt/sql-server-data-tools-ssdt-release-candidate.md)| [**DacFx 및 SqlPackage.exe - 릴리스 후보 다운로드**](../ssdt/sql-server-data-tools-ssdt-release-candidate.md) |SQL Server vNext에 대한 지원을 포함합니다.|



## <a name="download-visual-studio"></a>Visual Studio 다운로드

* [**Visual Studio Community 2015 다운로드**](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)

### <a name="use-ssdt-in-visual-studio-2017"></a>Visual Studio 2017에서 SSDT 사용

* [**Visual Studio 2017 다운로드**](https://www.visualstudio.com/) ([버전별 Visual Studio 2017 기능 비교](https://www.visualstudio.com/vs/compare/))

관계형 데이터베이스 프로젝트를 사용하려면 설치 중 **데이터 저장소 및 처리** 작업을 선택하는 것이 좋습니다. SSDT 데이터베이스 프로젝트 지원은 *Azure*, *ASP.Net 및 웹 개발* 및 *.NET Core 플랫폼 간 개발*을 비롯한 다른 여러 작업에도 포함되어 있습니다.

Visual Studio 2017에서 SSDT를 사용하는 경우 AS 및 RS 구성 요소를 설치하세요.
* [Analysis Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)
* [Reporting Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)


## <a name="installing-ssdt-without-visual-studio-pre-installed"></a>Visual Studio를 사전 설치하지 않고 SSDT 설치

컴퓨터에 Visual Studio를 설치하지 않은 경우 Visual Studio 2015용 SSDT를 설치하면 Visual Studio 2015의 최소 "통합 셸" 버전도 설치됩니다. 이 버전의 Visual Studio는 원하는 만큼 여러 대의 컴퓨터에서 무료로 설치하고 사용할 수 있습니다. 이 버전은 모든 SQL Server 프로젝트 형식과 더불어 SQL Server 개체 탐색기 및 기타 SQL 도구 환경도 제공합니다.

컴퓨터에 [Visual Studio 2015 Community Edition 이상](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)이 설치된 경우 SSDT를 설치하면 모든 SQL Server 도구가 기존 Visual Studio 설치에 추가됩니다. Visual Studio에는 원본 코드 제어 통합, SQL이 아닌 언어 지원 등과 같이 도움이 되는 여러 기능이 포함되어 있습니다. T-SQL을 개발할 때 최상의 환경을 이용하려면 Visual Studio 2015 Community 이상을 사용하는 것이 좋습니다.

## <a name="supported-sql-versions"></a>지원되는 SQL 버전
  
|프로젝트 템플릿|지원 되는 SQL 플랫폼|  
|-------------------|--------------------|  
관계형 데이터베이스|  SQL Server 2005* - SQL Server 2016 <br /><br />Azure SQL 데이터베이스<br /><br />Azure SQL Data Warehouse(쿼리만 지원, 데이터베이스 프로젝트는 아직 지원되지 않음)<br /><br />  * SQL Server 2005는 더 이상 지원되지 않습니다.<br /><br /> 공식적으로 지원되는 SQL 버전으로 전환하세요.|
  |Analysis Services 모델<br /><br />Reporting Services 보고서 | SQL Server 2008 – SQL Server 2016|
  |Integration Services 패키지| SQL Server 2012 – SQL Server 2016    |
  
## <a name="next-steps"></a>다음 단계  
SSDT를 설치한 후 데이터베이스, 패키지, 데이터 모델 및 SSDT를 사용하여 보고서를 만드는 방법에 알아보려면 이 자습서를 연습하세요.  
  
-   [프로젝트 기반 오프라인 데이터베이스 개발](https://msdn.microsoft.com/library/hh272702(v=vs.103).aspx)  
  
-   [SSIS 자습서: 간단한 ETL 패키지 만들기](https://msdn.microsoft.com/library/ms169917.aspx)  
  
-   [Analysis Services 자습서](https://msdn.microsoft.com/library/hh231701.aspx)  
  
-   [기본 테이블 보고서 만들기(SSRS 자습서)](https://msdn.microsoft.com/library/ms167305.aspx)  
  
## <a name="see-also"></a>참고 항목  
[Visual Studio의 SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[SSDT MSDN 포럼](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT 팀 블로그](http://blogs.msdn.com/b/ssdt/)  
[SSDT Connect 피드백](https://connect.microsoft.com/SQLServer/Feedback)  
[SSDT 설명서](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[DACFx API 참조](https://msdn.microsoft.com/library/dn645454.aspx)  
[SSMS(SQL Server Management Studio) 다운로드](../ssms/download-sql-server-management-studio-ssms.md)  

