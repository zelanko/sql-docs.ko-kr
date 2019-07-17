---
title: Reporting Services SharePoint 서비스 애플리케이션 관리 | Microsoft Docs
ms.date: 10/05/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 6e1b69fc176281e9be65ca7a9766fc8fb270a3de
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580084"
---
# <a name="manage-a-reporting-services-sharepoint-service-application"></a>Reporting Services SharePoint 서비스 애플리케이션 관리

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션은 SharePoint 중앙 관리에서 관리됩니다. 관리 및 속성 페이지에서 서비스 애플리케이션의 구성과 일반 관리 태스크를 업데이트할 수 있습니다.  

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.

## <a name="open-service-application-properties-page"></a>서비스 애플리케이션 속성 페이지 열기

 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션에 대한 속성 페이지를 열려면 다음을 완료합니다.  
  
1.  중앙 관리의 애플리케이션 관리 그룹에서 **서비스 애플리케이션 관리**를 클릭합니다.  
  
2.  서비스 애플리케이션 이름 근처를 클릭하거나 **유형** 열을 클릭하여 전체 행을 선택하고 SharePoint 리본에서 **속성** 을 클릭합니다.  
  
 서비스 애플리케이션 속성에 대한 자세한 내용은 [Step 3: Create a Reporting Services Service Application](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md#bkmk_create_serrviceapplication)을 참조하세요.  
  
## <a name="open-service-application-management-pages"></a>서비스 애플리케이션 관리 페이지 열기

 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션에 대한 관리 페이지를 열려면 다음을 완료합니다.  
  
1.  중앙 관리의 애플리케이션 관리 그룹에서 **서비스 애플리케이션 관리**를 클릭합니다.  
  
2.  서비스 애플리케이션 이름을 클릭하면 **Reporting Services 애플리케이션 관리** 페이지가 열립니다.  
  
3.  또는 서비스 애플리케이션의 이름 근처를 클릭하거나 **유형** 열을 클릭하여 전체 행을 선택한 다음 SharePoint 리본에서 **관리** 를 클릭할 수 있습니다.  
  
## <a name="system-settings-page"></a>시스템 설정 페이지

 시스템 설정 페이지에서 다양한 제한 시간을 포함하여 서비스 애플리케이션의 동작과 사용자 환경을 구성할 수 있습니다.
  
### <a name="report-settings"></a>보고서 설정
  
|설정|주석|  
|-------------|--------------|  
|외부 이미지 제한 시간|기본값은 600초입니다.|  
|스냅샷 압축|기본값은 SQL입니다.|  
|시스템 보고서 제한 시간|기본값은 1800초입니다.<br /><br /> 보고서 서버에서 보고서 처리를 일정 시간(초)으로 제한할지 여부를 지정합니다. 이 값은 보고서 서버의 보고서 처리에 적용되며, 사용자의 보고서에 데이터를 제공하는 데이터베이스 서버의 데이터 처리에는 영향을 주지 않습니다. 보고서 처리 시간은 보고서를 선택한 후 보고서가 열리는 데 걸리는 시간입니다. 데이터 처리 및 보고서 처리를 모두 완료하기에 충분한 값을 지정해야 합니다.|  
|시스템 스냅샷 제한|기본값은 -1(제한 없음)입니다.<br /><br /> 보관할 보고서 기록 복사본 수에 대한 사이트 전체 기본값을 설정합니다. 이 기본값은 각 보고서에 대해 저장할 수 있는 스냅샷 수를 설정하는 초기 설정이 됩니다. 특정 보고서에 대해 속성 페이지에서 다른 제한값을 지정할 수 있습니다.|  
|저장된 매개 변수 수명|기본값은 180입니다.|  
|저장된 매개 변수 임계값|기본값은 1500일입니다.|  
  
### <a name="session-settings"></a>세션 설정
  
|설정|주석|  
|-------------|--------------|  
|세션 제한 시간|기본값은 600초입니다.|  
|세션 쿠키 사용|기본값은 TRUE입니다.|  
|EDLX 보고서 제한 시간|기본값은 1800초입니다.|  
  
### <a name="system-settings-for-logging"></a>로깅에 대한 시스템 설정
  
|설정|주석|  
|-------------|--------------|  
|실행 로깅 사용|기본값은 TRUE입니다.<br /><br /> 보고서 서버에서 추적 로그를 생성할지 여부와 로그를 보관할 일 수를 지정합니다. 를 클릭합니다. 로그는 보고서 서버 컴퓨터의 \Microsoft SQL Server\MSSQL.n\ReportServer\Log 폴더에 저장됩니다. 서비스가 다시 시작될 때마다 새 로그 파일이 시작됩니다. 로그 파일에 대한 자세한 내용은 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)를 참조하세요.|  
|실행 로그 보관 일 수|기본값은 60일입니다.|  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 SharePoint ULS 로깅을 지원합니다.  자세한 내용은 [SharePoint 추적 로그에 대한 Reporting Services 이벤트 설정&#40;ULS&#41;](../../reporting-services/report-server/turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)  
  
### <a name="security-settings"></a>보안 설정
  
|설정|주석|  
|-------------|--------------|  
|통합 보안 사용|기본값은 TRUE입니다.<br /><br /> 보고서를 요청한 사용자의 Windows 보안 토큰을 사용하여 보고서 데이터 원본에 연결할 수 있는지 여부를 지정합니다.|  
|보고서 정의 로드 사용|기본값은 TRUE입니다.|  
|원격 오류 사용|기본값은 FALSE입니다.|  
|테스트 연결 자세한 오류 사용|기본값은 TRUE입니다.|  
  
### <a name="client-settings"></a>클라이언트 설정
  
|설정|주석|  
|-------------|--------------|  
|보고서 작성기 다운로드 사용|기본값은 TRUE입니다.<br /><br /> 클라이언트가 보고서 작성기 애플리케이션을 다운로드하기 위한 단추를 볼 수 있는지 여부를 지정합니다.|  
|보고서 작성기 시작 URL|보고서 서버에서 기본 보고서 작성기 URL을 사용하지 않는 경우에는 사용자 지정 URL을 지정합니다. 이 설정은 선택 사항입니다. 값을 지정하지 않으면 기본 URL이 사용되어 보고서 작성기가 시작됩니다. 보고서 작성기 3.0을 한 번 클릭 애플리케이션으로 시작하려면 https://\<computername>/ReportServer/ReportBuilder/ReportBuilder_3_0_0_0.application 값을 입력합니다.|  
|클라이언트 인쇄 기능 사용|기본값은 TRUE입니다.<br /><br /> 사용자가 인쇄 옵션을 제공 하는 클라이언트 쪽 컨트롤을 다운로드할 수 있는지 여부를 지정합니다.|  
|세션 제한 시간 편집|기본값은 7200초입니다.|  
|세션 캐시 제한 편집|기본값은 5입니다.|  
  
## <a name="manage-jobs"></a>작업 관리

 보고서 구독과 데이터 기반 구독에서 만들어진 작업과 같은 실행 중인 작업을 보고 삭제할 수 있습니다. 이 페이지는 구독을 관리하는 데 사용되지 않으며 구독에서 트리거된 작업을 관리하는 데 사용됩니다. 예를 들어 1시간에 한 번 실행되도록 예약된 구독은 **작업 관리** 페이지에 나타나는 작업을 1시간에 한 번 생성합니다.  
  
 ![실행 중인 작업 관리](../../reporting-services/report-server-sharepoint/media/ssrs-manage-jobs.gif "실행 중인 작업 관리")  
  
## <a name="key-management"></a>키 관리
 다음 표에는 키 관리 페이지가 요약되어 있습니다.  
  
> [!IMPORTANT]  
>  Reporting Services 암호화 키를 주기적으로 변경하는 것은 최상의 보안 권장 방법입니다. Reporting Services의 중요 버전 업그레이드 직후에 키를 변경하는 것이 가장 좋습니다. 업그레이드 후에 키를 변경하면 업그레이드 주기를 벗어나 Reporting Services 암호화 키를 변경할 경우에 발생하는 추가 서비스 중단이 최소화됩니다.  
  
|호출|설명|  
|----------|-----------------|  
|암호화 키 백업|1) **암호:** 상자와 **암호 확인:** 상자에 암호를 입력하고 **내보내기**를 클릭합니다. 입력한 암호가 도메인 정책의 복잡성 요구 사항을 충족하지 않으면 경고가 표시됩니다.<br /><br /> 2) 키 파일을 저장할 파일 위치를 묻는 메시지가 나타납니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 실행 중인 컴퓨터와 별도의 컴퓨터에 키 파일을 저장해야 합니다. 기본 파일 이름은 서비스 애플리케이션의 이름과 동일합니다.|  
|암호화 키 복원|1) **파일 위치** 상자에서 키 파일을 입력하거나 해당 위치를 찾습니다.<br /><br /> 2) **암호** 상자에 암호화 파일을 백업하는 데 사용된 암호를 입력합니다.<br /><br /> 3) **확인**을 클릭합니다.|  
|암호화 키 변경|이 작업에서는 새 키를 만들고 암호화된 내용을 다시 암호화합니다. 내용이 많은 경우 이 작업을 수행하는 데 몇 시간이 걸릴 수 있습니다.<br /><br /> 암호화 키 변경 작업이 완료되면 새 키를 백업하는 것이 좋습니다.|  
|삭제된 암호화된 내용|삭제된 내용을 복구할 수 없습니다.<br /><br /> **\*\* 중요 \*\*** 대칭 키 삭제 및 다시 만들기 동작은 되돌리거나 실행 취소할 수 없습니다. 키를 삭제 또는 다시 만들기는 현재 설치에 중요한 결과를 가져올 수 있습니다. 키를 삭제하면 대칭 키로 암호화된 모든 기존 데이터도 삭제됩니다. 삭제된 데이터에는 외부 보고서 데이터 원본에 대한 연결 문자열, 저장된 연결 문자열 및 일부 구독 정보가 포함되어 있습니다.|  

## <a name="execution-account"></a>실행 계정

 이 페이지를 사용하여 무인 모드 처리용으로 사용할 계정을 구성할 수 있습니다. 이 계정은 다음과 같이 다른 자격 증명 원본을 사용할 수 없는 특별한 환경에서 사용됩니다.  
  
-   보고서 서버가 자격 증명이 필요 없는 데이터 원본에 연결하는 경우 자격 증명이 필요 없는 데이터 원본의 예로는 XML 문서와 일부 클라이언트 쪽 애플리케이션이 있습니다.  
  
-   보고서 서버가 보고서에서 참조하는 외부 이미지 파일 또는 기타 리소스를 검색하기 위해 다른 서버에 연결하는 경우  

 이 계정 설정은 선택 사항이지만 설정하지 않은 경우 외부 이미지 및 일부 데이터 원본에 대한 연결을 사용하는 데 제한이 따릅니다. 외부 이미지 파일을 검색할 때 보고서 서버는 익명 연결을 설정할 수 있는지 여부를 확인합니다. 연결이 암호로 보호된 경우 보고서 서버는 무인 보고서 처리 계정을 사용하여 원격 서버에 연결합니다. 보고서에 대한 데이터를 검색할 때 데이터 원본 연결이 자격 증명 유형을 **없음** 으로 지정한 경우 보고서 서버는 현재 사용자를 가장하거나, 사용자에게 자격 증명을 요청하거나, 저장된 자격 증명을 사용하거나, 무인 처리 계정을 사용합니다. 보고서 서버는 다른 컴퓨터에 연결할 때 해당 서비스 계정 자격 증명을 위임 또는 가장할 수 없으므로 사용 가능한 다른 자격 증명이 없는 경우 무인 처리 계정을 사용해야 합니다.  

 서비스 계정을 실행하는 데 사용되는 계정과 다른 계정을 지정해야 합니다. 스케일 아웃 배포에서 보고서 서버를 실행하는 경우 이 계정은 각 보고서 서버에서 같은 방식으로 구성해야 합니다.  

 Windows 사용자 계정을 사용할 수 있습니다. 최상의 결과를 얻으려면 다른 컴퓨터와의 연결을 지원하는 네트워크 로그온 권한과 읽기 권한을 가진 계정을 선택합니다. 보고서에서 사용하려는 모든 외부 이미지 또는 데이터 파일에 대해 읽기 권한을 갖고 있어야 합니다. 모든 보고서 데이터 원본과 외부 이미지가 보고서 서버 컴퓨터에 저장되어 있지 않으면 로컬 계정을 지정하지 마세요. 이 계정은 무인 보고서 처리에만 사용합니다.  

 ### <a name="powershell-command"></a>PowerShell 명령

 다음은 UEAccount 속성과 함께 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션의 목록을 반환하는 예제 PowerShell 명령입니다.  

```
Get-SPRSServiceApplication | select typename, name, service, ueaccountname  
```

 자세한 내용은 [Reporting Services SharePoint 모드용 PowerShell cmdlet](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)을 참조하세요.  

### <a name="options"></a>옵션

 **실행 계정 지정**  
 계정을 지정하려면 선택합니다.  
  
 **계정**  
 Windows 도메인 사용자 계정을 입력합니다. *\<domain>\\<user account\>* 형식을 사용합니다.  
  
 **암호**  
 암호를 입력합니다.  
  
 **암호 확인**  
 암호를 다시 입력합니다.  

## <a name="e-mail-settings"></a>전자 메일 설정

 이 페이지에서는 보고서 서버에서 보고서 서버 전자 메일 배달을 가능하게 하는 SMTP(Simple Mail Transport Protocol) 설정을 지정할 수 있습니다. 보고서 서버 전자 메일 배달 확장 프로그램을 사용하여 전자 메일 구독을 통해 보고서 또는 보고서 처리 알림을 배포할 수 있습니다. 보고서 서버 전자 메일 배달 확장 프로그램을 사용하려면 SMTP 서버 및 보낸 사람 주소: 필드에 사용할 전자 메일 주소가 필요합니다.  

### <a name="options"></a>옵션

 **SMTP 서버 사용**  
 보고서 서버 전자 메일이 SMTP 서버를 통해 라우팅되도록 지정합니다.  
  
 **아웃바운드 SMTP 서버**  
 사용할 SMTP 서버 또는 게이트웨이를 지정합니다. 네트워크에서 로컬 서버나 SMTP 서버를 사용할 수 있습니다.  
  
 **보낸 사람 주소**  
 생성된 전자 메일의 보낸 사람: 필드에 사용할 전자 메일 주소를 지정합니다. SMTP 서버에서 메일을 보낼 수 있는 권한이 있는 사용자 계정을 지정해야 합니다.  

## <a name="provision-subscriptions-and-alerts"></a>구독 및 경고 프로비전

 이 페이지를 사용하여 SQL Server 에이전트가 실행 중인지 확인하고 SQL Server 에이전트를 사용하도록 보고 서비스에 대한 액세스를 프로비전합니다. SQL Server 에이전트는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독, 일정 및 데이터 경고에 필요합니다. [SSRS 서비스 애플리케이션에 대한 구독 및 경고 프로비전](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  

## <a name="proxy-association"></a>프록시 연결

 Reporting Services 서비스 애플리케이션을 만들 때 Reporting Services 서비스 애플리케이션을 통해 액세스하기 위해 권한을 연결 및 프로비전할 웹 애플리케이션을 선택했습니다. 연결하지 않거나 연결을 변경하려면 다음 단계를 수행할 수 있습니다.  
  
1.  SharePoint 중앙 관리의 애플리케이션 관리에서 **서비스 애플리케이션 연결 구성**을 클릭합니다.  
  
2.  서비스 애플리케이션 연결 페이지에서 보기를 **서비스 애플리케이션**으로 변경합니다.  
  
3.  새 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션의 이름을 찾아서 클릭합니다. 또한 애플리케이션 프록시 그룹 이름인 **기본값** 을 클릭하여 다음 단계를 완료하는 대신 기본 그룹에 프록시를 추가할 수도 있습니다.  
  
4.  **다음 연결 그룹 편집** 선택 상자에서 **사용자 지정**을 선택합니다.  
  
5.  해당 프록시의 상자를 선택하고 **확인**클릭합니다.  
  
추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
