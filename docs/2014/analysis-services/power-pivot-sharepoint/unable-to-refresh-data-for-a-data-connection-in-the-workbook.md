---
title: '통합 문서에서 데이터 연결에 대한 데이터를 새로 고칠 수 없습니다. 다시 시도하거나 시스템 관리자에게 문의하십시오. 다음 연결을 새로 고치지 못했습니다: PowerPivot 데이터 | Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 0f6fd52d-ac72-43e3-aa08-05a2d2bb873d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4deeeaae2bb08d9f1e2b4c434ec262d0fb7bd679
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48077493"
---
# <a name="unable-to-refresh-data-for-a-data-connection-in-the-workbook-try-again-or-contact-your-system-administrator-the-following-connections-failed-to-refresh-powerpivot-data"></a>통합 문서에서 데이터 연결에 대한 데이터를 새로 고칠 수 없습니다. 다시 시도하거나 시스템 관리자에게 문의하십시오. PowerPivot 데이터 연결을 새로 고치지 못했습니다.
  Excel Services는 PowerPivot 서버에 연결 요청을 제출하고 이 요청이 실패하는 경우 PowerPivot 데이터를 포함하는 Excel 통합 문서에 대해 이 오류를 반환합니다.  
  
## <a name="details"></a>설명  
  
|||  
|-|-|  
|적용 대상:|SharePoint용 PowerPivot 설치|  
|제품 버전|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|원인|아래를 참조하십시오.|  
|메시지 텍스트|통합 문서에서 데이터 연결에 대한 데이터를 새로 고칠 수 없습니다. 다시 시도하거나 시스템 관리자에게 문의하십시오. PowerPivot 데이터 연결을 새로 고치지 못했습니다.|  
  
## <a name="explanation-and-resolution"></a>설명 및 해결 방법  
 Excel Services가 PowerPivot 데이터에 연결하거나 로드할 수 없습니다. 이 오류가 발생하는 조건은 다음과 같습니다.  
  
 **시나리오 1: 서비스가 시작되지 않은 경우**  
  
 SQL Server Analysis Services(PowerPivot) 인스턴스가 시작되지 않았습니다. 만료된 암호로 인해 서비스 실행이 중지됩니다. 암호를 변경 하는 방법에 대 한 자세한 내용은 참조 하세요. [Configure PowerPivot Service Accounts](configure-power-pivot-service-accounts.md) 하 고 [시작 또는 Stop a PowerPivot for SharePoint 서버](start-or-stop-a-power-pivot-for-sharepoint-server.md)합니다.  
  
 **시나리오 2a: 서버에서 이전 버전의 통합 문서를 여는 경우**  
  
 열려는 통합 문서가 SQL Server 2008 R2 버전의 PowerPivot for Excel에서 작성되었을 수 있습니다. 이는 대개 데이터 연결 문자열에 지정된 Analysis Services 데이터 공급자가 요청을 처리할 컴퓨터에 없는 경우에 해당합니다.  
  
 이 경우 ULS 로그에서이 메시지를 확인할 수 있습니다: "통합 문서에서 ' PowerPivot 데이터 '에 대 한 새로 고침 실패 '\<통합 문서에 대 한 URL >'", "연결을 가져올 수 없습니다."입니다.  
  
 통합 문서의 버전을 확인하려면 Excel에서 해당 통합 문서를 열고 연결 문자열에 지정된 데이터 공급자를 확인합니다. SQL Server 2008 R2 통합 문서는 MSOLAP.4를 데이터 공급자로 사용합니다.  
  
 통합 문서를 업그레이드하여 이 문제를 해결할 수 있습니다. 또는 SharePoint용 PowerPivot이나 Excel 서비스를 실행하는 물리적 컴퓨터에 Analysis Services SQL Server 2008 R2 버전의 클라이언트 라이브러리를 설치할 수 있습니다.  
  
 [SharePoint 서버에서 Analysis Services OLE DB Provider 설치](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)  
  
 **시나리오 2b: 클라이언트 라이브러리 버전이 잘못된 응용 프로그램 서버에서 Excel Services를 실행 중인 경우**  
  
 기본적으로 SharePoint Server 2010은 Excel 서비스가 실행되는 응용 프로그램 서버에 SQL Server 2008 버전의 Analysis Services OLE DB 공급자를 설치합니다. PowerPivot 데이터 액세스를 지원하는 팜에서 Excel 서비스 및 SharePoint용 PowerPivot과 같이 PowerPivot 데이터를 요청하는 응용 프로그램을 실행하는 물리적인 서버는 모두 최신 버전의 데이터 공급자를 사용해야 합니다.  
  
 SharePoint용 PowerPivot을 실행하는 서버는 업데이트된 OLE DB 데이터 공급자를 자동으로 가져옵니다. 동일한 컴퓨터에서 SharePoint용 PowerPivot 없이 독립 실행형 인스턴스인 Excel 서비스를 실행하는 서버와 같은 다른 서버는 최신 클라이언트 라이브러리를 사용하도록 패치해야 합니다. 자세한 내용은 [SharePoint 서버에서 Analysis Services OLE DB 공급자 설치](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)를 참조하세요.  
  
 **시나리오 3b: 도메인 컨트롤러를 사용할 수 없는 경우**  
  
 사용자 ID의 유효성을 검사하는 데 도메인 컨트롤러를 사용할 수 없기 때문일 수 있습니다. 각 연결에서 SharePoint 사용자를 인증하려면 Windows 토큰 서비스에 대한 클레임에 도메인 컨트롤러가 필요합니다. Windows 토큰 서비스에 대한 클레임은 캐시된 자격 증명을 사용하지 않으며, 각 연결에 대해 사용자 ID 유효성을 검사합니다.  
  
 SharePoint 로그 파일을 통해 이 오류의 원인을 확인할 수 있습니다. SharePoint 로그에 "IClaimsIdentity에서 WindowsIdentity을(를) 가져오지 못했습니다." 메시지가 포함되어 있으면 사용자 ID를 인증할 수 없는 것입니다.  
  
 이 문제를 해결하려면 컴퓨터를 PowerPivot 서버와 같은 도메인에 참가시키거나 로컬 컴퓨터에 도메인 컨트롤러를 설치합니다. 두 번째 해결 방법인 도메인 컨트롤러 설치를 수행하려면 모든 서비스 및 사용자에 대해 로컬 도메인 계정을 만들어야 합니다. 정의한 계정에 대해 서비스 계정 및 SharePoint 권한을 구성해야 합니다.  
  
 오프라인 상태로 SharePoint용 PowerPivot을 사용하는 것이 목적인 경우 컴퓨터에 도메인 컨트롤러를 설치하면 유용합니다. 자세한 지침은 PowerPivot을 오프 라인으로 사용 하는 방법에 대 한 블로그 항목을 참조에서 "Taking your PowerPivot server off the network" [ http://www.powerpivotgeek.com ](http://go.microsoft.com/fwlink/?LinkId=184241)합니다.  
  
 **시나리오 4: 서버가 불안정한 경우**  
  
 하나 이상의 서비스가 일관성이 없는 상태일 수 있습니다. IISRESET를 실행하면 문제가 해결되는 경우가 있습니다.  
  
  
