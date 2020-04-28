---
title: 중앙 관리를 실행 하는 웹 프런트 엔드 서버에 ADOMD.NET 설치 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c2372180-e847-4cdb-b267-4befac3faf7e
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: f36e00a9393dcbdf1f8cbfe878b8382e6a8dac9d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952148"
---
# <a name="install-adomdnet-on-web-front-end-servers-running-central-administration"></a>중앙 관리를 실행하는 웹 프런트 엔드 서버에 ADOMD.NET 설치
  Excel Services 또는 SharePoint용 PowerPivot이 없는 중앙 관리의 토폴로지가 포함된 팜에 SharePoint용 PowerPivot을 설치하는 경우, PowerPivot 관리 대시보드의 모든 기본 제공 보고서에 액세스하려면 Microsoft ADOMD.NET 클라이언트 라이브러리를 다운로드하여 설치합니다. 대시보드의 일부 보고서는 ADOMD.NET을 사용하여 팜의 PowerPivot 쿼리 처리 및 서버 상태에 대한 보고 데이터를 제공하는 내부 데이터에 액세스합니다.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2010  
  
 SharePoint 2013의 경우 공급자가 SQL Server 기능 팩에 포함되어 있습니다. spPowerPivot.msi를 다운로드하는 방법에 대한 자세한 내용은 [Microsoft SQL Server 2014 기능 팩](https://www.microsoft.com/download/details.aspx?id=35577)을 참조하십시오.  
  
### <a name="download-and-install-the-client-library"></a>클라이언트 라이브러리 다운로드 및 설치  
  
1.  [SQL Server 2014 기능 팩 페이지](https://go.microsoft.com/fwlink/?LinkID=296473)에서 Microsoft ADOMD.NET을 찾습니다.  
  
2.  `SQL_AS_ADOMD.msi` 설치 프로그램의 x64 패키지를 다운로드합니다.  
  
3.  .msi를 실행하여 라이브러리를 설치합니다.  
  
4.  설치가 완료되면 IIS를 다시 설정합니다. 관리 명령 프롬프트를 열고 **IISRESET**을 입력합니다.  
  
### <a name="verify-installation"></a>설치 확인  
  
1.  Windows\Assembly로 이동합니다.  
  
2.  Microsoft.AnalysisServices.AdomdClient를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
3.  **버전**을 클릭합니다.  
  
4.  버전에 12.00이 포함 되어 있는지 확인 합니다. \<빌드 번호> 고 설명은 AnalysisService. microsoft.analysisservices.adomdclient.cellset<입니다.  
  
## <a name="see-also"></a>참고 항목  
 [PowerPivot 관리 대시보드 및 사용량 현황 데이터](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data)  
  
  
