---
title: "SQL Server Integration Services (SSIS) 확장 Support for High Availability | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2405235bcfa09d2cc49e007f4eae6975d9ebf7a5
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="scale-out-support-for-high-availability"></a>고가용성에 대 한 범위 확장 지원

Out 눈금 SSIS에서 작업자 측 고가용성 여러 스케일 아웃 Worker를 사용 하 여 패키지 실행을 통해 제공 됩니다.
마스터 쪽 가용성을 높일 수 있는 [Always On SSIS 카탈로그에 대 한](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) 및 Windows 장애 조치 클러스터입니다. 스케일 아웃 마스터의 여러 인스턴스는 Windows 장애 조치 클러스터에 호스트 됩니다. 스케일 아웃 마스터 서비스나 SSISDB 주 노드에서 다운 된 경우 서비스 또는 보조 노드에서 SSISDB 계속 해 서 사용자 요청을 수락 하 고 스케일 아웃 작업자와 통신 합니다. 

마스터 쪽 고가용성을 설정 하려면 다음 단계를 수행 합니다.

## <a name="1-prerequisites"></a>1. 필수 구성 요소
Windows 장애 조치(Failover) 클러스터를 설정합니다. 지침은 [Windows Server 2012용 장애 조치(Failover) 클러스터 기능 및 도구 설치](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) 블로그 게시물을 참조하세요. 모든 클러스터 노드에 기능 및 도구를 설치해야 합니다.

## <a name="2-install-scale-out-master-on-primary-node"></a>2. 스케일 아웃 마스터 주 노드에서 설치
데이터베이스 엔진 서비스, Integration Services 및 스케일 아웃 마스터 스케일 아웃 Master에 대 한 주 노드에서 설치 합니다. 

설치 하는 동안 
### <a name="21-set-the-account-running-scale-out-master-service-to-a-domain-account"></a>2.1에는 스케일 아웃 마스터 서비스 계정을 도메인 계정으로 실행 하는 계정을 설정 합니다.
이 계정은 Windows 장애 조치 클러스터의 보조 노드에서 SSISDB를 나중에 액세스 할 수 있어야 합니다. 스케일 아웃 마스터 서비스와 SSISDB 장애 조치 별도로와 동일한 노드에서 하지 못할 수 있습니다.

![HA 서버 구성](media/ha-server-config.PNG)

### <a name="22-include-scale-out-master-service-dns-host-name-in-the-cns-of-scale-out-master-certificate"></a>2.2 스케일 아웃 마스터 포함 서비스 DNS 호스트 이름에서 Cn 스케일 아웃 마스터의 인증서입니다.

이 호스트 이름은 스케일 아웃 마스터 끝점에 사용 됩니다. 

![HA 마스터 구성](media/ha-master-config.PNG)

## <a name="3-install-scale-out-master-on-secondary-node"></a>3. 보조 노드에서 스케일 아웃 마스터를 설치 합니다.
데이터베이스 엔진 서비스, Integration Services 및 스케일 아웃 마스터 스케일 아웃 Master에 대 한 보조 노드에 설치 합니다. 

주 노드와 동일한 스케일 아웃 마스터 인증서를 사용 해야 합니다. 개인 키가 있는 주 노드에서 스케일 아웃 마스터 SSL 인증서를 내보내고 보조 노드에서 loacl 컴퓨터의 루트 인증서 저장소에 설치 합니다. 스케일 아웃 마스터를 설치할 때이 인증서를 선택 합니다.

![HA 마스터 구성 2](media/ha-master-config2.PNG)

> [!Note]
> 보조 스케일 아웃 마스터에 대 한 작업을 반복 하 여 여러 백업 스케일 아웃 마스터를 설정할 수 있습니다.

## <a name="4-set-up-ssisdb-always-on"></a>4. 항상 SSISDB를 설정

설치 하려면 항상에서 SSISDB를 볼 수 있습니다에 대 한 지침 [SSIS 카탈로그 (SSISDB)에 대 한 Always On](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb)합니다.

또한 가용성 그룹에 SSISDB 추가 대 한 가용성 gourp 수신기를 만들려면 해야 합니다. 참조 [가용성 그룹 수신기 만들기 또는 구성](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)합니다.

## <a name="5-update-scale-out-master-service-configuration-file"></a>5. 스케일 아웃 마스터 서비스 구성 파일 업데이트
서비스 구성 파일을 스케일 아웃 마스터 업데이트 \<드라이버\>: 기본 및 보조 노드에서 files\microsoft SQL Server\140\DTS\Binn\MasterSettings.config 합니다. 업데이트 **SqlServerName** 를 *[가용성 그룹 수신기 DNS 이름] [Port]*합니다.

## <a name="6-enable-package-execution-logging"></a>6. 패키지 실행 로깅 사용

로그인에서 이루어진다는 SSISDB 로그인 **# # MS_SSISLogDBWorkerAgentLogin # #**, 암호가 자동으로 생성 됩니다. SSISDB의 모든 복제본에 대 한 로깅 작동 하려면 다음을 수행 합니다.

### <a name="61-change-the-password-of-msssislogdbworkeragentlogin-on-primary-sql-server"></a>6.1의 암호를 변경 **# # MS_SSISLogDBWorkerAgentLogin # #** 주 Sql Server에 있습니다.
### <a name="62-add-the-login-to-secondary-sql-server"></a>6.2 보조 Sql Server에 로그인을 추가 합니다.
### <a name="63-update-connection-string-of-logging"></a>6.3 로깅의 연결 문자열을 업데이트 합니다.
[Catalog] 저장된 프로시저를 호출 합니다. [update_logdb_info]와 

@server_name= '*[가용성 그룹 수신기 DNS 이름] [Port]*' 

및 @connection_string = ' 데이터 원본 =*[가용성 그룹 수신기 DNS 이름]*,*[Port]*; Initial Catalog = SSISDB; 사용자 Id = # # MS_SSISLogDBWorkerAgentLogin # #. 암호 =*[Password]*];'.

## <a name="7-congifure-scale-out-master-service-role-of-windows-failover-cluster"></a>7. Windows 장애 조치 클러스터의 Congifure 스케일 아웃 마스터 서비스 역할

장애 조치 클러스터 관리자, 범위 확장에 대 한 클러스터에 연결 합니다. 클러스터를 선택 하 고 클릭 **동작** 메뉴에서 다음 **역할 구성 중...** .

꺼낸에서 **고가용성 마법사**선택, **일반 서비스** 에 **역할 선택** 페이지 하 고 SQL Server Integration Services 스케일 아웃 마스터 14.0에서 선택 **서비스 선택** 페이지.

에 **클라이언트 액세스 지점** 페이지에서 스케일 아웃 마스터 서비스 DNS 호스트 이름을 입력 합니다.

![HA 마법사 1](media/ha-wizard1.PNG)

마법사를 마칩니다.

## <a name="8-update-master-address-in-ssisdb"></a>8. 마스터 업데이트 SSISDB에 주소

기본 SQL Server에서 저장된 프로시저 [SSIS]를 실행 합니다. [catalog]입니다. [update_master_address] 매개 변수와 함께 @MasterAddress N'https =: / / [스케일 아웃 마스터 서비스 DNS 호스트 이름]: [마스터 포트]'. 

## <a name="9-add-scale-out-worker"></a>9. 작업자 확장 추가

이제, 사용 하 여 스케일 아웃 작업자를 추가할 수 있습니다 [스케일 아웃 관리자](integration-services-ssis-scale-out-manager.md)합니다. 입력 *[SQL Server 가용성 그룹 수신기 DNS 이름]*,*[Port]* 연결 페이지에 있습니다.





