---
title: Analysis Services 연결에 사용 되는 데이터 공급자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 128f6dde-409d-4c12-9820-3305bab57b75
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 16e691ab6c6a6fcff4cb59fe54884fbb1b52268e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080095"
---
# <a name="data-providers-used-for-analysis-services-connections"></a>Analysis Services 연결에 사용되는 데이터 공급자
  Analysis Services는 서버 및 데이터 액세스를 위해 세 가지 데이터 공급자를 제공합니다. Analysis Services에 연결하는 모든 애플리케이션은 이러한 공급자 중 하나를 사용하여 서버 및 데이터 액세스를 수행합니다. 그중에서 ADOMD.NET 및 AMO(Analysis Services Management Objects) 공급자는 관리되는 데이터 공급자이며, Analysis Services OLE DB 공급자(MSOLAP DLL)는 네이티브 데이터 공급자입니다.  
  
 여러 버전의 Analysis Services를 실행하는 조직에서는 Analysis Services 데이터에 연결하는 사용자 워크스테이션에 최신 버전의 데이터 공급자를 설치해야 할 수 있습니다. 최신 버전의 Analysis Services에 연결하려면 동일한 주요 릴리스의 데이터 공급자가 필요합니다. 예를 들어 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]에 연결하려면 각 워크스테이션에 2014 릴리스의 데이터 공급자가 있어야 합니다. Excel에서는 연결하는 데 필요한 데이터 공급자를 설치하지만 사용하고 있는 Analysis Services 인스턴스 비해 해당 공급자가 오래되었을 수 있습니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
 [서버 버전을 확인하는 방법](#bkmk_ServVers)  
  
 [Analysis Services 데이터 공급자의 버전을 확인하는 방법](#bkmk_LibUpdate)  
  
 [최신 버전의 데이터 공급자를 얻는 위치](#bkmk_downloadsite)  
  
 [Analysis Services OLE DB 공급자](#bkmk_OLE)  
  
 [ADOMD.NET](#bkmk_ADOMD)  
  
 [AMO](#blkmk_AMO)  
  
##  <a name="bkmk_ServVers"></a> 서버 버전을 확인하는 방법  
 Analysis Services 인스턴스의 버전을 알고 있으면 조직에서 워크스테이션에 최신 버전의 데이터 공급자를 설치해야 하는지 여부를 확인하는 데 도움이 됩니다.  
  
-   SQL Server Management Studio에서 Analysis Services 인스턴스에 연결합니다. 확인, 가리킨 하려는 인스턴스를 마우스 오른쪽 단추로 클릭 **보고서**, 클릭 **일반**합니다. 에디션 및 버전 빌드 정보가 보고서에 나타납니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 의 최초 릴리스에 대한 주 빌드 번호는 12.0.2000.9입니다.  
  
 버전 및 빌드 정보를 얻는 방법은 [SQL Server 및 해당 구성 요소의 버전 및 에디션을 확인하는 방법](https://support.microsoft.com/kb/321185)을 참조하십시오.  
  
##  <a name="bkmk_LibUpdate"></a> Analysis Services 데이터 공급자의 버전을 확인하는 방법  
 데이터 공급자는 Analysis Services와 함께 설치될 뿐 아니라 Excel과 같은 Analysis Services 데이터베이스에 정기적으로 연결하는 클라이언트 애플리케이션에 의해서도 설치됩니다.  
  
 Office 2007은 SQL Server 2005의 데이터 공급자를 설치합니다. Office 2010은 SQL Server 2008의 데이터 공급자를 설치합니다. Office 2013은 SQL Server 2012의 데이터 공급자를 설치합니다. 여러 버전의 Office 또는 SQL Server를 사용하고 있는 경우 연결 또는 기능 가용성이 기대와 다르면 최신 버전의 데이터 공급자를 설치해야 할 수도 있습니다. 동일한 컴퓨터에서 각 데이터 공급자의 여러 주 버전을 함께 실행할 수 있습니다.  
  
#### <a name="find-the-file-version-of-the-oledb-provider"></a>OLEDB 공급자의 파일 버전 찾기  
  
1.  \Program Files\Microsoft Analysis Services\AS OLEDB\120으로 이동합니다.  
  
2.  Msolap120.dll을 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다.  
  
 이 위치에서 파일을 찾을 수 없거나 폴더 경로에 AS OLEDB\110 또는 AS OLEDB\90이 포함되어 있는 경우 이전 라이브러리를 사용하고 있는 것이며 이제 최신 버전(AS OLEDB\11)을 설치하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에 연결해야 합니다.  
  
#### <a name="find-the-file-version-of-adomdnet-and-amo"></a>ADOMD.NET 및 AMO의 파일 버전 찾기  
  
1.  C:\Windows\Assembly로 이동합니다.  
  
2.  Microsoft.AnalysisServices.AdomdClient를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다. **버전**을 클릭합니다.  
  
     AMO의 경우 Microsoft.AnalysisServices를 마우스 오른쪽 단추로 클릭합니다.  
  
 릴리스별 버전 및 빌드 번호에 대한 자세한 내용은 [Blogspot의 SQL Server 빌드](http://sqlserverbuilds.blogspot.com)를 참조하십시오.  
  
##  <a name="bkmk_downloadsite"></a> 최신 버전의 데이터 공급자를 얻는 위치  
 클라이언트 컴퓨터에 설치된 버전은 데이터를 제공하는 서버의 주 버전과 일치해야 합니다. 서버 설치가 네트워크에서 워크스테이션에 설치된 데이터 공급자보다 최신인 경우 최신 라이브러리를 설치해야 할 수 있습니다.  
  
#### <a name="find-the-data-providers-on-the-download-site"></a>다운로드 사이트에서 데이터 공급자 찾기  
  
1.  [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/p/?LinkID=296473)로 이동합니다.  
  
2.  **설치 지침**을 확장합니다.  
  
3.  Analysis Services 구성 요소가 포함된 섹션으로 스크롤합니다. ADOMD.NET, OLE DB 공급자 및 AMO는 목록에서 두 번째, 세 번째, 네 번째에 있습니다. 각 라이브러리는 32비트 또는 64비트 버전에서 사용할 수 있습니다. 64비트 운영 체제를 실행하는 서버와 최신 워크스테이션에는 64비트 버전이 필요합니다.  
  
##  <a name="bkmk_OLE"></a> Analysis Services OLE DB 공급자  
 Analysis Services OLE DB 공급자는 Analysis Services 데이터베이스 연결에 대한 기본 공급자입니다. MSOLAP는 ADOMD.NET과 AMO에서 간접적으로 사용되어 연결 요청을 데이터 공급자에 위임합니다. 또한 애플리케이션 코드에서 OLE DB 공급자를 직접 호출할 수도 있습니다. 솔루션 요구 사항에서 관리되는 API의 사용을 배제하는 경우 이렇게 할 수 있습니다.  
  
 Analysis Services OLE DB 공급자는 SQL Server 설치, Excel 및 Analysis Services 데이터베이스에 액세스하는 데 자주 사용되는 기타 애플리케이션에 의해 자동으로 설치됩니다. 다운로드 센터에서 다운로드하여 수동으로 설치할 수도 있습니다. 기본적으로 공급자는 \Program Files\Microsoft Analysis Services 폴더에서 찾을 수 있습니다. 공급자는 Analysis Services 데이터에 액세스하는 데 사용되는 모든 워크스테이션에 설치되어야 합니다.  
  
 MSOLAP130.dll은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에 기본 제공되는 Analysis Services OLE DB 공급자 버전입니다. 기타 이전 최신 버전에는 MSOLAP10.dll(SQL Server 2008 및 2008 R2의 경우) 및 MSOLAP90.dll(SQL Server 2005의 경우)이 포함됩니다.  
  
 OLE DB 공급자는 종종 연결 문자열에 지정됩니다. Analysis Services 연결 문자열을 다른 명명법을 사용 하 여 OLE DB 공급자를 참조 하세요. MSOLAP입니다. \<버전 >.dll  
  
 MSOLAP.5.dll은 Excel 2013과 함께 설치된 최신 Analysis Services OLE DB 공급자입니다. MSOLAP.4.dll 또는 MSOLAP.3.dll과 같은 이전 버전은 이전 버전의 Excel을 실행하는 워크스테이션에서 흔히 발견됩니다. PowerPivot 추가 기능과 같은 일부 Analysis Services 기능에는 특정 버전의 OLE DB 공급자가 필요합니다. 자세한 내용은 [연결 문자열 속성&#40;Analysis Services&#41;](connection-string-properties-analysis-services.md)을 참조하세요.  
  
##  <a name="bkmk_ADOMD"></a> ADOMD.NET  
 ADOMD.NET은 Analysis Services 데이터를 쿼리하는 데 사용되는 관리되는 데이터 공급자입니다. Excel에서는 특정 Analysis Services 큐브에 연결할 때 ADOMD.NET을 사용합니다. Excel에서 표시되는 연결 문자열은 ADOMD.NET 연결용입니다.  
  
 ADOMD.NET은 SQL Server 설치 프로그램으로 설치되며 SQL Server 클라이언트 애플리케이션에서 Analysis Services에 연결하는 데 사용됩니다. Office는 이 라이브러리를 설치하여 Excel에서 데이터 연결을 지원합니다. SQL Server에 포함된 다른 데이터 공급자와 마찬가지로 사용자 지정 코드에서 라이브러리를 사용할 경우 ADOMD.NET을 재배포할 수 있습니다. 또한 다운로드하고 수동으로 설치하여 최신 버전을 가져올 수 있습니다(이 항목의 [Analysis Services 데이터 공급자의 버전을 확인하는 방법](#bkmk_LibUpdate) 참조).  
  
 파일 버전 정보를 확인하려면 `Microsoft.AnalysisServices.AdomdClient`로 나열된 전역 어셈블리 캐시에서 ADOMD.NET을 찾으십시오.  
  
 데이터베이스에 연결할 때 세 가지 라이브러리에 대한 연결 문자열 속성은 모두 대개 동일합니다. ADOMD.NET에 대해 정의하는 거의 모든 연결 문자열(<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>)이 AMO 및 Analysis Services OLE DB 공급자에 대해서도 작동합니다. 자세한 내용은 [연결 문자열 속성&#40;Analysis Services&#41;](connection-string-properties-analysis-services.md)을 참조하세요.  
  
 프로그래밍 방식 연결에 대한 자세한 내용은 [Establishing Connections in ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-client/connections-in-adomd-net)을 참조하십시오.  
  
##  <a name="blkmk_AMO"></a> AMO  
 AMO는 서버 관리와 데이터 정의에 사용되는 관리되는 데이터 공급자입니다. 예를 들어 SQL Server Management Studio는 AMO를 사용하여 Analysis Services에 연결합니다.  
  
 AMO는 SQL Server 설치 프로그램으로 설치되며 SQL Server 클라이언트 애플리케이션에서 Analysis Services에 연결하는 데 사용됩니다. 또한 AMO를 사용자 지정 코드에서 사용하는 경우 다운로드하고 수동으로 설치할 수 있습니다(이 항목의 [Analysis Services 데이터 공급자의 버전을 확인하는 방법](#bkmk_LibUpdate) 참조). 전역 어셈블리 캐시에서 `Microsoft.AnalysisServices`로 AMO를 찾을 수 있습니다.  
  
 AMO를 사용 하 여 연결이 일반적으로 아주 적으며 "데이터 원본 =\<서버 이름 >"입니다. 연결이 설정된 후에는 API를 사용하여 데이터베이스 컬렉션 및 주요 개체로 작업합니다. SSDT와 SSMS는 AMO를 사용하여 Analysis Services 인스턴스에 연결합니다.  
  
 프로그래밍 방식 연결에 대한 자세한 내용은 [Programming AMO Fundamental Objects](https://docs.microsoft.com/bi-reference/amo/programming-amo-fundamental-objects)을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services에 연결](connect-to-analysis-services.md)  
  
  
