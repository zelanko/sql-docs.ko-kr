---
title: 인증서 관리(SQL Server 구성 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 01/16/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: f767dba6c45c3bdc0d91b29ab561cb5f5de74844
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66785163"
---
# <a name="certificate-management-sql-server-configuration-manager"></a>인증서 관리(SQL Server 구성 관리자)

이 항목에서는 SQL Server Always On 장애 조치 클러스터 또는 가용성 그룹 토폴로지에서 인증서를 배포하고 관리하는 방법을 설명합니다.

SSL/TLS 인증서는 SQL Server에 대한 액세스를 보호하기 위해 널리 사용됩니다. 이전 버전의 SQL Server를 사용하는 대규모 SQL Server를 가진 조직은 SQL Server 인증서 인프라를 유지 관리하는 데 상당한 노력을 들여서 스크립트를 개발하고 수동 명령을 실행해야 했습니다. SQL Server 2019를 사용하면 인증서 관리는 SQL Server 구성 관리자에 통합되어 다음과 같은 일반적인 작업을 간소화합니다. 

* SQL Server 인스턴스에 설치된 인증서 보기 및 유효성 검사 
* 만료 시기가 가까운 인증서 식별 
* 주 복제본을 보유한 노드의 가용성 그룹에 인증서 배포 
* 활성 노드의 장애 조치(Failover) 클러스터 인스턴스에 참여한 머신에 인증서 배포

> [!NOTE]
> SQL Server 2008부터는 낮은 버전의 SQL Server를 사용하여 SQL Server 구성 관리자에서 인증서 관리를 사용할 수 있습니다.

##  <a name="provision-single-server-cert"></a> 단일 SQL Server 인스턴스에 대한 인증서를 설치하려면  
  
1. SQL Server 구성 관리자의 콘솔 창에서 **SQL Server 네트워크 구성**을 확장합니다.  
  
2. **프로토콜 대상** *&lt;인스턴스 이름&gt;* 을 마우스 오른쪽 단추로 클릭한 다음, **속성**을 선택합니다.  
  
3. **인증서** 탭을 선택한 다음, **가져오기**를 선택합니다.  
  
4. **찾아보기**를 선택한 다음, 인증서 파일을 선택합니다.  
  
5. **다음**을 선택하여 인증서의 유효성을 검사합니다. 오류가 없는 경우 **다음**을 선택하여 로컬 인스턴스에 인증서를 가져옵니다.  
  
 
##  <a name="provision-failover-cluster-cert"></a> 장애 조치 클러스터 구성에서 인증서를 설치하려면  
  
1. SQL Server 구성 관리자의 콘솔 창에서 **SQL Server 네트워크 구성**을 확장합니다.
  
2. **프로토콜 대상** *&lt;인스턴스 이름&gt;* 을 마우스 오른쪽 단추로 클릭한 다음, **속성**을 선택합니다. 

3. **인증서** 탭을 선택한 다음, **가져오기**를 선택합니다.

4. 인증서 형식 및 현재 노드 전용 또는 각 개별 클러스터 노드에 가져올지 여부를 선택합니다.

5. 단일 노드를 설치하는 경우 **찾아보기**를 선택하여 인증서 파일을 선택합니다. 그런 다음, 8단계로 건너뜁니다.

6. 각 노드에 인증서를 설치하는 경우 **다음**을 선택하여 가능한 소유자 노드를 나열합니다. 현재 SQL Server FCI의 가능한 소유자는 미리 선택되어 있습니다.

7. **다음**을 선택하여 가져올 인증서를 선택합니다.

8. 프롬프트가 표시되면 암호를 입력합니다. 유효성 검사 후에 경고 또는 오류를 찾아봅니다.

9. **다음**을 선택하여 선택한 인증서를 가져옵니다.

> [!NOTE]
> SQL Server 장애 조치 클러스터 인스턴스의 활성 노드에서 이러한 단계를 완료하세요. 사용자는 모든 클러스터 노드에서 관리자 권한이 있어야 합니다.

##  <a name="provision-availability-group-cert"></a>가용성 그룹 구성에 인증서를 설치하려면  
  
1. SQL Server 구성 관리자의 콘솔 창에서 **SQL Server 네트워크 구성**을 확장합니다.
  
2. **프로토콜 대상** *&lt;인스턴스 이름&gt;* 을 마우스 오른쪽 단추로 클릭한 다음, **속성**을 선택합니다.  
  
3. **인증서** 탭을 선택한 다음, **가져오기**를 선택합니다.  
  
4. 인증서 형식을 선택하고, **다음**을 선택하여 알려진 가용성 그룹의 목록 중에서 하나를 선택합니다.  

5. **다음**을 선택하여 각 복제본 노드의 인증서를 선택합니다. 인증서에는 노드의 NetBIOS 이름과 일치하는 파일 이름이 있어야 합니다.

6. **다음**을 선택하여 각 노드에 인증서를 가져옵니다.


> [!NOTE]
> 가용성 그룹 주 복제본을 보유한 노드에서 이러한 단계를 완료하세요. 사용자는 모든 클러스터 노드에서 관리자 권한이 있어야 합니다.

