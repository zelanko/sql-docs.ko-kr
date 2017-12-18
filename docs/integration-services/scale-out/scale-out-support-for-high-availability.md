---
title: "고가용성에 대한 SSIS(SQL Server Integration Services) Scale Out 지원 | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2202b61a9efce26edb0edcef53204351338ecee6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="scale-out-support-for-high-availability"></a>고가용성에 대한 Scale Out 지원

SSIS Scale Out에서 작업자 쪽 고가용성은 여러 개의 Scale Out 작업자를 사용하여 패키지를 실행함으로써 제공됩니다.
마스터 쪽 고가용성은 [SSIS 카탈로그용 Always On](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) 및 Windows 장애 조치 클러스터를 사용하여 달성됩니다. Scale Out 마스터의 여러 인스턴스가 Windows 장애 조치 클러스터에서 호스팅됩니다. 주 노드에서 Scale Out 마스터 서비스 또는 SSISDB가 작동되지 않으면 보조 노드의 서비스 또는 SSISDB에서 계속하여 사용자 요청을 수락하고 Scale Out 작업자와 통신합니다. 

마스터 쪽 고가용성을 설정하려면 다음 단계를 수행합니다.

## <a name="1-prerequisites"></a>1. 필수 구성 요소
Windows 장애 조치(Failover) 클러스터를 설정합니다. 지침은 [Windows Server 2012용 장애 조치(Failover) 클러스터 기능 및 도구 설치](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) 블로그 게시물을 참조하세요. 모든 클러스터 노드에 기능 및 도구를 설치해야 합니다.

## <a name="2-install-scale-out-master-on-primary-node"></a>2. 주 노드에 Scale Out 마스터 설치
Scale Out 마스터의 주 노드에 데이터베이스 엔진 서비스, Integration Services 및 Scale Out 마스터를 설치합니다. 

설치하는 동안 다음을 수행해야 합니다. 
### <a name="21-set-the-account-running-scale-out-master-service-to-a-domain-account"></a>2.1 Scale Out 마스터 서비스를 실행하는 계정을 도메인 계정으로 설정합니다.
이 계정은 나중에 Windows 장애 조치 클러스터의 보조 노드에서 SSISDB에 액세스할 수 있어야 합니다. Scale Out 마스터 서비스 및 SSISDB에서 별도의 장애 조치를 수행할 수 있으므로 동일한 노드에 있지 않을 수 있습니다.

![HA 서버 구성](media/ha-server-config.PNG)

### <a name="22-include-scale-out-master-service-dns-host-name-in-the-cns-of-scale-out-master-certificate"></a>2.2 Scale Out 마스터 서비스 DNS 호스트 이름을 Scale Out 마스터 인증서의 CN에 포함합니다.

이 호스트 이름은 Scale Out 마스터 엔드포인트에서 사용됩니다. 

![HA 마스터 구성](media/ha-master-config.PNG)

## <a name="3-install-scale-out-master-on-secondary-node"></a>3. 보조 노드에 Scale Out 마스터 설치
Scale Out 마스터의 보조 노드에 데이터베이스 엔진 서비스, Integration Services 및 Scale Out 마스터를 설치합니다. 

주 노드와 동일한 Scale Out 마스터 인증서를 사용해야 합니다. 주 노드에서 개인 키를 사용하여 Scale Out 마스터 SSL 인증서를 내보내고, 보조 노드에 있는 로컬 컴퓨터의 루트 인증서 저장소에 설치합니다. Scale Out 마스터를 설치할 때 이 인증서를 선택합니다.

![HA 마스터 구성 2](media/ha-master-config2.PNG)

> [!Note]
> 보조 Scale Out 마스터에 대한 작업을 반복하여 여러 개의 백업 Scale Out 마스터를 설정할 수 있습니다.

## <a name="4-set-up-ssisdb-always-on"></a>4. SSISDB Always On 설정

SSISDB용 Always On을 설정하기 위한 지침은 [SSIS 카탈로그(SSISDB)용 Always On](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb)에서 참조할 수 있습니다.

또한 추가된 SSISDB 가용성 그룹에 대한 가용성 그룹 수신기를 만들어야 합니다. [가용성 그룹 수신기 만들기 또는 구성](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)을 참조하세요.

## <a name="5-update-scale-out-master-service-configuration-file"></a>5. Scale Out 마스터 서비스 구성 파일 업데이트
주 노드와 보조 노드에서 Scale Out 마스터 서비스 구성 파일(\<드라이버\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config)을 업데이트합니다. **SqlServerName**을 *[가용성 그룹 수신기 DNS 이름],[포트]*로 업데이트합니다.

## <a name="6-enable-package-execution-logging"></a>6. 패키지 실행 로깅 사용

SSISDB에서 로깅은 **##MS_SSISLogDBWorkerAgentLogin##** 로그인으로 수행되며, 이 로그인의 암호는 자동으로 생성됩니다. 모든 SSISDB 복제본에 대한 로깅을 만들려면 다음을 수행합니다.

### <a name="61-change-the-password-of-msssislogdbworkeragentlogin-on-primary-sql-server"></a>6.1 주 SQL Server에서 **##MS_SSISLogDBWorkerAgentLogin##**의 암호를 변경합니다.
### <a name="62-add-the-login-to-secondary-sql-server"></a>6.2 보조 SQL Server에 로그인을 추가합니다.
### <a name="63-update-connection-string-of-logging"></a>6.3 로깅 연결 문자열을 업데이트합니다.
다음을 사용하여 [catalog].[update_logdb_info] 저장 프로시저를 호출합니다. 

@server_name = '*[가용성 그룹 수신기 DNS 이름],[포트]*' 및 

@connection_string = 'Data Source=*[가용성 그룹 수신기 DNS 이름]*,*[포트]*;Initial Catalog=SSISDB;User Id=##MS_SSISLogDBWorkerAgentLogin##;Password=*[암호]*];'

## <a name="7-congifure-scale-out-master-service-role-of-windows-failover-cluster"></a>7. Windows 장애 조치 클러스터의 Scale Out 마스터 서비스 역할 구성

장애 조치 클러스터 관리자에서 Scale Out용 클러스터에 연결합니다. 클러스터를 선택하고 메뉴에서 **작업**, **역할 구성...**을 차례로 클릭합니다.

**고가용성 마법사**가 표시되면 **역할 선택** 페이지에서 **일반 서비스**를 선택하고, **서비스 선택** 페이지에서 SQL Server Integration Services Scale Out 마스터 14.0을 선택합니다.

**클라이언트 액세스 지점** 페이지에서 Scale Out 마스터 서비스 DNS 호스트 이름을 입력합니다.

![HA 마법사 1](media/ha-wizard1.PNG)

마법사를 마칩니다.

## <a name="8-update-master-address-in-ssisdb"></a>8. SSISDB에서 마스터 주소 업데이트

주 SQL Server에서 @MasterAddress = N'https://[Scale Out 마스터 서비스 DNS 호스트 이름]:[마스트 포트]' 매개 변수를 사용하여 [SSIS].[catalog].[update_master_address] 저장 프로시저를 실행합니다. 

## <a name="9-add-scale-out-worker"></a>9. Scale Out 작업자 추가

이제 [Scale Out 관리자](integration-services-ssis-scale-out-manager.md)를 통해 Scale Out 작업자를 추가할 수 있습니다. 연결 페이지에서 *[SQL Server 가용성 그룹 수신기 DNS 이름]*,*[포트]*를 입력합니다.




