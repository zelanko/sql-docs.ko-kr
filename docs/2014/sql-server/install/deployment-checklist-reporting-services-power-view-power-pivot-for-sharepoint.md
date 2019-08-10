---
title: '배포 검사 목록: Reporting Services, 파워 뷰 및 SharePoint용 PowerPivot | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 9a2575c8-06fc-4ef4-9f24-c19e52b1bbcf
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: be1c0b23afa8110fcf32b969e93fae7d9bf7f324
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890601"
---
# <a name="deployment-checklist-reporting-services-power-view-and-powerpivot-for-sharepoint"></a>배포 검사 목록: Reporting Services, Power View 및 SharePoint용 PowerPivot
  다음 검사 목록을 사용 하 여 동일한 SharePoint 팜에 이러한 BI 기능을 설치 합니다. SharePoint용 PowerPivot, 보고서 작성기 및 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]입니다. 이 검사 목록에서는 특정 설치 순서를 권장하지만 실제로는 어떠한 순서로도 이 기능을 설치할 수 있습니다. 이 검사 목록에서는 다음 제품 또는 기능이 설치되어 있다고 가정합니다.  
  
1.  SharePoint Server 2010 SP1(서비스 팩 1)  
  
2.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]데이터베이스 엔진  
  
3.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Reporting Services 및 Reporting Services 추가 기능  
  
4.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SharePoint용 PowerPivot  
  
 이 기능을 설치하면 다음과 같은 작업을 수행할 수 있습니다.  
  
-   SharePoint 사이트에서 PowerPivot for Excel에서 만든 PowerPivot 통합 문서에 액세스할 수 있습니다.  
  
-   SharePoint에서 PowerPivot 통합 문서를 기반으로 대화형 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 보고서를 작성할 수 있습니다.  
  
-   SharePoint에서 보고서 작성기를 시작하여 보고서 작성기 보고서를 만들 수 있습니다.  
  
> [!NOTE]  
>  SharePoint용 PowerPivot을 사용하려면 SharePoint 팜에 SharePoint 2010 SP1(서비스 팩 1)을 설치해야 합니다. 평가 목적으로 소프트웨어를 설치하는 경우 팜 업그레이드 단계로 인한 오버헤드를 방지할 수 있도록 새로운 서버에서 시작하는 것이 좋습니다. 팜 업그레이드는 SharePoint 작업에 영향을 미치므로 주의깊게 계획해야 합니다. 가능한 빨리 SharePoint용 PowerPivot을 설치하고 싶다면 SharePoint 2010을 설치하고 SharePoint 2010 SP1을 설치한 다음 이후 단계에서 팜을 구성합니다. SharePoint 2010 SP1을 설치할 때 팜이 구성되지 않으므로 업그레이드가 수행되지 않습니다.  
>   
>  이 검사 목록에서는 PowerPivot 구성 도구를 사용하여 SharePoint용 PowerPivot을 구성하는 동안 팜 구성 단계가 수행되는 것으로 가정합니다. 또는 원하는 경우 SharePoint 제품 구성 마법사를 사용할 수도 있습니다. 두 방법 모두 결과적으로 SharePoint용 PowerPivot을 지원하는 팜이 작동합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 SQL Server 설치 프로그램을 실행하려면 로컬 관리자여야 합니다.  
  
 SharePoint용 PowerPivot를 사용하려면 SharePoint Server 2010 Enterprise Edition이 필요합니다. Evaluation Enterprise Edition을 사용할 수도 있습니다.  
  
 SharePoint Server 2010 SP1을 설치해야 합니다. 없을 경우 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 기능을 사용하도록 팜을 구성할 수 없습니다.  
  
 컴퓨터가 도메인에 조인되어 있어야 합니다.  
  
 이 서비스를 프로비전하려면 하나 이상의 도메인 사용자 계정이 있어야 합니다. 다음 서비스에 대 한 도메인 사용자 계정이 필요 합니다. SharePoint 웹 서비스 및 관리 서비스, Reporting Services, Analysis Services, Excel Services, Secure Store Services 및 PowerPivot 시스템 서비스. SharePoint의 관리되는 계정 기능을 지원하려면 도메인 계정이 필요합니다. 데이터베이스 엔진은 가상 계정을 사용하여 프로비전할 수 있지만 다른 모든 서비스는 도메인 사용자로 실행되어야 합니다.  
  
 PowerPivot 인스턴스 이름을 사용할 수 있어야 합니다. SharePoint용 PowerPivot을 설치하는 컴퓨터에 기존의 명명된 PowerPivot 인스턴스가 있어서는 안 됩니다.  
  
 기존 팜에 SharePoint용 PowerPivot를 설치하는 경우 클래식 모드 인증을 사용하도록 구성된 SharePoint 웹 애플리케이션이 하나 이상 필요합니다. PowerPivot 데이터 액세스는 웹 애플리케이션에서 클래식 모드 인증이 지원되는 경우에만 작동합니다. 클래식 모드 요구 사항에 대한 자세한 내용은 [PowerPivot Authentication and Authorization](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization)를 참조하십시오.  
  
 시스템 및 버전 요구 사항을 이해하려면 다음 항목을 검토하십시오.  
  
-   [SharePoint 2010 팜에서 SQL Server BI 기능을 사용하기 위한 지침](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
## <a name="steps"></a>단계  
 다음 단계에서는 관리자가 서버를 설치하고 구성한다고 가정합니다. SharePoint의 설치 사용자는 팜 관리자이기도 하며 기본 사이트 모음의 주 사이트 관리자인 경우가 많습니다. 다음 단계를 여러 명에게 나누는 경우 각 단계가 작동하도록 추가적인 권한이 있어야 합니다.  
  
|단계|링크|  
|----------|----------|  
|SharePoint 2010 제품 준비 도구 실행|SharePoint 2010 설치 미디어가 있어야 합니다. 준비 도구는 설치 미디어의 PreRequisiteInstaller.exe입니다.|  
|SharePoint Server 2010 Enterprise 또는 Enterprise Evaluation Edition 설치|SharePoint를 설치할 때 설치 프로그램을 마친 후 SharePoint 2010 제품 구성 마법사를 실행하지 않음으로써 팜을 나중에 구성하도록 선택할 수 있습니다. 팜을 구성 하려고 대기 하면 이후 단계에서 설치 되는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 데이터베이스 엔진 인스턴스를 팜의 데이터베이스 서버로 사용할 수 있습니다. 팜을 구성하려면 PowerPivot 구성 도구를 사용합니다. 여기에는 팜이 아직 구성되지 않은 경우 팜을 프로비전하는 동작이 포함되어 있습니다.|  
|SharePoint Server 2010 SP1 설치|에서 s p [https://support.microsoft.com/kb/2460045](https://go.microsoft.com/fwlink/p/?linkID=219697)1을 다운로드 합니다.|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 설치 프로그램을 실행하여 데이터베이스 엔진과 SharePoint용 PowerPivot 설치|[SharePoint 2010용 PowerPivot 설치](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)<br /><br /> 1단계에서는 SharePoint용 PowerPivot 설치 방법에 대해 설명합니다. 이 단계에서는 설치 역할 페이지에서 데이터베이스 엔진을 역할에 추가하는 확인란을 클릭해야 합니다. 이렇게 하면 다음 단계에서 팜을 구성할 때 팜의 데이터베이스 서버로 사용할 수 있도록 데이터베이스 엔진 설치에 추가 됩니다. 그러나 팜이 이미 구성되어 있는 경우 이 단계를 건너뛸 수 있습니다.<br /><br /> 2단계에서는 서버를 구성합니다. 이 단계에서 PowerPivot 구성 도구를 선택하십시오. 여러 접근 방법을 사용할 수 있지만 독립 실행형 설치의 경우 구성 도구를 사용하는 것이 가장 효율적입니다.<br /><br /> SharePoint 2010이 설치되었지만 구성되지 않은 경우 이 도구에서는 팜, 기본 웹 애플리케이션 및 루트 사이트 모음을 만드는 동작이 미리 선택됩니다. 팜이 만들어지도록 이 옵션들을 선택된 상태로 두십시오. 팜을 이미 구성한 경우 이 도구는 이러한 동작을 생략하고 SharePoint용 PowerPivot 구성에 필요한 동작만 제공합니다.<br /><br /> 3단계에서는 SQL Server 2008 R2 버전의 Analysis Services OLE DB 공급자를 설치하는 방법에 대해 설명합니다. 이 단계는 2008 R2 버전의 PowerPivot for Excel에서 만든 통합 문서 버전을 지원하기 위해 필요합니다.|  
|팜이 작동하는지 확인|먼저 중앙 관리를 시작하여 팜이 사용 가능한지 확인합니다. 다음으로를 입력 http://localhost 하 여 팀 사이트를 엽니다.  SharePoint 팀 사이트가 표시되어야 합니다.|  
|SharePoint용 PowerPivot이 작동하는지 확인|[SharePoint용 PowerPivot 설치 확인](https://docs.microsoft.com/analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation)<br /><br /> 이 태스크에서는 업로드한 예제 통합 문서를 사용하여 PowerPivot 데이터 액세스를 확인합니다.|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 설치 프로그램을 실행하여 Reporting Services 및 Reporting Services 추가 기능 설치 및 구성|[SharePoint 2010용 Reporting Services SharePoint 모드 설치](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)<br /><br /> 표 형식 데이터를 호스팅하기 위해 보조 리소스가 필요한 경우 Reporting Services를 설치하는 동안 선택적으로 설치 기능 트리에 Analysis Services 인스턴스를 더 추가할 수 있습니다. 추가 Analysis Services 인스턴스는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 만든 표 형식 model 데이터베이스를 호스팅하는 데 사용할 수 있습니다. 표 형식 데이터베이스는 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 보고서에 사용할 수 있는 데이터 원본입니다.<br /><br /> [테이블 형식 모드에서 Analysis Services 설치](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services)|  
|Reporting Services가 작동하는지 확인|[Reporting Services 설치 확인](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)|  
|(사이트 관리자) SharePoint 권한 구성|SharePoint 라이브러리에서 항목을 추가, 편집 또는 삭제하려면 참가 권한이 있어야 합니다. 포함된 데이터를 나타내는 PowerPivot 통합 문서 및 보고서에 읽기 전용으로 액세스하려면 보기 수준 권한만 있으면 됩니다.<br /><br /> 외부 데이터 원본으로 액세스되는 PowerPivot 통합 문서(이때 통합 문서 URL은 다른 통합 문서 또는 보고서의 연결 문자열)에는 보기 권한보다 높은 읽기 권한이 필요합니다.<br /><br /> BI 의미 체계 모델 연결에도 읽기 권한이 필요합니다. 올바른 권한을 제공하기 위해 새 권한 수준 또는 SharePoint 그룹을 만들어야 할 수도 있습니다.|  
|(사이트 관리자) 문서 라이브러리 확장|BI 콘텐츠 형식을 사용 하도록 문서 라이브러리를 확장 합니다. BI 의미 체계 모델 연결, Reporting Services 공유 데이터 원본, 보고서 작성기 보고서:<br /><br /> 1) <br />                    **콘텐츠 형식 관리 사용**. 공유 문서 또는 다른 문서 라이브러리의 라이브러리 탭에서 **라이브러리 설정**을 클릭합니다. 일반 설정에서 **고급 설정**을 클릭합니다. 콘텐츠 형식에서 **예** 를 선택하여 콘텐츠 형식 관리를 허용한 다음 **확인**을 클릭합니다.<br /><br /> 2) <br />                    **BI 콘텐츠 형식 선택**. 라이브러리 탭에서 **라이브러리 설정**을 클릭합니다. 콘텐츠 형식에서 **기존 사이트 콘텐츠 형식에서 추가**를 클릭합니다. 비즈니스 인텔리전스 콘텐츠 형식 그룹에서 **BI 의미 체계 모델 연결 파일** 과 **보고서 데이터 원본**을 추가합니다. 필요에 따라 추가 보고서 작성 시나리오를 설정하기 위해 보고서 모델과 같은 다른 Reporting Services 콘텐츠 형식을 추가할 수도 있습니다.<br /><br /> <br /><br /> 자세한 내용은 [라이브러리 &#40;에 BI 의미 체계 모델 연결 콘텐츠 형식 추가 SharePoint용 PowerPivot&#41; ](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/add-bi-semantic-model-connection-content-type-to-library) 및 [SharePoint 통합 모드 &#40;&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md).|  
|(사이트 관리자) [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]를 시작하는 데 사용되는 데이터 연결 파일 만들기|[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]에 대한 데이터 원본으로 BI 의미 체계 모델 연결(.bism) 또는 Reporting Services 공유 데이터 원본(.rsds)을 만들어야 합니다. 데이터 연결 파일을 만든 후 이 데이터 연결을 데이터 원본으로 사용하여 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]를 시작할 수 있습니다.<br /><br /> [PowerPivot 통합 문서에 대한 BI 의미 체계 모델 연결 만들기](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-power-pivot-workbook)<br /><br /> [테이블 형식 model 데이터베이스에 대한 BI 의미 체계 모델 연결 만들기](../../relational-databases/databases/model-database.md)<br /><br /> 참고: [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 를 사용할 수 있는 이유는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 버전의 Reporting Services를 설치했고 서버를 공유 서비스로 구성했기 때문입니다. Reporting Services를 설치하고 이를 SQL Server 2008 수준의 통합용으로 구성한 경우 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]를 사용할 수 없습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 2012 버전에서 지 원하는 기능](https://go.microsoft.com/fwlink/?linkid=232473)  
  
  
