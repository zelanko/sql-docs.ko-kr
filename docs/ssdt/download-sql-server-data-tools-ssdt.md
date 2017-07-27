---
title: "SSDT(SQL Server Data Tools) 다운로드 | Microsoft 문서"
ms.custom: 
ms.date: 05/18/2017
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
ms.translationtype: Human Translation
ms.sourcegitcommit: 5bd0e1d3955d898824d285d28979089e2de6f322
ms.openlocfilehash: 7aaa4c48419bf24357b2bef95c40d721d1ab2f2a
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="download-sql-server-data-tools-ssdt"></a>SSDT(SQL Server Data Tools) 다운로드

**[SQL Server Data Tools](https://msdn.microsoft.com/mt186501)**는 SQL Server 관계형 데이터베이스, Azure SQL 데이터베이스, Integration Services 패키지, Analysis Services 데이터 모델 및 Reporting Services 보고서를 빌드할 수 있는 최신형 개발 도구로, 무료로 다운로드할 수 있습니다. SSDT를 사용하면 Visual Studio에서 응용 프로그램을 개발할 때처럼 쉽게 SQL Server 콘텐츠 형식을 디자인 및 배포할 수 있습니다. 이 릴리스에서는 SQL Server 2017에서 SQL Server 2005까지 지원하며 SQL Server 2016의 새로운 기능을 추가하기 위한 디자인 환경을 제공합니다.  
    
    
![다운로드](../ssdt/media/download.png) [Visual Studio 2015용 SQL Server Data Tools 17.1 다운로드](https://go.microsoft.com/fwlink/?linkid=849393)

![다운로드](../ssdt/media/download.png) [데이터 계층 응용 프로그램 프레임워크(DacFx) 17.1 다운로드](https://www.microsoft.com/download/details.aspx?id=55255)

## <a name="sql-server-data-tools"></a>SQL Server Data Tools   
**버전 정보**  
  
릴리스 번호: 17.1  
이 릴리스에 대한 빌드 번호: 14.0.61705.170
  
 **새로운 기능**
 - AS 비모델 관련 IntelliSense에 대한 오프라인 지원(예: 강조 표시, 문 완성 및 매개 변수 정보)
 - M 식을 표시하기 위해 테이블 형식 모델 탐색기에 추가된 사항
 - 테이블 형식 모델의 역할 멤버를 구성하기 위한 Azure Active Directory 사용자 선택기
 - 1400 모델을 정의할 때 UI에서 힌트 인코딩 지원
 - AS 프로젝트 버그에 대한 여러 수정 사항
 - DacFx 버그에 대한 여러 수정 사항

 **알려진 문제**
 - 1400 호환성 수준 AS 모델에서 새 데이터 원본을 만들 때 파일 기반 데이터 원본을 선택한 다음 [취소]를 눌러 취소한 후에 데이터 원본을 만드는 경우 테이블 형식 편집기(Model.bim)가 읽기 전용이 됩니다. 단지 테이블 형식 편집기를 닫았다가 솔루션 탐색기에서 다시 열면 이 문제를 방지할 수 있습니다.

[changelog](changelog-for-sql-server-data-tools-ssdt.md)에서 사용 가능한 변경 내용의 전체 목록

 > Visual Studio 2017에서 SQL Server Data Tools를 사용하려면 아래의 [이](#use-ssdt-in-visual-studio-2017) 섹션을 참조하세요.

  **사용 가능한 언어**  
  
 이 SSDT 릴리스는 다음 언어로 설치할 수 있습니다.  
[중국어(중국)]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x804) | 
[중국어(대만)]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x404) | 
[영어(미국)]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x409) | 
[프랑스어]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x40c)  
[독일어]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x407) | 
[이탈리아어]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x410) | 
[일본어]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x411) | 
[한국어]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x412) | 
[포르투갈어(브라질)]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x416) | 
[러시아어]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x419) | 
[스페인어]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x40a)  

**ISO 이미지**

SSDT의 ISO 이미지를 사용해도 SSDT를 설치하거나 관리 설치 지점을 설정할 수 있습니다. ISO는 SSDT에 필요한 모든 구성 요소가 들어 있는 자체 포함된 파일이고 다시 시작 가능한 다운로드 관리자를 사용하여 다운로드할 수 있어 네트워크 대역폭이 제한되어 있거나 덜 안정적인 상황에 유용합니다. 다운로드가 완료된 다음 ISO를 드라이브로 탑재하거나 DVD로 구울 수 있습니다.

[중국어(중국)]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x804) |
[중국어(대만)]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x404) |
[영어(미국)]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x409) |
[프랑스어]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x40c)  
[독일어]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x407) |
[이탈리아어]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x410) |
[일본어]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x411) |
[한국어]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x412) |
[포르투갈어(브라질)]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x416) |
[러시아어]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x419) |
[스페인어]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x40a)

## <a name="download-visual-studio"></a>Visual Studio 다운로드

* [**Visual Studio Community 2015 다운로드**](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)

## <a name="installing-ssdt-without-visual-studio-pre-installed"></a>Visual Studio를 사전 설치하지 않고 SSDT 설치

컴퓨터에 Visual Studio를 설치하지 않은 경우 Visual Studio 2015용 SSDT를 설치하면 Visual Studio 2015의 최소 "통합 셸" 버전도 설치됩니다. 이 버전의 Visual Studio는 원하는 만큼 여러 대의 컴퓨터에서 무료로 설치하고 사용할 수 있습니다. 이 버전은 모든 SQL Server 프로젝트 형식과 더불어 SQL Server 개체 탐색기 및 기타 SQL 도구 환경도 제공합니다.

컴퓨터에 [Visual Studio 2015 Community Edition 이상](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)이 설치된 경우 SSDT를 설치하면 모든 SQL Server 도구가 기존 Visual Studio 설치에 추가됩니다. Visual Studio에는 원본 코드 제어 통합, SQL이 아닌 언어 지원 등과 같이 도움이 되는 여러 기능이 포함되어 있습니다. T-SQL을 개발할 때 최상의 환경을 이용하려면 Visual Studio 2015 Community 이상을 사용하는 것이 좋습니다.

## <a name="supported-sql-versions"></a>지원되는 SQL 버전
  
|프로젝트 템플릿|지원 되는 SQL 플랫폼|  
|-------------------|--------------------|  
관계형 데이터베이스|  SQL Server 2005* - SQL Server 2017 <br /><br />Azure SQL 데이터베이스<br /><br />Azure SQL Data Warehouse(쿼리만 지원, 데이터베이스 프로젝트는 아직 지원되지 않음)<br /><br />  * SQL Server 2005는 더 이상 지원되지 않습니다.<br /><br /> 공식적으로 지원되는 SQL 버전으로 전환하세요.|
  |Analysis Services 모델<br /><br />Reporting Services 보고서 | SQL Server 2008 – SQL Server 2017|
  |Integration Services 패키지| SQL Server 2012 – SQL Server 2017    |
  
## <a name="next-steps"></a>다음 단계  
SSDT를 설치한 후 데이터베이스, 패키지, 데이터 모델 및 SSDT를 사용하여 보고서를 만드는 방법에 알아보려면 이 자습서를 연습하세요.  
  
-   [프로젝트 기반 오프라인 데이터베이스 개발](https://msdn.microsoft.com/library/hh272702(v=vs.103).aspx)  
  
-   [SSIS 자습서: 간단한 ETL 패키지 만들기](https://msdn.microsoft.com/library/ms169917.aspx)  
  
-   [Analysis Services 자습서](https://msdn.microsoft.com/library/hh231701.aspx)  
  
-   [기본 테이블 보고서 만들기(SSRS 자습서)](https://msdn.microsoft.com/library/ms167305.aspx)  
  
## <a name="use-ssdt-in-visual-studio-2017"></a>Visual Studio 2017에서 SSDT 사용 

* [**Visual Studio 2017 다운로드**](https://www.visualstudio.com/) ([버전별 Visual Studio 2017 기능 비교](https://www.visualstudio.com/vs/compare/))

관계형 데이터베이스 프로젝트를 사용하려면 설치 중 **데이터 저장소 및 처리** 작업을 선택하는 것이 좋습니다. SSDT 데이터베이스 프로젝트 지원은 *Azure*, *ASP.Net 및 웹 개발* 및 *.NET Core 플랫폼 간 개발*을 비롯한 다른 여러 작업에도 포함되어 있습니다.

> [!NOTE]
> Visual Studio 2017의 SSDT 데이터베이스 프로젝트는 현재 SQL Server 2016까지 지원합니다.  SQL Server 2017에 대한 지원은 Visual Studio 2017 업데이트에서 곧 제공될 예정입니다.

Visual Studio 2017에서 SSDT를 사용하는 경우 AS 및 RS 구성 요소를 설치하세요.
* [Analysis Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)
* [Reporting Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)


## <a name="see-also"></a>관련 항목:  
[Visual Studio의 SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[SSDT MSDN 포럼](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT 팀 블로그](http://blogs.msdn.com/b/ssdt/)  
[SSDT Connect 피드백](https://connect.microsoft.com/SQLServer/Feedback)  
[SSDT 설명서](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[DACFx API 참조](https://msdn.microsoft.com/library/dn645454.aspx)  
[SSMS(SQL Server Management Studio) 다운로드](../ssms/download-sql-server-management-studio-ssms.md)  

