---
title: 고가용성에 대한 SSIS(SQL Server Integration Services) Scale Out 지원 | Microsoft Docs
description: 이 문서에서는 고가용성에 대한 SSIS Scale Out 구성 방법 설명
ms.custom: performance
ms.date: 05/23/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
manager: craigg
ms.openlocfilehash: 53fc11dc3735f1a27401164044c452a038c9c0ce
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47594772"
---
# <a name="scale-out-support-for-high-availability"></a>고가용성에 대한 Scale Out 지원

SSIS Scale Out에서 여러 Scale Out 작업자를 사용하여 패키지를 실행함으로써 Scale Out 작업자 쪽에 고가용성을 제공할 수 있습니다.

Scale Out 마스터 쪽 고가용성은 [SSIS 카탈로그용 Always On](../catalog/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) 및 Windows 장애 조치(failover) 클러스터링을 사용하여 구현됩니다. 이 솔루션에서는 Scale Out 마스터의 여러 인스턴스가 Windows 장애 조치(failover) 클러스터에서 호스팅됩니다. 주 노드에서 Scale Out 마스터 서비스 또는 SSISDB가 작동되지 않으면 보조 노드의 서비스 또는 SSISDB에서 계속하여 사용자 요청을 수락하고 Scale Out 작업자와 통신합니다.

또는 SQL Server 장애 조치(failover) 클러스터 인스턴스로 Scale Out 마스터 쪽에서 고가용성을 구현할 수 있습니다. [SQL Server 장애 조치(failover) 클러스터 인스턴스를 통한 고가용성을 위한 Scale Out 지원](scale-out-failover-cluster-instance.md)을 참조하세요.

SSIS 카탈로그에 Always On을 사용하려면 Scale Out 마스터 쪽에 고가용성을 설정하려면 다음 작업을 수행합니다.

## <a name="1-prerequisites"></a>1. 사전 요구 사항
Windows 장애 조치(Failover) 클러스터를 설정합니다. 지침은 [Windows Server 2012용 장애 조치(Failover) 클러스터 기능 및 도구 설치](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) 블로그 게시물을 참조하세요. 모든 클러스터 노드에 기능 및 도구를 설치합니다.

## <a name="2-install-scale-out-master-on-the-primary-node"></a>2. 주 노드에 Scale Out 마스터 설치
Scale Out 마스터의 주 노드에 SQL Server 데이터베이스 엔진 서비스, Integration Services 및 Scale Out 마스터를 설치합니다. 

설치하는 동안 다음과 같은 작업을 수행합니다.

### <a name="21-set-the-account-running-scale-out-master-service-to-a-domain-account"></a>2.1 Scale Out 마스터 서비스를 실행하는 계정을 도메인 계정으로 설정
이 계정은 나중에 Windows 장애 조치 클러스터의 보조 노드에서 SSISDB에 액세스할 수 있어야 합니다. Scale Out 마스터 서비스 및 SSISDB에서 별도의 장애 조치를 수행할 수 있으므로 장애 조치 이후 동일한 노드에 있지 않을 수 있습니다.

![HA 서버 구성](media/ha-server-config.PNG)

### <a name="22-include-the-dns-host-name-for-the-scale-out-master-service-in-the-cns-of-the-scale-out-master-certificate"></a>2.2 Scale Out 마스터 서비스 DNS 호스트 이름을 Scale Out 마스터 인증서의 CN에 포함

이 호스트 이름은 Scale Out 마스터 엔드포인트에서 사용됩니다. (서버 이름이 아닌 DNS 호스트 이름을 제공하는지 확인합니다.)

![HA 마스터 구성](media/ha-master-config.PNG)

## <a name="3-install-scale-out-master-on-the-secondary-node"></a>3. 보조 노드에 Scale Out 마스터 설치
Scale Out 마스터의 보조 노드에 SQL Server 데이터베이스 엔진 서비스, Integration Services 및 Scale Out 마스터를 설치합니다. 

주 노드에 보낸 것과 동일한 Scale Out 마스터 인증서를 사용합니다. 주 노드에서 개인 키를 사용하여 Scale Out 마스터 SSL 인증서를 내보내고, 보조 노드에서 로컬 컴퓨터의 루트 인증서 저장소에 설치합니다. 보조 노드에서 Scale Out 마스터를 설치할 때 이 인증서를 선택합니다.

![HA 마스터 구성 2](media/ha-master-config2.PNG)

> [!NOTE]
> 다른 보조 노드에서 Scale Out 마스터에 이러한 작업을 반복하여 여러 개의 백업 Scale Out 마스터를 설정할 수 있습니다.

## <a name="4-set-up-and-configure-ssisdb-support-for-always-on"></a>4. Always On에 대한 SSISDB 지원 설정 및 구성

[SSIS 카탈로그(SSISDB)용 Always On](../catalog/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb)에서 Always On에 대한 SSISDB 지원을 설정하고 구성하기 위한 지침을 따릅니다.

또한 SSISDB를 추가한 가용성 그룹의 가용성 그룹 수신기를 만들어야 합니다. [가용성 그룹 수신기 만들기 또는 구성](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)을 참조하세요.

## <a name="5-update-the-scale-out-master-service-configuration-file"></a>5. Scale Out 마스터 서비스 구성 파일 업데이트
기본 및 보조 노드에서 Scale Out 마스터 서비스 구성 파일 `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config`를 업데이트합니다. **SqlServerName**을 *[가용성 그룹 수신기 DNS 이름],[포트]* 로 업데이트합니다.

## <a name="6-enable-package-execution-logging"></a>6. 패키지 실행 로깅 사용

SSISDB에서 로깅은 **##MS_SSISLogDBWorkerAgentLogin##** 로그인으로 수행되며, 이 로그인의 암호는 자동으로 생성됩니다. 모든 SSISDB 복제본에 대한 로깅을 만들려면 다음을 수행합니다.

### <a name="61-change-the-password-of-msssislogdbworkeragentlogin-on-the-primary-sql-server"></a>6.1 주 SQL Server에서 **##MS_SSISLogDBWorkerAgentLogin##** 의 암호 변경

### <a name="62-add-the-login-to-the-secondary-sql-server"></a>6.2 보조 SQL Server에 로그인 추가

### <a name="63-update-the-connection-string-used-for-logging"></a>6.3 로깅에 사용되는 연결 문자열 업데이트.
다음 매개 변수 값을 사용하여 저장 프로시저 `[catalog].[update_logdb_info]`를 호출합니다.

-   `@server_name = '[Availability Group Listener DNS name],[Port]' `

-   `@connection_string = 'Data Source=[Availability Group Listener DNS name],[Port];Initial Catalog=SSISDB;User Id=##MS_SSISLogDBWorkerAgentLogin##;Password=[Password]];'`

## <a name="7-configure-the-scale-out-master-service-role-of-the-windows-server-failover-cluster"></a>7. Windows Server 장애 조치(failover) 클러스터의 Scale Out 마스터 서비스 역할 구성

1.  장애 조치(Failover) 클러스터 관리자에서 Scale Out용 클러스터에 연결합니다. 클러스터를 선택합니다. 메뉴에서 **동작**을 선택한 후 **역할 구성**을 선택합니다.

2.  **고가용성 마법사** 대화 상자의 **역할 선택** 페이지에서 **일반 서비스**를 선택합니다. **서비스 선택** 페이지에서 SQL Server Integration Services Scale Out 마스터 14.0을 선택합니다.

3.  **클라이언트 액세스 지점** 페이지에서 Scale Out 마스터 서비스 DNS 호스트 이름을 입력합니다.

    ![HA 마법사 1](media/ha-wizard1.PNG)

4.  마법사를 마칩니다.

Azure 가상 머신에서 이 구성 단계는 추가 단계가 필요합니다. 이러한 개념 및 이러한 단계에 대한 자세한 설명은 이 문서의 범위를 벗어납니다.

1.  Azure 도메인을 설정해야 합니다. Windows Server 장애 조치(failover) 클러스터링은 클러스터의 모든 구성 요소가 동일한 도메인의 구성원이 될 것을 요구합니다. 자세한 내용은 [Azure Portal을 사용하여 Azure Active Directory Domain Services 활성화](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-getting-started)를 참조합니다.

2. Azure 부하 분산 장치를 설정해야 합니다. 가용성 그룹 수신기에 대한 요구 사항입니다. 자세한 내용은 [자습서: Azure Portal을 사용하여 VM에 Basic Load Balancer와 함께 내부 트래픽 부하 분산](https://docs.microsoft.com/azure/load-balancer/tutorial-load-balancer-basic-internal-portal)을 참조합니다.

## <a name="8-update-the-scale-out-master-address-in-ssisdb"></a>8. SSISDB에서 Scale Out 마스터 주소 업데이트

기본 SQL Server에서 매개 변수 값 `@MasterAddress = N'https://[Scale Out Master service DNS host name]:[Master Port]'`를 사용하여 저장 프로시저 `[catalog].[update_master_address]`를 실행합니다. 

## <a name="9-add-the-scale-out-workers"></a>9. Scale Out 작업자 추가

이제 [Integration Services Scale Out 관리자](integration-services-ssis-scale-out-manager.md)를 통해 Scale Out 작업자를 추가할 수 있습니다. 연결 페이지에서 `[SQL Server Availability Group Listener DNS name],[Port]`를 입력합니다.

# <a name="upgrade-scale-out-in-high-availability-environment"></a>고가용성 환경에서 Scale Out 업그레이드
고가용성 환경에서 Scale Out을 업그레이드하려면 [SSIS 카탈로그용 Always On의 업그레이드 단계](../catalog/ssis-catalog.md#Upgrade)를 따르고, 각 머신에서 Scale Out 마스터와 Scale Out 작업자를 업그레이드 하고, Scale Out 마스터 서비스의 새 버전으로 7단계 위에 Windows Server 장애 조치(failover) 클러스터 역할을 다시 만듭니다.

## <a name="next-steps"></a>다음 단계
자세한 내용은 다음 문서를 참조하세요.
-   [Integration Services(SSIS) Scale Out 마스터](integration-services-ssis-scale-out-master.md)
-   [Integration Services(SSIS) Scale Out 작업자](integration-services-ssis-scale-out-worker.md)
