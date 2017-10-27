---
title: "SQL Server Reporting Services 설치 | Microsoft Docs"
ms.date: 10/10/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 52c2f8fae79884b025e067b7d628cd3154ba93f4
ms.openlocfilehash: 5ce83ff18d6908441a3eaaf05599068ec5876308
ms.contentlocale: ko-kr
ms.lasthandoff: 10/10/2017

---
# <a name="install-sql-server-reporting-services"></a>SQL Server Reporting Services 설치

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

SQL Server Reporting Services 설치에는 보고서 항목을 저장 하면 보고서를 렌더링 하 고 구독 및 기타 보고서 서비스 처리를 위한 서버 구성 요소가 포함 됩니다.  Power BI 보고서 서버를 설치 하는 방법에 알아봅니다.

SQL Server 2017 Reporting Services를 다운로드 하려면로 이동 된 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=55252)합니다.

> [!NOTE]
> Power BI 보고서 서버를 찾고 있나요? 참조 [Power BI 보고서 서버 설치](https://powerbi.microsoft.com/documentation/reportserver-install-report-server/)합니다.

## <a name="before-you-begin"></a>시작하기 전 주의 사항

Reporting Services를 설치 하기 전에 검토는 [SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)합니다.

## <a name="install-your-report-server"></a>보고서 서버 설치

보고서 서버를 설치 하는 단순 합니다. 파일을 설치 하는 간단한 단계가 있습니다.

> [!NOTE]
> 설치 시 사용 가능한 SQL Server 데이터베이스 엔진 서버가 필요가 없습니다. 설치 후 Reporting Services를 구성 하려면 하나 필요 합니다.

1. SQLServerReportingServices.exe의 위치를 찾아 설치 관리자를 시작 합니다.

2. 선택 **Reporting Services 설치**합니다.

    ![Reporting Services 설치](media/install-reporting-services/report-server-install.png)

3. 설치 하 여 다음 선택 버전 **다음**합니다.

    ![버전 선택](media/install-reporting-services/report-server-install-edition.png)

    아래로 드롭다운에서 Evaluation 또는 Developer 버전을 선택할 수 있습니다.

    ![Evaluation 또는 developer edition](media/install-reporting-services/report-server-install-edition-select.png)

    그렇지 않은 경우 제품 키를 입력할 수 있습니다.

4. 읽기 및 사용 약관 및 조건에 동의 선택한 후 **다음**합니다.

5. 보고서 서버 데이터베이스를 저장할 수 있는 데이터베이스 엔진이 필요 합니다. 선택 **다음** 만 보고서 서버를 설치 합니다.

    ![데이터베이스를 설치 하는 데 필요 하지](media/install-reporting-services/report-server-install-db-engine.png)

6. 보고서 서버에 대 한 설치 위치를 지정 합니다. 선택 **설치** 를 계속 합니다.

    ![설치 경로 지정 합니다.](media/install-reporting-services/report-server-install-file-path.png)

    > [!NOTE]
    > 기본 경로 C:\Program Files\Microsoft SQL Server Reporting Services.

7. 성공적으로 설치 후에 선택 **보고서 서버 구성** 를 Reporting Services 구성 관리자를 시작 합니다.

    ![보고서 서버 구성](media/install-reporting-services/report-server-install-configure.png)

## <a name="configuration-your-report-server"></a>구성 보고서 서버

선택한 후 **보고서 서버 구성** 는 설치 프로그램에서 나타납니다와 **보고서 서버 구성 관리자**합니다. 자세한 내용은 참조 [보고서 서버 구성 관리자](reporting-services-configuration-manager-native-mode.md)합니다.

해야 [보고서 서버 데이터베이스 만들기](ssrs-report-server-create-a-report-server-database.md) Reporting Services의 초기 구성을 완료 합니다. 이 단계를 완료 하는 SQL Server 데이터베이스 서버에 필요 합니다.

### <a name="creating-a-database-on-a-different-server"></a>다른 서버에 데이터베이스 만들기

다른 컴퓨터에 데이터베이스 서버에서 보고서 서버 데이터베이스를 만드는 경우 데이터베이스 서버에서 인식 하는 자격 증명에 보고서 서버에 대 한 서비스 계정을 변경 해야 합니다.

기본적으로 보고서 서버에는 가상 서비스 계정을 사용합니다. 다른 서버에 데이터베이스를 만들려고 하는 경우에 적용 연결 권한 단계에 대해 다음 오류가 나타날 수 있습니다.

`System.Data.SqlClient.SqlException (0x80131904): Windows NT user or group '(null)' not found. Check the name again.`

이 오류를 해결 하려면 서비스 계정을 도메인 계정 또는 네트워크 서비스를 변경할 수 있습니다. 네트워크 서비스에 서비스 계정 변경 보고서 서버에 대 한 컴퓨터 계정의 컨텍스트에서 권한을 적용 합니다.

자세한 내용은 참조 [보고서 서버 서비스 계정 구성](configure-the-report-server-service-account-ssrs-configuration-manager.md)합니다.

## <a name="windows-service"></a>Windows 서비스

Windows 서비스는 설치의 일부로 만들어집니다. 로 표시 **SQL Server Reporting Services**합니다. 서비스 이름은 **SQLServerReportingServices**합니다.

## <a name="default-url-reservations"></a>기본 URL 예약

URL 예약은 접두사, 호스트 이름, 포트 및 가상 디렉터리로 구성됩니다.

|부분|설명|
|----------|-----------------|
|접두사|기본 접두사는 HTTP입니다. (SECURE Sockets Layer) 인증서를 이전에 설치한 경우 설치 프로그램이 HTTPS 접두사를 사용 하는 URL 예약을 만들려고 시도 합니다.|
|호스트 이름|기본 호스트 이름은 강력한 와일드카드(+)로서 보고서 서버가 컴퓨터로 확인 되는 모든 호스트 이름에 대해 지정된 된 포트에서 HTTP 요청을 수락 지정 포함 하 여 `http://<computername>/reportserver`, `http://localhost/reportserver`, 또는`http://<IPAddress>/reportserver.`|
|포트|기본 포트는 80입니다. 포트 80 이외의 포트를 사용 하는 경우 명시적으로 브라우저 창에서 웹 포털을 열 때 URL에 추가 해야 합니다.|
|가상 디렉터리|기본적으로 형식의 ReportServer는 보고서 서버 웹 서비스 및 보고서에 대 한 웹 포털에 대 한 가상 디렉터리가 만들어집니다. 보고서 서버 웹 서비스의 기본 가상 디렉터리는 **reportserver**이고 웹 포털의 기본 가상 디렉터리는 **보고서**합니다.|

전체 URL 문자열의 예는 다음과 같습니다.

- `http://+:80/reportserver`보고서 서버에 대 한 액세스를 제공 합니다.

- `http://+:80/reports`를 웹 포털에 대 한 액세스를 제공 합니다.

## <a name="firewall"></a>방화벽

원격 컴퓨터에서 보고서 서버를 액세스 하면 하려는 경우에 방화벽이 있는 경우 모든 방화벽 규칙을 구성 했는지 확인 합니다.

웹 서비스 URL과 웹 포털 URL에 대해 구성 된 TCP 포트를 열어야 할 했습니다. 이러한 경로 기본적으로 TCP 포트 80에 구성 됩니다.

## <a name="additional-configuration"></a>기타 고려 사항

- Power BI 대시보드에 보고서 항목을 고정할 수 있도록 Power BI 서비스와 통합을 구성 하려면 참조 [Power BI 서비스와 통합](power-bi-report-server-integration-configuration-manager.md)합니다.

- 구독 처리를 위해 전자 메일을 구성 하려면 참조 [전자 메일 설정](e-mail-settings-reporting-services-native-mode-configuration-manager.md) 및 [전자 메일 배달 보고서 서버에서](../subscriptions/e-mail-delivery-in-reporting-services.md)합니다.

- 보고서 보기 및 관리 하려면 원격 컴퓨터에서 액세스할 수 있도록 웹 포털을 구성 하려면 참조 [보고서 서버 액세스를 위한 방화벽 구성](../report-server/configure-a-firewall-for-report-server-access.md) 및 [원격 관리를 위한 보고서 서버 구성](../report-server/configure-a-report-server-for-remote-administration.md) .

## <a name="related-information"></a>관련 정보

SQL Server 2016 Reporting Services 기본 모드 설치 하는 방법에 대 한 정보를 참조 하십시오. [Install Reporting Services 기본 모드 보고서 서버](install-reporting-services-native-mode-report-server.md)합니다. SharePoint 통합 모드에서 SQL Server 2016 Reporting Services를 설치 하는 방법에 대 한 정보를 참조 하십시오. [SharePoint 모드에서 첫 번째 보고서 서버 설치](install-the-first-report-server-in-sharepoint-mode.md)합니다.

## <a name="next-steps"></a>다음 단계

설치 된 보고서 서버에 보고서를 만들고 보고서 서버에 해당 인터페이스를 배포 하기 시작 합니다. 보고서 작성기로 시작 하는 방법에 대 한 정보를 참조 하십시오. [보고서 작성기 설치](../../reporting-services/install-windows/install-report-builder.md)합니다.

SQL Server Data Tools를 사용 하 여 보고서를 만들려면 [SQL Server Data Tools 다운로드](http://go.microsoft.com/fwlink/?LinkID=616714)합니다.

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)

