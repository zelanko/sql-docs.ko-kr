---
title: 스케일 아웃 배포의 암호화 키 추가 및 제거 | Microsoft Docs
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- encryption keys [Reporting Services]
- deleting encryption keys
- removing encryption keys
- adding encryption keys
- rskeymgmt utility
- scale-out deployments [Reporting Services]
ms.assetid: 2da86fb3-4b4d-407f-9825-74dcc42486f5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 288e4a4fab078a7b4d8afb7544416ee8a7429340
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43281599"
---
# <a name="add-and-remove-encryption-keys-for-scale-out-deployment"></a>확장 배포의 암호화 키 추가 및 제거
  여러 보고서 서버에서 공유 보고서 서버 데이터베이스를 사용하도록 구성하여 스케일 아웃 배포 모델에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 실행할 수 있습니다. 스케일 아웃 배포의 멤버 자격은 보고서 서버가 암호화 키를 보고서 서버 데이터베이스에 저장하는지 여부에 따라 결정됩니다. 특정 보고서 서버 인스턴스에 대한 암호화 키를 추가 및 제거하여 스케일 아웃 배포 멤버 자격을 제어할 수 있습니다. 배포에서 노드를 제거하는 경우 순서에 관계없이 제거할 수 있습니다. 배포에 노드를 추가할 경우 이미 배포에 포함되어 있는 보고서 서버로부터 새 인스턴스를 조인해야 합니다.  
  
## <a name="using-the-reporting-services-configuration-tool-to-configure-scale-out-deployment"></a>Reporting Services 구성 도구를 사용하여 확장 배포 구성  
 스케일 아웃 배포를 구성하는 가장 쉬운 방법은 Reporting Services 구성 도구를 사용하는 것입니다. 자세한 내용 및 단계별 지침은 [기본 모드 보고서 서버 스케일 아웃 배포 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)을 참조하세요.  
  
## <a name="using-rskeymgmt-to-configure-scale-out-deployment"></a>Rskeymgmt를 사용하여 확장 배포 구성  
 **rskeymgmt** 유틸리티를 사용하여 공유 보고서 서버 데이터베이스를 사용하도록 보고서 서버 인스턴스를 초기화할 수 있습니다. 스케일 아웃 배포에 보고서 서버를 추가하려면 보고서 서버를 초기화해야 합니다. 초기화를 위해서는 관리자 권한이 필요합니다. 배포에 참여시킬 보고서 서버를 호스팅하는 원격 컴퓨터에 대해 관리자 자격 증명이 있어야 합니다.  
  
### <a name="how-to-join-a-report-server-to-a-scale-out-deployment-rskeymgmt"></a>스케일 아웃 배포에 보고서 서버를 참여시키는 방법(rskeymgmt)  
  
1.  이미 보고서 서버 스케일 아웃 배포의 멤버인 보고서 서버를 호스트하는 컴퓨터에서 로컬로 **rskeymgmt.exe** 를 실행합니다.  
  
2.  **-j** 인수를 사용하여 보고서 서버를 보고서 서버 데이터베이스에 연결합니다. **-m** 및 **-n** 인수를 사용하여 배포에 추가할 원격 보고서 서버 인스턴스를 지정합니다. **-u** 및 **-v** 인수를 사용하여 원격 컴퓨터의 관리자 계정을 지정합니다. 같은 컴퓨터에서 여러 보고서 서버 인스턴스를 사용하여 스케일 아웃 배포를 만드는 경우 사용하는 구문이 약간 다릅니다. 사용해야 할 구문에 대한 자세한 내용은 [rskeymgmt 유틸리티&#40;SSRS&#41;](../../reporting-services/tools/rskeymgmt-utility-ssrs.md)를 참조하세요.  
  
     다음 예에서는 원격 보고서 서버를 스케일 아웃 배포에 조인하려는 경우 지정해야 하는 인수에 대해 설명합니다. 원격 컴퓨터에서 관리자 권한이 있으면 자격 증명을 생략해도 됩니다.  
  
    ```  
    rskeymgmt -j -m <remotecomputer> -n <namedreportserverinstance> -u <administratoraccount> -v <administratorpassword>  
    ```
3. Reporting Services Windows 서비스를 다시 시작합니다.
  
### <a name="how-to-remove-a-report-server-from-a-scale-out-deployment-rskeymgmt"></a>스케일 아웃 배포에서 보고서 서버를 제거하는 방법(rskeymgmt)  
  
1.  제거하려는 보고서 서버의 reportserver.config 파일을 열고 설치 ID를 찾습니다. 이 파일의 기본 위치는 Program Files\Microsoft SQL Server\MSSQL.*n*\Reporting Services\ReportServer입니다.  
  
     단일 인스턴스를 설치한 경우 컴퓨터에는 rsreportserver.config 파일이 하나만 있습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스를 여러 개 설치한 경우 Reporting Services 구성 도구의 서버 상태 페이지를 사용하여 제거하려는 보고서 서버의 인스턴스 식별자(예: MSSQL.2)를 찾습니다. 보고서 서버 인스턴스에 대한 프로그램 파일을 저장하는 폴더 이름은 인스턴스 식별자를 기반으로 합니다(예: Program Files\Microsoft SQL Server\MSSQL.2).  
  
2.  **rskeymgmt.exe**를 실행합니다. 보고서 서버 스케일 아웃 배포에 속하는 어떠한 보고서 서버에 대해서도 이 프로그램을 실행할 수 있습니다.  
  
3.  **-r** 인수를 사용하여 스케일 아웃 배포에서 보고서 서버 인스턴스를 해제합니다. 다음은 인수 지정 예입니다.  
  
    ```  
    rskeymgmt -r <installation ID>  
    ```  
4. Reporting Services Windows 서비스를 다시 시작합니다.
  
 이 단계를 수행하면 스케일 아웃 배포에서 보고서 서버가 제거되지만, 보고서 서버에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스의 설치가 제거되지는 않습니다. 스케일 아웃 배포에서 보고서 서버를 제거한 후 해당 서버에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]가 더 이상 필요하지 않은 경우 서버에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 제거할 수 있습니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 [SQL Server의 기존 인스턴스 제거&#40;설치 프로그램&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [암호화 키 구성 및 관리&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)   
 [보고서 서버 초기화&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)  
  
  
