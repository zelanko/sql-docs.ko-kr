---
title: 서버 구성-서비스 계정 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- service account configuration, SQL Server
ms.assetid: c283702d-ab20-4bfa-9272-f0c53c31cb9f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8435b0c677f80bf4f26acd4411d90ab63c7473d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092267"
---
# <a name="server-configuration---service-accounts"></a>서버 구성 - 서비스 계정
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사의 서버 구성 페이지에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 로그인 계정을 할당할 수 있습니다. 이 페이지에서 구성하는 실제 서비스는 사용자가 설치하도록 선택한 기능에 따라 달라집니다.  
  
 시작 하 고 실행 하는 데 사용 되는 시작 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] HYPERLINK "ms-help://SQL11_I1033/s11sq_GetStart_I/html/309b9dac-0b3a-4617-85ef-c4519ce9d014.htm" \l "Domain_User" 도메인 사용자 계정, 로컬 사용자 계정, 관리 되는 서비스 계정 수 가상 계정 또는 기본 제공 시스템 계정입니다.  
  
## <a name="options"></a>변수  
 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 동일한 로그인 계정을 할당하거나 각 서비스 계정을 따로 구성할 수 있습니다. 서비스 시작 유형을 자동 또는 수동으로 지정하거나 서비스의 해제 여부도 지정할 수 있습니다. 대부분의 설치에 기본 계정을 사용하는 것이 좋습니다.  
  
 Windows 7과 [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2에서는 대부분의 계정이 기본적으로 가상 계정으로 설정됩니다.  
  
 도메인 계정을 사용하도록 서비스를 구성한 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 은 서비스 계정을 개별적으로 구성하여 각 서비스에 대해 최소한의 권한을 제공하도록 권장합니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에는 태스크를 완료하는 데 필요한 최소한의 권한만 부여됩니다. 계정 유형 설명을 포함하여 자세한 내용은 [Configure Windows Service Accounts and Permissions](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하십시오.  
  
 **구성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정을 개별적으로 (권장)**  
 표를 사용하여 로그온 사용자 이름과 암호를 개별 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 제공하고 서비스 시작 유형을 설정할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에는 기본 제공 시스템 계정, 로컬 계정, 로컬 그룹, 도메인 그룹 또는 도메인 사용자 계정을 사용할 수 있습니다.  
  
 다음 서비스를 선택하여 해당 설정을 사용자 지정할 수 있습니다.  
  
|선택할 서비스|인증 설정을 구성할 서비스|  
|-------------------------|----------------------------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트|작업을 실행하고, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 모니터링하며, 관리 태스크의 자동화를 지원하는 서비스입니다.<br /><br /> 이 서비스에 대한 기본 로그온 계정이 없습니다.<br /><br /> 기본 시작 유형은 수동입니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|기본 시작 유형은 자동입니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|기본 시작 유형은 자동입니다.<br /><br /> SharePoint 통합 모드의 경우 Windows 도메인 사용자 계정을 지정해야 합니다. 지정한 계정은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스에 사용됩니다. 이후에 같은 팜에 추가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스를 추가할 때도 현재 인스턴스에 지정한 계정을 사용해야 합니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|서비스 계정은 보고서 서버 데이터베이스 연결을 구성하는 데 사용됩니다. 기본 인증 설정을 사용하려는 경우 기본 제공 네트워크 서비스를 선택합니다. 도메인 사용자 계정을 지정할 때 보고서 서버에서 Windows 인증을 사용하는 경우 해당 계정에 대한 SPN(서비스 사용자 이름)을 등록해야 합니다. 자세한 내용은 [Configure Windows Authentication on the Report Server](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)을 참조하세요.<br /><br /> 기본 시작 유형은 자동입니다.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 데이터 이동, 복사 및 변환을 위한 그래픽 도구 및 프로그래밍 가능 개체 집합입니다.<br /><br /> 기본 시작 유형은 자동입니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client|Distributed Replay Client 서비스에 사용되는 서비스 계정입니다.<br /><br /> Distributed Replay Client 서비스를 실행할 계정을 지정합니다. 이 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 사용하는 계정과 달라야 합니다.<br /><br /> 기본 시작 유형은 수동입니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller|Distributed Replay Controller 서비스에 사용되는 서비스 계정입니다.<br /><br /> Distributed Replay Controller 서비스를 실행할 계정을 지정합니다. 이 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 사용하는 계정과 달라야 합니다.<br /><br /> 기본 시작 유형은 수동입니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전체 텍스트 필터 데몬 시작 관리자|fdhost.exe 프로세스를 만드는 서비스입니다. 이 서비스는 전체 텍스트 인덱싱을 위해 텍스트 데이터를 처리하는 단어 분리기 및 필터를 호스팅하는 데 필요합니다.<br /><br /> FDHOST Launcher 서비스를 실행할 도메인 계정을 지정하는 경우에는 권한 수준이 낮은 계정을 사용하는 것이 좋습니다. 이 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 사용하는 계정과 달라야 합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser는 클라이언트 컴퓨터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 정보를 제공하는 이름 확인 서비스입니다. 이 서비스는 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 인스턴스에서 공유됩니다. 기본 로그온 계정은 NT Authority\Local 서비스이며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 도중에 변경할 수 없습니다. 이 계정은 설치가 완료된 다음에 변경할 수 있습니다. 시작 유형을 설치 중에 지정하지 않으면 다음과 같이 결정됩니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser가 자동으로 설정되어 다음에 설명된 설치 시나리오대로 실행됩니다.<br />-<br />                            [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스<br />-<br />                            TCP 또는 NP 설정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 명명된 인스턴스<br />-<br />                            Analysis Server의 명명된 인스턴스(클러스터링되지 않음)<br /><br /> 위의 시나리오에 해당되지 않는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser가 이미 설치되어 있다면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser의 현재 상태가 유지됩니다.<br /><br /> 설치하기 전에 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전의 기존 인스턴스가 없는 경우에는 시작 유형이 사용 안 함으로 설정되고 중지됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 설치에 대한 보안 고려 사항](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
