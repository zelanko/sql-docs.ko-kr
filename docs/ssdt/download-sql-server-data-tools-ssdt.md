---
title: SSDT(SQL Server Data Tools) 다운로드 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssdt
ms.topic: conceptual
keywords:
- ssdt 설치, ssdt 다운로드, 최신 ssdt
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: d296a30e017172e1e753d6dbaaa065b0644792bb
ms.sourcegitcommit: 31c8f9eab00914e056e9219093dbed1b0b4542a6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2019
ms.locfileid: "55513943"
---
# <a name="download-and-install-sql-server-data-tools-ssdt-for-visual-studio"></a>Visual Studio용 SSDT(SQL Server Data Tools) 다운로드 및 설치

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

> [!div class="nextstepaction"]
> [SQL Docs 목차에 대한 피드백을 공유하세요!](https://aka.ms/sqldocsurvey)

**SQL Server Data Tools**는 SQL Server 관계형 데이터베이스, Azure SQL 데이터베이스, AS(Analysis Services) 데이터 모델, IS(Integration Services) 패키지 및 RS(Reporting Services) 보고서를 빌드하기 위한 최신형 개발 도구입니다. SSDT를 사용하면 Visual Studio에서 애플리케이션을 개발할 때처럼 쉽게 SQL Server 콘텐츠 형식을 디자인 및 배포할 수 있습니다.

*대부분의 사용자의 경우 SSDT(SQL Server Data Tools)는 Visual Studio를 설치하는 동안 설치됩니다. Visual Studio 설치 관리자를 사용하여 SSDT를 설치하면 기본 SSDT 기능을 추가하므로 AS, IS 및 RS 도구를 가져오기 위해 [SSDT 독립 실행형 설치 관리자](#ssdt-for-vs-2017-standalone-installer)를 여전히 실행해야 합니다.*

## <a name="install-ssdt-with-visual-studio-2017"></a>Visual Studio 2017을 사용하여 SSDT 설치

[Visual Studio를 설치](https://docs.microsoft.com/visualstudio/install/install-visual-studio)하는 동안 SSDT를 설치하려면 **데이터 스토리지 및 처리** 작업을 선택한 다음, **SQL Server Data Tools**를 선택합니다. Visual Studio가 이미 설치된 경우 [작업의 목록을 편집](https://docs.microsoft.com/visualstudio/install/modify-visual-studio)하여 SSDT: ![데이터 스토리지 및 처리 워크로드](../ssdt/media/download-sql-server-data-tools-ssdt/data-workload.png)를 포함할 수 있습니다.

## <a name="install-analysis-services-integration-services-and-reporting-services-tools"></a>Analysis Services, Integration Services 및 Reporting Services 도구 설치

AS, IS 및 RS 프로젝트 지원을 설치하려면 [SSDT 독립 실행형 설치 관리자](#ssdt-for-vs-2017-standalone-installer)를 실행합니다. 

설치 관리자는 SSDT 도구를 추가할 사용 가능한 Visual Studio 인스턴스를 나열합니다. Visual Studio가 설치되지 않은 경우 **새 SQL Server Data Tools 인스턴스 설치**를 선택하면 최소 버전의 Visual Studio로 SSDT를 설치하지만 최상의 환경을 위해 [최신 버전의 Visual Studio](https://www.visualstudio.com/downloads)로 SSDT를 사용하는 것이 좋습니다. 

![AS, IS, RS 선택](../ssdt/media/download-sql-server-data-tools-ssdt/select-services.png)



## <a name="ssdt-for-vs-2017-standalone-installer"></a>VS 2017용 SSDT(독립 실행형 설치 관리자)

[![다운로드](../ssdt/media/download.png) Visual Studio 2017용 SSDT(15.9.0) 다운로드](https://go.microsoft.com/fwlink/?linkid=2052454) 

> [!IMPORTANT]
> - Visual Studio 2017용 SSDT(15.9.0)를 설치하기 전에 *Analysis Services Projects* 및 *Reporting Services Projects* 확장이 이미 설치되어 있는 경우 모두 제거하고, VS 인스턴스를 모두 닫습니다.
> - 15.8.2 이후의 Visual Studio 2017용 SSDT는 Teradata 원본/대상이 포함된 패키지 디자인을 지원하지 않습니다. Visual Studio 2017용 SSDT(15.8)를 사용하세요.



**버전 정보**  
  
릴리스 번호: 15.9.0  
빌드 번호: 14.0.16186.0  
릴리스 날짜: 2019년 1월 28일  

전체 변경 내용 목록은 [변경 로그](changelog-for-sql-server-data-tools-ssdt.md)를 참조하세요.

Visual Studio 2017용 SSDT는 Visual Studio와 동일한 [시스템 요구 사항](https://docs.microsoft.com/visualstudio/productinfo/vs2017-system-requirements-vs)을 갖습니다.  

### <a name="available-languages---ssdt-for-vs-2017"></a>사용 가능한 언어 - VS 2017용 SSDT

이 **VS 2017용 SSDT** 릴리스는 다음 언어로 설치할 수 있습니다.

- [중국어(간체)]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x804)
- [중국어(번체)]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x404)
- [영어(미국)]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x409)
- [프랑스어]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x40c)
- [독일어]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x407)
- [이탈리아어]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x410)
- [일본어]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x411)
- [한국어]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x412)
- [포르투갈어(브라질)]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x416)
- [러시아어]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x419)
- [스페인어]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x40a)

## <a name="offline-install"></a>오프라인 설치

인터넷에 연결되어 있지 않은 경우 SSDT를 설치하려면 이 섹션의 단계를 따르세요. 자세한 내용은 [Visual Studio 2017의 네트워크 설치 만들기](https://docs.microsoft.com/visualstudio/install/create-a-network-installation-of-visual-studio)를 참조하세요.

먼저 온라인 상태에서 다음 단계를 완료하세요.

1. [SSDT 독립 실행형 설치 관리자를 다운로드](#ssdt-for-vs-2017-standalone-installer)합니다.
2. [vs_sql.exe를 다운로드](https://aka.ms/vs/15/release/vs_sql.exe)합니다.
3. 여전히 온라인 상태에서 다음 명령 중 하나를 실행하여 오프라인 설치에 필요한 모든 파일을 다운로드합니다. `--layout` 옵션을 사용하는 것이 핵심입니다. 오프라인 설치를 위한 실제 파일을 다운로드합니다. `<filepath>`를 파일을 저장할 실제 레이아웃 경로와 바꿉니다.

   
   1.   특정 언어의 경우 `vs_sql.exe --layout c:\<filepath> --lang en-us` 로캘을 전달합니다(단일 언어는 1GB 이하).  
   2. 모든 언어의 경우 `--lang` 인수를 생략한 `vs_sql.exe --layout c:\<filepath>` 형태를 사용합니다(모든 언어는 3.9GB 이하).

4. `SSDT-Setup-ENU.exe /layout c:\<filepath>`를 실행하여 VS2017 파일이 다운로드된 동일한 `<filepath>` 위치로 SSDT 페이로드를 추출합니다. 이렇게 하면 두 폴더의 모든 파일이 단일 레이아웃 폴더에 결합됩니다.

이전 단계를 완료한 후 오프라인 상태에서 다음 작업을 완료할 수 있습니다.

1. `vs_setup.exe --NoWeb`을 실행하여 VS2017 Shell 및 SQL Server Data Project를 설치합니다.
2. 레이아웃 폴더에서 `SSDT-Setup-ENU.exe /install`을 실행하고 SSIS/SSRS/SSAS를 선택합니다.

   - 무인 설치의 경우 `SSDT-Setup-ENU.exe /INSTALLALL[:vsinstances] /passive`를 실행합니다.  

사용 가능한 옵션을 보려면 `SSDT-Setup-ENU.exe /help`를 실행하세요.

> [!NOTE]
> Visual Studio 2017 전체 버전을 사용하는 경우 SSDT 전용 오프라인 폴더를 만들고 새로 생성된 이 폴더에서 `SSDT-Setup-ENU.exe`를 실행합니다(다른 Visual Studio 2017 오프라인 레이아웃에 SSDT를 추가 안 함). 기존 Visual Studio 오프라인 레이아웃에 SSDT 레이아웃을 추가하면 필요한 런타임(.exe) 구성 요소가 만들어지지 않습니다.

## <a name="supported-sql-versions"></a>지원되는 SQL 버전
  
|프로젝트 템플릿|지원 되는 SQL 플랫폼|  
|-------------------|--------------------|  
|관계형 데이터베이스|  SQL Server 2005\* - SQL Server 2017<br> (Visual Studio 2017에 대해 SSDT 17.x 또는 SSDT를 사용하여 [Linux의 SQL Server](../linux/sql-server-linux-overview.md)에 연결)<br /><br />Azure SQL 데이터베이스<br /><br />Azure SQL Data Warehouse(쿼리만 지원, 데이터베이스 프로젝트는 아직 지원되지 않음)<br /><br /> \* SQL Server 2005는 더 이상 지원되지 않습니다.<br /><br /> 공식적으로 지원되는 SQL 버전으로 전환하세요.|
|Analysis Services 모델<br /><br />Reporting Services 보고서 | SQL Server 2008 - SQL Server 2017|
|Integration Services 패키지| SQL Server 2012 - SQL Server 2019 |
  
## <a name="dacfx"></a>DacFx

Visual Studio 2015용 SSDT 및 Visual Studio 2017용 SSDT는 모두 DacFx 17.4.1을 사용합니다. [데이터 계층 애플리케이션 프레임워크(DacFx) 17.4.1](https://www.microsoft.com/download/details.aspx?id=56508).

## <a name="previous-versions"></a>이전 버전

Visual Studio 2015용 SSDT 또는 SSDT의 이전 버전을 다운로드하고 설치하려면 [SQL Server Data Tools의 이전 릴리스(SSDT 및 SSDT-BI)](previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

SSDT를 설치한 후 데이터베이스, 패키지, 데이터 모델 및 SSDT를 사용하여 보고서를 만드는 방법에 알아보려면 이 자습서를 연습하세요.  

- [프로젝트 기반 오프라인 데이터베이스 개발](project-oriented-offline-database-development.md)  
- [SSIS 자습서: 간단한 ETL 패키지 만들기](../integration-services/ssis-how-to-create-an-etl-package.md)  
- [Analysis Services 자습서](../analysis-services/analysis-services-tutorials-ssas.md)  
- [기본 테이블 보고서 만들기(SSRS 자습서)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

## <a name="see-also"></a>참고 항목

[SSDT MSDN 포럼](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT 팀 블로그](https://blogs.msdn.com/b/ssdt/)  
[DACFx API 참조](https://msdn.microsoft.com/library/dn645454.aspx)  
[SSMS(SQL Server Management Studio) 다운로드](../ssms/download-sql-server-management-studio-ssms.md)  
