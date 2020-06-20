---
title: Analysis Services |에서 사용 되는 도구 및 응용 프로그램 Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0ddb3b7a-7464-4d04-8659-11cb2e4cf3c3
author: minewiskan
ms.author: owend
ms.openlocfilehash: 13da2ecc244c1596789a1d816bac81a13bcd4c62
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938334"
---
# <a name="tools-and-applications-used-in-analysis-services"></a>Analysis Services에서 사용되는 도구 및 애플리케이션
  Analysis Services 모델을 개발하고 Analysis Services 인스턴스에서 연결된 데이터베이스를 관리하기 위해 필요한 도구 및 애플리케이션을 찾으세요.

## <a name="analysis-services-model-designers"></a>Analysis Services 모델 디자이너
 테이블 형식 및 다차원 모델은 Visual Studio 셸에서 작성된 솔루션의 프로젝트 템플릿에서 생성됩니다. 프로젝트 템플릿은 Analysis Services 솔루션을 구성하는 모델, 큐브, 차원 및 역할을 만들기 위해 디자이너를 제공합니다.

### <a name="download-sql-server-data-tools-for-business-intelligence-ssdt-bi"></a>SQL Server Data Tools for Business Intelligence(SSDT-BI) 다운로드
 이전에는 BIDS(Business Intelligence Development Studio)라고 하던 SSDT-BI([!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] for Business Intelligence)는 Analysis Services 모델, Reporting Services 보고서 및 Integration Services 패키지를 만드는 데 사용됩니다. 다음 위치에서 SSDT-BI를 다운로드할 수 있습니다.

-   [Visual Studio 2013용 SSDT-BI 다운로드](https://go.microsoft.com/fwlink/p/?LinkId=396526)

-   [Visual Studio 2012용 SSDT-BI 다운로드](https://go.microsoft.com/fwlink/p/?LinkID=273673)

 이전 버전의 SSDT-BI 또는 BIDS가 컴퓨터에 설치되어 있는 경우 최신 버전이 이전 버전과 함께 설치됩니다. 특정 버전의 서버에 연결된 프로젝트 및 솔루션을 수정할 수 있도록 하기 위해 최신 및 이전 버전의 디자인 도구를 단일 워크스테이션에서 실행하는 것이 일반적입니다.

> [!NOTE]
>  Visual Studio 2012 및 Visual Studio 2013 버전의 SSDT를 다운로드할 수 있는 몇몇 사이트가 있습니다. 대부분의 다운로드에는 BI 프로젝트 템플릿이 포함되어 있지 않습니다. 위의 링크를 사용하면 올바른 버전을 얻을 수 있습니다. 비즈니스 인텔리전스 프로젝트 템플릿 폴더가 표시 되는 경우 올바른 버전의 SSDT가 있는 것을 알 수 있습니다. 이 폴더에는 Analysis Services, Reporting Services 및 Integration Services의 프로젝트 템플릿이 포함되어 있습니다. SSDT-BI를 설치한 방법에 따라 SQL Server 데이터베이스의 추가 프로젝트 템플릿이 표시될 수도 있습니다.

 ![SSDT의 새 프로젝트 템플릿](media/ssdt-biprojects.png "SSDT의 새 프로젝트 템플릿")

## <a name="administrative-tools"></a>관리 도구

### <a name="sql-server-management-studio"></a>SQL Server Management Studio
 Management Studio는 Analysis Services를 비롯하여 모든 SQL Server 기능의 기본 관리 도구입니다. SQL Server Management Studio는 선택적 구성 요소입니다. Windows Server 2012의 앱 페이지에서 다른 SQL Server 애플리케이션에 표시되지 않는 경우 SQL Server 설치 프로그램을 실행하여 설치에 추가합니다.

### <a name="sql-server-profiler"></a>SQL Server Profiler
 공식적으로는 더 이상 사용되지 않는 SQL Server Profiler를 통해 연결, MDX 쿼리 실행 및 기타 서버 작동을 간편하게 모니터링할 수 있습니다. SQL Server Profiler는 기본적으로 설치됩니다. Windows Server 2012의 앱에서 SQL Server 애플리케이션과 함께 찾을 수 있습니다.

### <a name="powershell"></a>PowerShell
 PowerShell 명령을 사용하여 많은 관리 작업을 수행할 수 있습니다. 자세한 내용은 [Analysis Services PowerShell](analysis-services-powershell.md) 을 참조하세요.

### <a name="community-and-third-party-tools"></a>커뮤니티 및 타사 도구
 커뮤니티 코드 샘플은 [Analysis Services codeplex 페이지](https://sqlsrvanalysissrvcs.codeplex.com/) (영문)를 참조하세요. [포럼](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlanalysisservices) 은 Analysis Services를 지 원하는 타사 도구에 대 한 권장 사항을 검색할 때 유용할 수 있습니다.
