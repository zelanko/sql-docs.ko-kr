---
title: 테이블 형식 모델 데이터베이스에 연결 (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 983d0c8a-77da-4c6e-8638-283bcb14f143
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6f73a8e9e79a08c3f4a1f1e2b40ff5f83a0e39b7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66067655"
---
# <a name="connect-to-a-tabular-model-database-ssas"></a>테이블 형식 모델 데이터베이스에 연결(SSAS)
  테이블 형식 모델을 빌드하여 Analysis Services 테이블 형식 모드 서버로 배포한 후 클라이언트 애플리케이션에서 사용할 수 있도록 권한을 설정해야 합니다. 이 항목에서는 사용 권한을 부여하는 방법과 클라이언트 애플리케이션에서 데이터베이스에 연결하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  기본적으로 방화벽을 구성해야만 Analysis Services에 대한 원격 연결을 사용할 수 있습니다. 클라이언트 연결에 대해 명명된 인스턴스 또는 기본 인스턴스를 구성하는 경우 적절한 포트를 열어야 합니다. 자세한 내용은 [Configure the Windows Firewall to Allow Analysis Services Access](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)을 참조하세요.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
 [데이터베이스에 대 한 사용자 권한](#bkmk_userpermissions)  
  
 [서버에 대 한 관리 권한](#bkmk_admin)  
  
 [Excel 또는 SharePoint에서 연결](#bkmk_excelconn)  
  
 [연결 문제 해결](#bkmk_Tshoot)  
  
##  <a name="bkmk_userpermissions"></a>데이터베이스에 대 한 사용자 권한  
 테이블 형식 데이터베이스에 연결하는 사용자는 읽기 액세스 권한을 지정하는 데이터베이스 역할의 멤버여야 합니다.  
  
 
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 모델을 작성할 때 또는 배포된 모델에 대해 역할 또는 역할 멤버 자격이 정의됩니다. 
  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 역할 관리자를 사용하여 역할을 만드는 방법은 [역할 만들기 및 관리&#40;SSAS 테이블 형식&#41;](roles-ssas-tabular.md)를 참조하세요. 배포된 모델에 대한 역할을 만들고 관리하는 방법은 [테이블 형식 모델 역할&#40;SSAS 테이블 형식&#41;](tabular-model-roles-ssas-tabular.md)을 참조하세요.  
  
> [!CAUTION]  
>  
  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 에서 역할 관리자를 사용하여 정의한 역할로 테이블 형식 모델 프로젝트를 다시 배포하면 배포된 테이블 형식 모델에 정의된 역할을 덮어씁니다.  
  
##  <a name="bkmk_admin"></a>서버에 대 한 관리 권한  
 SharePoint를 사용하여 Excel 통합 문서 또는 Reporting Services 보고서를 호스팅하는 조직에서는 테이블 형식 모델 데이터를 SharePoint 사용자가 사용할 수 있도록 추가로 구성 작업을 수행해야 합니다. SharePoint를 사용하지 않는 경우 이 섹션을 건너뛰십시오.  
  
 테이블 형식 데이터가 포함된 Excel 통합 문서 또는 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 보고서를 보려면 Excel 서비스 또는 Reporting Services를 실행하는 데 사용된 계정에 Analysis Services 인스턴스에 대한 관리자 권한이 있어야 합니다. 관리 권한이 있어야 Analysis Services 인스턴스가 이러한 서비스를 신뢰할 수 있습니다.  
  
#### <a name="grant-administrative-access-on-the-server"></a>서버에 대한 관리 권한 부여  
  
1.  중앙 관리에서 서비스 계정 구성 페이지를 엽니다.  
  
2.  Excel 서비스에서 사용하는 서비스 애플리케이션 풀을 선택합니다. **서비스 응용 프로그램 풀-SharePoint 웹 서비스 시스템** 또는 사용자 지정 응용 프로그램 풀을 서비스 할 수 있습니다. Excel 서비스에서 사용하는 관리되는 계정이 페이지에 나타납니다.  
  
     SharePoint 모드의 Reporting Services가 포함된 SharePoint 팜의 경우 Reporting Services 서비스 애플리케이션에 대한 계정 정보도 가져옵니다.  
  
     다음 단계에서는 Analysis Services 인스턴스의 서버 역할에 이 계정을 추가합니다.  
  
3.  
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 인스턴스에 연결하고 서버 인스턴스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다. 개체 탐색기에서 **역할** 을 마우스 오른쪽 단추로 클릭한 다음 **새 역할**을 선택합니다.  
  
4.  Analysis Services 속성 페이지에서 **보안**을 클릭합니다.  
  
5.  
  **추가**를 클릭하고 Excel 서비스에 사용되는 계정을 입력하고 그 뒤에 Reporting Services에 사용되는 계정을 입력합니다.  
  
##  <a name="bkmk_excelconn"></a>Excel 또는 SharePoint에서 연결  
 Analysis Services 데이터베이스에 대한 액세스를 제공하는 클라이언트 라이브러리를 사용하여 테이블 형식 모드 서버에서 실행되는 모델 데이터베이스에 연결할 수 있습니다. 이러한 라이브러리에는 Analysis Services OLE DB 공급자, ADOMD.NET 및 AMO가 포함됩니다.  
  
 Excel은 OLE DB 공급자를 사용합니다. SQL Server 2008 R2의 MSOLAP.4(파일 이름 msolap100.dll, 10.50.1600.1 버전) 또는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 버전의 PowerPivot for Excel과 함께 설치된 MSOLAP.5(파일 이름 msolap110.dll)가 있는 경우 테이블 형식 데이터베이스에 연결할 수 있습니다.  
  
 다음 방법 중 하나를 사용하여 Excel에서 모델 데이터베이스에 연결할 수 있습니다.  
  
-   다음 섹션의 설명에 따라 Excel 내에서 데이터 연결을 만듭니다.  
  
-   Analysis Services 테이블 형식 모드 서버에서 실행되는 데이터베이스에 대한 리디렉션을 제공하는 BI 의미 체계 모델 연결 파일(.bism)을 SharePoint에서 만듭니다. BI 의미 체계 모델 연결 파일은 연결에 지정된 모델 데이터베이스를 사용하여 Excel을 시작하는 마우스 오른쪽 단추 실행 명령을 제공합니다. Reporting Services가 설치된 경우 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 도 시작됩니다. BI 의미 체계 모델 연결 파일을 만들고 사용하는 방법은 [테이블 형식 모델 데이터베이스에 대한 BI 의미 체계 모델 연결 만들기](../power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)를 참조하세요.  
  
-   테이블 형식 데이터베이스를 데이터 원본으로 참조하는 Reporting Services 공유 데이터 원본을 만듭니다. SharePoint에서 공유 데이터 원본을 만들어서 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]를 시작하는 데 사용할 수 있습니다.  
  
#### <a name="connect-from-excel"></a>Excel에서 연결  
  
1.  Excel의 **데이터** 탭에 있는 **외부 데이터 가져오기**에서 **기타 원본**을 클릭합니다.  
  
2.  
  **Analysis Services**를 선택합니다.  
  
3.  
  **서버 이름**에서 해당 데이터베이스를 호스팅하는 Analysis Services 인스턴스를 지정합니다. 서버 이름은 대개 서버 소프트웨어를 실행하는 컴퓨터의 이름입니다. 서버가 명명 된 인스턴스로 설치 된 경우 \<servername>\\<instancename\>형식으로 이름을 지정 해야 합니다.  
  
     서버 인스턴스는 독립 실행형 테이블 형식 배포를 사용하도록 구성되어야 하며 서버 인스턴스에는 액세스를 허용하는 인바운드 규칙이 있어야 합니다. 자세한 내용은 [Analysis Services 인스턴스의 서버 모드 확인](../instances/determine-the-server-mode-of-an-analysis-services-instance.md) 및 [Analysis Services 액세스를 허용하도록 Windows 방화벽 구성](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)을 참조하세요.  
  
4.  로그온 자격 증명의 경우 데이터베이스에 대한 읽기 권한이 있으면 **Windows 인증 사용** 을 선택합니다. 그렇지 않으면 **다음 사용자 이름과 암호 사용**을 선택하고 데이터베이스 권한이 있는 Windows 계정의 사용자 이름과 암호를 입력합니다. **다음**을 클릭합니다.  
  
5.  데이터베이스를 선택합니다. 올바르게 선택하면 데이터베이스에 대해 단일 **모델** 큐브가 표시됩니다. 
  **다음**을 클릭한 후 **마침**을 클릭합니다.  
  
 연결이 설정되면 데이터를 사용하여 피벗 테이블 또는 피벗 차트를 만들 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [Excel에서 분석&#40;SSAS 테이블 형식&#41;](analyze-in-excel-ssas-tabular.md)에서 역할 관리자 대화 상자를 사용하여 역할을 정의하는 테이블 형식 모델 작성자를 위한 것입니다.  
  
##  <a name="bkmk_sharepoint"></a>SharePoint에서 연결  
 SharePoint용 PowerPivot을 사용하는 경우 Analysis Services 테이블 형식 모드 서버에서 실행되는 데이터베이스에 대한 리디렉션을 제공하는 BI 의미 체계 모델 연결 파일을 SharePoint에서 만들 수 있습니다. BI 의미 체계 모델 연결은 데이터베이스에 대한 HTTP 엔드포인트를 제공합니다. 또한 BI 의미 체계 모델 연결을 사용하면 SharePoint 사이트에서 문서를 정기적으로 사용하는 지식 근로자가 테이블 형식 모델에 쉽게 액세스할 수 있습니다. 지식 근로자는 BI 의미 체계 모델 연결 파일의 위치 또는 해당 URL만 알면 테이블 형식 모델 데이터베이스에 액세스할 수 있습니다. 서버 위치 또는 데이터베이스 이름 정보는 BI 의미 체계 모델 연결에 캡슐화됩니다. BI 의미 체계 모델 연결 파일을 만들고 사용 하는 방법에 대 한 자세한 내용은 [POWERPIVOT Bi 의미 체계 모델 연결 &#40;. bism&#41;](../power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md) 및 [테이블 형식 모델 데이터베이스에 대 한 BI 의미 체계 모델 연결 만들기](../power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)를 참조 하세요.  
  
##  <a name="bkmk_Tshoot"></a>연결 문제 해결  
 이 섹션에서는 테이블 형식 모델 데이터베이스에 연결하는 동안 발생하는 문제에 대한 원인과 해결 단계를 제공합니다.  
  
 **데이터 연결 마법사가 지정한 데이터 원본에서 데이터베이스 목록을 가져올 수 없습니다.**  
  
 데이터를 가져올 때 마법사를 사용하여 원격 Analysis Services 서버에 있는 테이블 형식 모델 데이터베이스에 연결하려고 하지만 권한이 부족한 경우 이 Microsoft Excel 오류가 발생합니다. 이 오류를 해결하려면 데이터베이스에 대한 사용자 액세스 권한이 있어야 합니다. 이 항목의 앞부분에 있는 데이터에 대한 사용자 액세스 권한 부여 지침을 참조하십시오.  
  
 **외부 데이터 원본에 대 한 연결을 설정 하는 동안 오류가 발생 했습니다. 다음 연결을 새로 고치지 못했습니다. \<모델 이름> 샌드박스**  
  
 SharePoint에서 모델 데이터를 사용하는 피벗 테이블에서 데이터 필터링과 같은 데이터 상호 작용을 시도할 때 이 Microsoft Excel 오류가 발생합니다. 이 오류는 원격 Analysis Services 서버에 대한 충분한 사용 권한이 없기 때문에 발생합니다. 이 오류를 해결하려면 데이터베이스에 대한 사용자 액세스 권한이 있어야 합니다. 이 항목의 앞부분에 있는 데이터에 대한 사용자 액세스 권한 부여 지침을 참조하십시오.  
  
 **이 작업을 수행 하는 동안 오류가 발생 했습니다. 통합 문서를 다시 로드 한 다음이 작업을 다시 수행 하십시오.**  
  
 SharePoint에서 모델 데이터를 사용하는 피벗 테이블에서 데이터 필터링과 같은 데이터 상호 작용을 시도할 때 이 Microsoft Excel 오류가 발생합니다. 이 오류는 모델 데이터가 배포된 Analysis Services 인스턴스가 Excel 서비스를 신뢰하지 않기 때문에 발생합니다. 이 오류를 해결하려면 Analysis Services 인스턴스에 대한 Excel 서비스 관리 권한을 부여해야 합니다. 이 항목의 앞부분에 있는 관리자 권한 부여 지침을 참조하십시오. 오류가 계속되면 Excel 서비스 애플리케이션 풀을 재활용하십시오.  
  
 **통합 문서에 사용 되는 외부 데이터 원본에 대 한 연결을 설정 하는 동안 오류가 발생 했습니다.**  
  
 SharePoint에서 모델 데이터를 사용하는 피벗 테이블에서 데이터 필터링과 같은 데이터 상호 작용을 시도할 때 이 Microsoft Excel 오류가 발생합니다. 이 오류는 사용자가 통합 문서에 대해 충분한 SharePoint 권한을 가지고 있지 않기 때문에 발생합니다. 사용자에게 **읽기** 이상의 권한이 있어야 합니다. **보기 전용 권한으로** 는 데이터 액세스에 충분 하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 형식 모델 솔루션 배포 &#40;SSAS 테이블 형식&#41;](tabular-model-solution-deployment-ssas-tabular.md)  
  
  
