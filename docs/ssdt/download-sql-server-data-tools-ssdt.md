---
title: SSDT(SQL Server Data Tools) 다운로드 | Microsoft 문서
ms.custom: ''
ms.date: 06/04/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssdt
ms.reviewer: ''
ms.suite: sql
ms.technology: ssdt
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords:
- ssdt 설치, ssdt 다운로드, 최신 ssdt
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6794784b2339fe9c246dc4aec017e4e7cbb93311
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34773339"
---
# <a name="download-and-install-sql-server-data-tools-ssdt-for-visual-studio"></a>Visual Studio용 SSDT(SQL Server Data Tools) 다운로드 및 설치
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
**SQL Server Data Tools**는 SQL Server 관계형 데이터베이스, Azure SQL 데이터베이스, AS(Analysis Services) 데이터 모델, IS(Integration Services) 패키지 및 RS(Reporting Services) 보고서를 빌드하기 위한 최신형 개발 도구입니다. SSDT를 사용하면 Visual Studio에서 응용 프로그램을 개발할 때처럼 쉽게 SQL Server 콘텐츠 형식을 디자인 및 배포할 수 있습니다.

*대부분의 사용자의 경우 SSDT(SQL Server Data Tools)는 Visual Studio를 설치하는 동안 설치됩니다. Visual Studio 설치 관리자를 사용하여 SSDT를 설치하면 기본 SSDT 기능을 추가하므로 AS, IS 및 RS 도구를 가져오기 위해 [SSDT 독립 실행형 설치 관리자](#ssdt-for-vs-2017-standalone-installer)를 여전히 실행해야 합니다.*

## <a name="install-ssdt-with-visual-studio-2017"></a>Visual Studio 2017을 사용하여 SSDT 설치

[Visual Studio를 설치](https://docs.microsoft.com/visualstudio/install/install-visual-studio)하는 동안 SSDT를 설치하려면 **데이터 저장소 및 처리** 작업을 선택한 다음, **SQL Server Data Tools**를 선택합니다. Visual Studio가 이미 설치된 경우 [작업의 목록을 편집](https://docs.microsoft.com/visualstudio/install/modify-visual-studio)하여 SSDT: ![데이터 저장소 및 처리 작업](../ssdt/media/download-sql-server-data-tools-ssdt/data-workload.png)을 포함할 수 있습니다.



## <a name="install-analysis-services-integration-services-and-reporting-services-tools"></a>Analysis Services, Integration Services 및 Reporting Services 도구 설치
AS, IS 및 RS 프로젝트 지원을 설치하려면 [SSDT 독립 실행형 설치 관리자](#ssdt-for-vs-2017-standalone-installer)를 실행합니다. 

설치 관리자는 SSDT 도구를 추가할 사용 가능한 Visual Studio 인스턴스를 나열합니다. Visual Studio가 설치되지 않은 경우 **새 SQL Server Data Tools 인스턴스 설치**를 선택하면 최소 버전의 Visual Studio로 SSDT를 설치하지만 최상의 환경을 위해 [최신 버전의 Visual Studio](https://www.visualstudio.com/downloads)로 SSDT를 사용하는 것이 좋습니다. 

![AS, IS, RS 선택](../ssdt/media/download-sql-server-data-tools-ssdt/select-services.png)



## <a name="ssdt-for-vs-2017-standalone-installer"></a>VS 2017용 SSDT(독립 실행형 설치 관리자)

[![다운로드](../ssdt/media/download.png) Visual Studio 2017용 SSDT(15.7.0) 다운로드](https://go.microsoft.com/fwlink/?linkid=874716) 

> [!IMPORTANT]
> Visual Studio 2017용 SSDT(15.7.0)를 설치하기 전에 "Microsoft Analysis Services Projects" 및 "Microsoft Reporting Services Projects" 확장이 이미 설치되어 있는 경우 모두 제거하고, VS 인스턴스를 모두 닫습니다. 



**버전 정보**  
  
릴리스 번호: 15.7.0  
빌드 번호: 14.0.16165.0  
릴리스 날짜: 2018년 6월 1일  

전체 변경 내용 목록은 [변경 로그](changelog-for-sql-server-data-tools-ssdt.md)를 참조하세요.

Visual Studio 2017용 SSDT는 Visual Studio와 동일한 [시스템 요구 사항](https://docs.microsoft.com/visualstudio/productinfo/vs2017-system-requirements-vs)을 갖습니다.  

### <a name="available-languages---ssdt-for-vs-2017"></a>사용 가능한 언어 - VS 2017용 SSDT

이 **VS 2017용 SSDT** 릴리스는 다음 언어로 설치할 수 있습니다.  

[중국어(중국)]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x804) | 
[중국어(대만)]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x404) | 
[영어(미국)]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x409) | 
[프랑스어]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x40c)  
[독일어]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x407) | 
[이탈리아어]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x410) | 
[일본어]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x411) | 
[한국어]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x412) | 
[포르투갈어(브라질)]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x416) | 
[러시아어]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x419) | 
[스페인어]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x40a)  



## <a name="ssdt-for-vs-2015-standalone-installer"></a>VS 2015용 SSDT(독립 실행형 설치 관리자)

[![다운로드](../ssdt/media/download.png)Visual Studio 2015용 SSDT(17.4) 다운로드](https://go.microsoft.com/fwlink/?linkid=863440)

**버전 정보**  
  
릴리스 번호: 17.4

이 릴리스에 대한 빌드 번호: 14.0.61712.050
  
전체 변경 내용 목록은 [변경 로그](changelog-for-sql-server-data-tools-ssdt.md)를 참조하세요.

### <a name="available-languages---ssdt-for-vs-2015"></a>사용 가능한 언어 - VS 2015용 SSDT
  
이 **VS 2015용 SSDT** 릴리스는 다음 언어로 설치할 수 있습니다.  

[중국어(중국)]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x804) | 
[중국어(대만)]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x404) | 
[영어(미국)]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x409) | 
[프랑스어]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x40c)  
[독일어]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x407) | 
[이탈리아어]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x410) | 
[일본어]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x411) | 
[한국어]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x412) | 
[포르투갈어(브라질)]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x416) | 
[러시아어]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x419) | 
[스페인어]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x40a)  

### <a name="iso-images---ssdt-for-vs-2015"></a>ISO 이미지 - VS 2015용 SSDT

SSDT의 ISO 이미지를 사용해도 SSDT를 설치하거나 관리 설치 지점을 설정할 수 있습니다. ISO는 SSDT에 필요한 모든 구성 요소가 들어 있는 자체 포함된 파일이고 다시 시작 가능한 다운로드 관리자를 사용하여 다운로드할 수 있어 네트워크 대역폭이 제한되어 있거나 덜 안정적인 상황에 유용합니다. 다운로드가 완료된 다음 ISO를 드라이브로 탑재하거나 DVD로 구울 수 있습니다.

> [!NOTE]
> 지금 VS 2015 17.4용 SSDT의 ISO 이미지를 사용할 수 있습니다.

[중국어(중국)]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x804) |
[중국어(대만)]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x404) |
[영어(미국)]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x409) |
[프랑스어]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x40c)  
[독일어]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x407) |
[이탈리아어]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x410) |
[일본어]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x411) |
[한국어]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x412) |
[포르투갈어(브라질)]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x416) |
[러시아어]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x419) |
[스페인어]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x40a)



## <a name="supported-sql-versions"></a>지원되는 SQL 버전
  
|프로젝트 템플릿|지원 되는 SQL 플랫폼|  
|-------------------|--------------------|  
관계형 데이터베이스|  SQL Server 2005* - SQL Server 2017<br> (Visual Studio 2017에 대해 SSDT 17.x 또는 SSDT를 사용하여 [Linux의 SQL Server](../linux/sql-server-linux-overview.md)에 연결)<br /><br />Azure SQL 데이터베이스<br /><br />Azure SQL Data Warehouse(쿼리만 지원, 데이터베이스 프로젝트는 아직 지원되지 않음)<br /><br />  * SQL Server 2005는 더 이상 지원되지 않습니다.<br /><br /> 공식적으로 지원되는 SQL 버전으로 전환하세요.|
  |Analysis Services 모델<br /><br />Reporting Services 보고서 | SQL Server 2008 – SQL Server 2017|
  |Integration Services 패키지| SQL Server 2012 – SQL Server 2017    |
  
## <a name="dacfx"></a>DacFx
Visual Studio 2015용 SSDT 및 Visual Studio 2017용 SSDT는 모두 DacFx 17.4.1를 사용합니다. [DacFx(Data-Tier Application Framework) 17.4.1 다운로드](https://www.microsoft.com/download/details.aspx?id=56508)


## <a name="next-steps"></a>다음 단계  
SSDT를 설치한 후 데이터베이스, 패키지, 데이터 모델 및 SSDT를 사용하여 보고서를 만드는 방법에 알아보려면 이 자습서를 연습하세요.  

- [프로젝트 기반 오프라인 데이터베이스 개발](https://msdn.microsoft.com/library/hh272702(v=vs.103).aspx)  
- [SSIS 자습서: 간단한 ETL 패키지 만들기](../integration-services/ssis-how-to-create-an-etl-package.md)  
- [Analysis Services 자습서](../analysis-services/analysis-services-tutorials-ssas.md)  
- [기본 테이블 보고서 만들기(SSRS 자습서)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]


## <a name="see-also"></a>참고 항목  
[Visual Studio의 SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[SSDT MSDN 포럼](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT 팀 블로그](http://blogs.msdn.com/b/ssdt/)  
[SSDT 설명서](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[DACFx API 참조](https://msdn.microsoft.com/library/dn645454.aspx)  
[SSMS(SQL Server Management Studio) 다운로드](../ssms/download-sql-server-management-studio-ssms.md)  