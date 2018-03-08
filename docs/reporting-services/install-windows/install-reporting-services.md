---
title: "SQL Server Reporting Services(2017 이상) 설치 | Microsoft Docs"
ms.date: 12/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.custom: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Active
ms.openlocfilehash: d3f53de12e07925af838b5188e9b889ae44eb090
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="install-sql-server-reporting-services-2017-and-later"></a>SQL Server Reporting Services(2017 이상) 설치

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

SQL Server Reporting Services 설치에는 보고서 항목을 저장하고 보고서를 렌더링하며 구독 및 기타 보고서 서비스를 처리하기 위한 서버 구성 요소가 포함됩니다. 

SQL Server 2017 Reporting Services를 다운로드하려면 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=55252)로 이동하세요.

> [!NOTE]
> Power BI Report Server를 찾고 있나요? [Power BI Report Server 설치](https://powerbi.microsoft.com/documentation/reportserver-install-report-server/)를 참조하세요.

## <a name="before-you-begin"></a>시작하기 전 주의 사항

Reporting Services를 설치하기 전에 [SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)을 검토합니다.

## <a name="install-your-report-server"></a>보고서 서버 설치

보고서 서버를 설치하는 것은 간단합니다. 파일을 설치하는 몇 가지 단계가 있습니다.

> [!NOTE]
> 설치 시 사용 가능한 SQL Server 데이터베이스 엔진 서버가 필요하지 않습니다. 설치 후 Reporting Services를 구성하려면 하나가 필요합니다.

1. SQLServerReportingServices.exe의 위치를 찾고 설치 관리자를 시작합니다.

2. **Reporting Services 설치**를 선택합니다.

    ![Reporting Services 설치](media/install-reporting-services/report-server-install.png)

3. 버전을 선택하여 설치한 후 **다음**을 선택합니다.

    ![버전 선택](media/install-reporting-services/report-server-install-edition.png)

    무료 버전의 경우 드롭다운에서 평가판 또는 개발자 버전을 선택합니다.

    ![평가판 또는 개발자 버전](media/install-reporting-services/report-server-install-edition-select.png)

    그렇지 않은 경우 제품 키를 입력합니다. [SQL Server 2017 Reporting Services의 제품 키를 찾습니다](find-reporting-services-product-key-ssrs.md).

4. 사용 조건을 읽고 동의한 후 **다음**을 선택합니다.

5. 보고서 서버 데이터베이스를 저장하는 데 사용할 수 있는 데이터베이스 엔진이 있어야 합니다. **다음**을 선택하여 보고서 서버만 설치합니다.

    ![데이터베이스는 설치하는 데 필요하지 않음](media/install-reporting-services/report-server-install-db-engine.png)

6. 보고서 서버에 대한 설치 위치를 지정합니다. 계속하려면 **설치**를 선택합니다.

    ![설치 경로 지정](media/install-reporting-services/report-server-install-file-path.png)

    > [!NOTE]
    > 기본 경로는 C:\Program Files\Microsoft SQL Server Reporting Services입니다.

7. 성공적으로 설치 후 **보고서 서버 구성**을 선택하여 Reporting Services 구성 관리자를 시작합니다.

    ![보고서 서버 구성](media/install-reporting-services/report-server-install-configure.png)

## <a name="configuration-your-report-server"></a>보고서 서버 구성

설치에서 **보고서 서버 구성**을 설치한 후 **보고서 서버 구성 관리자**가 나타납니다. 자세한 내용은 [보고서 서버 구성 관리자](reporting-services-configuration-manager-native-mode.md)를 참조하세요.

Reporting Services의 초기 구성을 완료하기 위해 [보고서 서버 데이터베이스를 만들어야](ssrs-report-server-create-a-report-server-database.md) 합니다. 이 단계를 완료하는 데 SQL Server 데이터베이스 서버가 필요합니다.

### <a name="creating-a-database-on-a-different-server"></a>다른 서버에 데이터베이스 만들기

다른 컴퓨터의 데이터베이스 서버에서 보고서 서버 데이터베이스를 만드는 경우 보고서 서버에 대한 서비스 계정을 데이터베이스 서버에서 인식하는 자격 증명으로 변경해야 합니다.

기본적으로 보고서 서버는 가상 서비스 계정을 사용합니다. 다른 서버에서 데이터베이스를 만들려고 하는 경우 연결 적용 권한 단계에서 다음 오류가 나타날 수 있습니다.

`System.Data.SqlClient.SqlException (0x80131904): Windows NT user or group '(null)' not found. Check the name again.`

오류를 해결하기 위해 서비스 계정을 네트워크 서비스 또는 도메인 계정으로 변경할 수 있습니다. 서비스 계정을 네트워크 서비스로 변경하는 것은 보고서 서버에 대한 컴퓨터 계정의 컨텍스트에서 권한을 적용합니다.

자세한 내용은 [보고서 서버 서비스 계정 구성](configure-the-report-server-service-account-ssrs-configuration-manager.md)을 참조하세요.

## <a name="windows-service"></a>Windows 서비스

Windows 서비스는 설치의 일부로 만들어집니다. **SQL Server Reporting Services**로 표시됩니다. 서비스 이름은 **SQLServerReportingServices**입니다.

## <a name="default-url-reservations"></a>기본 URL 예약

URL 예약은 접두사, 호스트 이름, 포트 및 가상 디렉터리로 구성됩니다.

|부분|Description|
|----------|-----------------|
|접두사|기본 접두사는 HTTP입니다. 이전에 SSL(Secure Sockets Layer) 인증서를 설치한 경우 설치 프로그램에서 HTTPS 접두사를 사용하는 URL 예약을 만들려고 시도합니다.|
|호스트 이름|기본 호스트 이름은 강력한 와일드카드(+)로서 보고서 서버가 `http://<computername>/reportserver`, `http://localhost/reportserver` 또는`http://<IPAddress>/reportserver.`를 포함하여 컴퓨터로 확인되는 모든 호스트 이름에 대해 지정된 포트에서 HTTP 요청을 수락하도록 지정합니다.|
|포트|기본 포트는 80입니다. 80 이외의 포트를 사용하는 경우 브라우저 창에서 웹 포털을 열 때 URL에 해당 포트를 명시적으로 추가해야 합니다.|
|가상 디렉터리|기본적으로 가상 디렉터리는 보고서 서버 웹 서비스의 경우 ReportServer 형식, 웹 포털의 경우 Reports 형식으로 만들어집니다. 보고서 서버 웹 서비스의 기본 가상 디렉터리는 **reportserver**이고 웹 포털의 기본 가상 디렉터리는 **reports**입니다.|

전체 URL 문자열의 예는 다음과 같습니다.

- `http://+:80/reportserver`, 보고서 서버에 대한 액세스를 제공합니다.

- `http://+:80/reports`, 웹 포털에 대한 액세스를 제공합니다.

## <a name="firewall"></a>방화벽

원격 컴퓨터에서 보고서 서버에 액세스하는 경우 방화벽이 있으면 모든 방화벽 규칙을 구성했는지 확인합니다.

웹 서비스 URL과 웹 포털 URL에 대해 구성된 TCP 포트를 열어야 합니다. 기본적으로 이는 TCP 포트 80에서 구성됩니다.

## <a name="additional-configuration"></a>기타 고려 사항

- 보고서 항목을 Power BI 대시보드에 고정할 수 있도록 Power BI 서비스와 통합을 구성하려면 [Power BI 서비스와 통합](power-bi-report-server-integration-configuration-manager.md)을 참조하세요.

- 구독 처리를 위해 전자 메일을 구성하려면 [전자 메일 설정](e-mail-settings-reporting-services-native-mode-configuration-manager.md) 및 [보고서 서버에서 전자 메일 배달](../subscriptions/e-mail-delivery-in-reporting-services.md)을 참조하세요.

- 원격 컴퓨터에서 액세스하여 보고서를 보고 관리할 수 있도록 웹 포털을 구성하려면 [보고서 서버 액세스를 위한 방화벽 구성](../report-server/configure-a-firewall-for-report-server-access.md) 및 [원격 관리를 위한 보고서 서버 구성](../report-server/configure-a-report-server-for-remote-administration.md)을 참조하세요.

## <a name="related-information"></a>관련 정보

SQL Server 2016 Reporting Services 기본 모드를 설치하는 방법에 대한 자세한 내용은 [Reporting Services 기본 모드 보고서 서버 설치](install-reporting-services-native-mode-report-server.md)를 참조하세요. SharePoint 통합 모드에서 SQL Server 2016 Reporting Services를 설치하는 방법에 대한 자세한 내용은 [SharePoint 모드에서 첫 번째 보고서 서버 설치](install-the-first-report-server-in-sharepoint-mode.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

설치된 보고서 서버를 사용하여 보고서를 만들고 보고서 서버에 배포하기를 시작합니다. 보고서 작성기 시작 방법에 대한 자세한 내용은 [보고서 작성기 설치](../../reporting-services/install-windows/install-report-builder.md)를 참조하세요.

SQL Server Data Tools를 사용하여 보고서를 만들려면 [SQL Server Data Tools를 다운로드합니다](http://go.microsoft.com/fwlink/?LinkID=616714).

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
