---
title: 구성 및 SharePoint 로그 파일과 진단 로깅 (SharePoint 용 PowerPivot) 보기 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 85f62d29-cdc6-45b3-be1f-ff1182939858
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6196466246529521f356c193c3e8cc0ee688c197
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53354700"
---
# <a name="configure-and-view-sharepoint-log-files--and-diagnostic-logging-powerpivot-for-sharepoint"></a>Configure and View SharePoint Log Files  and Diagnostic Logging (PowerPivot for SharePoint)
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버 작업, 이벤트 및 메시지가 SharePoint 로그 파일에 기록됩니다. 로깅 수준을 구성하고 로그 파일 정보를 보려면 이 항목의 정보를 사용합니다. 파일에 기록되는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버 이벤트를 제어할 수 있습니다. 또한 기록되는 메시지의 심각도를 제어할 수 있습니다. 자세한 내용은 [에 대 한 사용 현황 데이터 수집 구성 &#40;SharePoint 용 PowerPivot](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)합니다.  
  
 항목 내용  
  
-   [로그 파일 위치](#bkmk_filelocation)  
  
-   [개별 이벤트 범주에 대한 진단 로깅 수준 수정](#bkmk_modifyloglevels)  
  
-   [SharePoint 로그 파일을 보는 방법](#bkmk_how2viewlogfiles)  
  
##  <a name="bkmk_filelocation"></a> 로그 파일 위치  
 기본적으로 SharePoint 로그 파일은 다음 위치에 저장됩니다.  
  
 `C:\Program files\Common Files\Microsoft Shared\Web Server Extensions\14\LOGS`  
  
 LOGS 폴더에는 로그 파일(`.log`), 데이터 파일(`.txt`) 및 사용 파일(`.usage`)이 포함되어 있습니다. 파일 명명 규칙에 따라 서버 이름과 날짜 및 타임스탬프가 순서대로 결합되어 SharePoint 추적 로그의 이름이 지정됩니다. SharePoint 추적 로그는 IISRESET이 있을 때마다 정기적으로 만들어집니다. 일반적으로 24시간 내에 많은 추적 로그가 생성됩니다.  
  
##  <a name="bkmk_modifyloglevels"></a> 개별 이벤트 범주에 대한 진단 로깅 수준 수정  
 기본적으로 PowerPivot 이벤트의 ULS 로깅은 *보통*으로 설정됩니다. 이 설정은 SQL Server 2012에서 새로 포함된 설정입니다. 이전 릴리스에서 서버를 업그레이드한 경우 로깅 수준이 SQL Server 2008 R2의 기본 수준인 *자세히*로 설정될 수 있습니다. PowerPivot 서버 사용 정보에 대한 ULS 로그를 검토하는 데 익숙한 경우 이러한 변경 결과로 PowerPivot 서버 작업에 대한 정보가 적게 포함되어 있음을 알 수 있습니다.  
  
 *높음*유형을 제외하고 모든 PowerPivot 메시지는 자세히 범주에 해당합니다. 연결, 요청 또는 쿼리 보고와 같은 일상적인 서버 작업에 대한 로그 항목이 필요한 경우에는 로깅 수준을 자세히로 변경해야 합니다.  
  
 개별 이벤트 범주에 대한 진단 로깅 수준을 수정하려면  
  
1.  SharePoint 중앙 관리에서 **모니터링**을 클릭합니다.  
  
2.  **진단 로깅 구성**을 클릭합니다.  
  
3.  **PowerPivot 서비스**로 스크롤합니다.  
  
4.  범주를 확장하고 개별 범주를 선택합니다.  
  
     **애플리케이션 페이지 요청** 은 PowerPivot 데이터 원본 로딩 및 팜의 다른 서버와의 통신을 위해 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 를 찾을 때 서비스 애플리케이션에 의해 트리거되는 이벤트를 지정합니다.  
  
     **요청 처리** 는 팜의 서버에 로드되어 있는 PowerPivot 데이터베이스에 대한 쿼리 요청에 의해 트리거되는 이벤트를 지정합니다.  
  
     **사용** 은 PowerPivot 사용 데이터 컬렉션과 관련된 이벤트를 지정합니다.  
  
5.  최소 중요 이벤트에서 이벤트 로그에 보고하려면 **없음** 을 선택하여 해당 범주에 대한 이벤트 로깅을 해제하거나 **오류** 를 선택하여 오류만으로 로깅을 제한합니다.  
  
6.  이벤트 로그에 모든 이벤트를 기록하려면 **자세히** 를 선택합니다.  
  
7.  최소 중요 이벤트에서 추적 로그에 보고하려면 **없음** 을 선택하여 해당 범주에 대한 추적을 해제하거나 **오류** 를 선택하여 오류만으로 추적을 제한합니다.  
  
8.  추적 로그에 모든 이벤트를 기록하려면 **자세히** 를 선택합니다.  
  
9. **확인**을 클릭합니다.  
  
##  <a name="bkmk_how2viewlogfiles"></a> SharePoint 로그 파일을 보는 방법  
 로그 파일은 텍스트 파일이므로 텍스트 편집기에서 열 수 있습니다. 타사 로그 뷰어 애플리케이션을 사용할 수도 있습니다.  
  
#### <a name="use-a-text-editor"></a>텍스트 편집기 사용  
 텍스트 편집기를 사용하여 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버 오류를 해결하려면 다음 팁을 참조하여 파일에서 관련 정보를 찾을 수 있습니다.  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서 게시, 보기 또는 새로 고침 관련 오류인 경우 로그 파일에서 통합 문서의 이름을 검색합니다.  
  
-   상관 관계 ID를 제공하는 오류인 경우 ID를 복사한 후 로그 파일에서 검색 단어로 사용합니다.  
  
-   오류 상태 "High" 또는 "Exception"을 검색합니다. "PowerPivot 서비스"를 검색 합니다.  
  
-   오류가 발생한 시간을 알고 있는 경우 날짜 및 시간 정보를 사용하여 스크롤해야 하는 항목 범위를 좁힙니다.  
  
#### <a name="use-a-log-viewer-application"></a>로그 뷰어 애플리케이션 사용  
 텍스트 편집기를 사용하여 추적 로그를 개별적으로 볼 수도 있지만, 여러 로그 파일을 동시에 볼 수 있는 로그 뷰어 애플리케이션을 사용하면 더욱 유용합니다. 단일 작업 영역에서 여러 추적 로그를 볼 수 있는 다양한 타사 로그 뷰어 애플리케이션을 Codeplex 사이트에서 다운로드할 수 있습니다.  
  
 다음 지침에는 Codeplex에서 다운로드할 수 있는 많이 사용되는 SharePoint ULS Log Viewer에 대한 링크가 포함되어 있습니다.  
  
1.  Codeplex 사이트의 [SharePoint LogViewer](http://sharepointlogviewer.codeplex.com) 또는 [SharePoint ULS Log Viewer](https://go.microsoft.com/fwlink/?LinkId=150052) 로 이동합니다.  
  
2.  **Downloads** 탭을 클릭합니다.  
  
3.  실행 파일을 클릭합니다. 실행 파일은 **SharePointLogViewer.exe** 또는 **ULS Viewer 2.0 Binary**입니다.  
  
4.  사용권 계약을 읽고 동의합니다.  
  
5.  **Save** 를 클릭하여 소프트웨어를 로컬 시스템에 다운로드합니다.  
  
     SharePoint ULS Log Viewer를 다운로드할 경우 ULSViewer.zip을 Downloads 폴더에 저장합니다.  
  
6.  Downloads 폴더에서 ULSViewer.zip을 마우스 오른쪽 단추로 클릭한 다음 **모두 추출**을 선택합니다.  
  
7.  대상 폴더를 지정한 다음 **추출**을 클릭합니다.  
  
8.  추출된 프로그램 파일이 들어 있는 폴더에서 **ULSViewer** 를 두 번 클릭하여 애플리케이션을 실행합니다.  
  
9. 애플리케이션 창의 왼쪽 위 모퉁이에서 폴더 아이콘을 클릭합니다.  
  
10. \Program files\Common Files\Microsoft Shared\Web Server Extensions\14\Logs로 이동합니다.  
  
11. 추적 로그를 하나 이상 선택합니다. 기본적으로 추적 로그 파일 이름은 컴퓨터 이름과 날짜 및 시간 정보로 구성됩니다. 파일 형식은 텍스트 문서입니다.  
  
12. **열기** 를 클릭하고 파일이 로드될 때까지 기다립니다.  
  
13. 기본 제공 필터를 사용하여 심각도, 프로세스, 범주 또는 사용자 정의 텍스트 파일을 기반으로 레코드를 선택합니다. 열 머리글을 클릭하여 정렬 순서를 변경할 수도 있습니다.  
  
#### <a name="entries-for-powerpivot-services"></a>PowerPivot 서비스 항목  
 다음 표는 SharePoint 로그 파일에 표시될 가능성이 높은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 이벤트 작업 항목을 보여 줍니다.  
  
|처리|영역|범주|Level|메시지|설명|  
|-------------|----------|--------------|-----------|-------------|-------------|  
|w3wp.exe|PowerPivot 서비스|사용|자세히|로그는 물론이고 현재 요청 통계도 없습니다.|미리 정해진 간격에 따라 서비스에서는 사용 데이터 컬렉션 시스템에 쿼리 응답 통계를 사용 이벤트로 보고합니다. 이 메시지는 보고할 쿼리 통계가 없다는 것을 나타냅니다.|  
|w3wp.exe|PowerPivot 서비스|웹 프런트 엔드|자세히|데이터 원본에 대 한 응용 프로그램 서버 찾기 시작 =\<*경로*>|연결 요청이 수신되면 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스에서는 요청을 처리하는 데 사용할 수 있는 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 를 식별합니다. 팜에 서버가 하나만 있는 경우 로컬 서버에서 모든 경우의 요청을 수락합니다.|  
|w3wp.exe|PowerPivot 서비스|웹 프런트 엔드|자세히|애플리케이션 서버를 찾았습니다.|요청이 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 애플리케이션에 할당되었습니다.|  
|w3wp.exe|PowerPivot 서비스|웹 프런트 엔드|자세히|에 대 한 요청을 \< *PowerPivotdata 원본*>에 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)].|요청이 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]에 전달되었습니다.|  
|w3wp.exe|PowerPivot 서비스|요청 처리|자세히|사용자 이름에 대 한 요청\<*SharePoint 사용자*> 데이터베이스로|SharePoint 사용자를 대신하여 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 원본에 대한 가장 연결을 만들었습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [PowerPivot 사용 현황 데이터 수집](power-pivot-usage-data-collection.md)   
 [SQL Server 설치 로그 파일 보기 및 읽기](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [사용 현황 데이터 수집 구성 &#40;SharePoint 용 PowerPivot](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  
