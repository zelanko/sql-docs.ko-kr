---
title: 기본 SQL Server 네트워크 프로토콜 구성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- protocols [SQL Server], default settings
- default protocols, after install
ms.assetid: 635ea361-a797-4971-bd05-e3415862bc5c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 218389eaf76336e33d866f16c6b79ef54661be0b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68011953"
---
# <a name="default-sql-server-network-protocol-configuration"></a>기본 SQL Server 네트워크 프로토콜 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
보안을 강화하기 위해 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 에서는 새로 설치하는 일부의 경우 네트워크 연결을 사용하지 않습니다. Enterprise, Standard, Evaluation 또는 Workgroup 버전을 사용하거나 이전에 설치된 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]가 있는 경우 TCP/IP를 사용하는 네트워크 연결은 사용할 수 없습니다. 서버에 로컬로 연결할 수 있도록 모든 설치에 대해 공유 메모리 프로토콜이 사용됩니다. 설치 조건이나 설치 옵션에 따라 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 브라우저 서비스가 중지될 수도 있습니다.

설치 후 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 구성 관리자의 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 네트워크 구성 노드를 사용하여 네트워크 프로토콜을 구성할 수 있습니다. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 구성 관리자의 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 서비스 노드를 사용하여 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 브라우저 서비스가 자동으로 시작되도록 구성할 수 있습니다. 자세한 내용은 [서버 네트워크 프로토콜 설정 또는 해제](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)를 참조하세요.


## <a name="default-configuration"></a>기본 구성

다음 표에서는 설치 후의 구성에 대해 설명합니다.

|버전 | 새로 설치 또는 이전 설치 | 공유 메모리 | TCP/IP | 명명된 파이프|
| -------- | -- | -- | -- | --  |  
|Enterprise | 새로 설치 | 설정 | 설정 | 네트워크 연결 사용 안 함|
|Standard | 새로 설치 | 설정 | 설정 | 네트워크 연결 사용 안 함|
|Web | 새로 설치 | 설정 | 설정 | 네트워크 연결 사용 안 함|
|Developer | 새로 설치 | 설정 | 사용 안 함 | 네트워크 연결 사용 안 함|
|Evaluation | 새로 설치 | 설정 | 설정 | 네트워크 연결 사용 안 함|
|SQL Server Express | 새로 설치 | 설정 | 사용 안 함 | 네트워크 연결 사용 안 함|
|모든 버전 | 이전 설치가 있지만 업그레이드 중이 아님 | 새로 설치와 같음 | 새로 설치와 같음 | 새로 설치와 같음|
|모든 버전 | 업그레이드 | 설정 | 이전 설치의 설정이 유지됨 | 이전 설치의 설정이 유지됨|


>[!NOTE]
> 인스턴스가 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 장애 조치 클러스터에서 실행되고 있으면 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치 중에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에 대해 선택된 각 IP 주소의 포트에서 수신 대기합니다.
 
>[!NOTE]
> 명령 프롬프트 인수를 사용하여 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 를 설치하는 경우 `TCPENABLED` 및 `NPENABLED` 매개 변수를 사용하여 설정할 프로토콜을 지정할 수 있습니다. 자세한 내용은 [명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)를 참조하세요.

## <a name="creating-a-connection-string"></a>연결 문자열 만들기

샘플 연결 문자열에 대한 다음 항목을 참조하세요.
* [공유 메모리 프로토콜을 사용하여 유효한 연결 문자열 만들기](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)
* [TCP/IP를 사용하여 유효한 연결 문자열 만들기](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)



## <a name="includessnoversionmdincludesssnoversion-mdmd-browser-settings"></a>[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 브라우저 설정

설정 중에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Browser 서비스가 자동으로 시작되도록 구성할 수 있습니다. 기본적으로 다음 조건에서만 자동으로 시작됩니다.

* 설치를 업그레이드하는 경우
* 다른 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스와 함께 설치하는 경우
* 클러스터에 설치하는 경우
* [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Express의 모든 인스턴스를 포함한 데이터베이스 엔진의 명명된 인스턴스를 설치하는 경우
* Analysis Services의 명명된 인스턴스를 설치하는 경우

## <a name="see-also"></a>참고 항목

[SQL Server 2016 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)

[노출 영역 구성](../../relational-databases/security/surface-area-configuration.md)  



