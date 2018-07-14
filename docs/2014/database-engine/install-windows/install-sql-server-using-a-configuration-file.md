---
title: Install SQL Server 2014 구성 파일을 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a832153a-6775-4bed-83f0-55790766d885
caps.latest.revision: 28
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9536c674f9bf5733fb6d20109ee03206a50570c4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37231863"
---
# <a name="install-sql-server-2014-using-a-configuration-file"></a>구성 파일을 사용하여 SQL Server 2014 설치
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 시 시스템 기본값 및 런타임 입력을 기반으로 구성 파일을 생성할 수 있습니다. 구성 파일을 사용하면 동일한 구성으로 회사 전체에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 배포할 수 있습니다. 또한 Setup.exe를 실행하는 배치 파일을 만들어 수동 설치를 전사적으로 표준화할 수도 있습니다.  
  
 구성 파일은 명령 프롬프트에서 설치할 경우에만 사용할 수 있습니다. 구성 파일을 사용할 때 매개 변수의 처리 순서는 다음과 같습니다.  
  
-   구성 파일이 패키지의 기본값을 덮어씁니다.  
  
-   명령줄 값이 구성 파일의 값을 덮어씁니다.  
  
 구성 파일을 사용하여 각 설치의 매개 변수와 값을 추적할 수 있습니다. 따라서 구성 파일은 설치를 검사 및 감사할 때 유용합니다.  
  
## <a name="configuration-file-structure"></a>구성 파일 구조  
 ConfigurationFile.ini 파일은 매개 변수(이름/값 쌍)와 설명이 있는 텍스트 파일입니다.  
  
 다음은 ConfigurationFile.ini 파일의 예입니다.  
  
```  
; Microsoft SQL Server Configuration file  
[OPTIONS]  
; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE.   
; This is a required parameter.   
ACTION="Install"  
; Specifies features to install, uninstall, or upgrade.   
; The list of top-level features include SQL, AS, RS, IS, and Tools.   
; The SQL feature will install the database engine, replication, and full-text.   
; The Tools feature will install Management Tools, Books online,   
; SQL Server Data Tools, and other shared components.   
FEATURES=SQL,Tools  
```  
  
#### <a name="how-to-generate-a-configuration-file"></a>구성 파일을 생성하는 방법  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 미디어를 넣고 루트 폴더에서 Setup.exe를 두 번 클릭합니다. 네트워크 공유에서 설치하려면 공유에서 루트 폴더를 찾은 다음 Setup.exe를 두 번 클릭합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express Edition 설치 프로그램이 구성 파일을 자동으로 만들지 않습니다. 다음 명령으로 설치 프로그램을 시작하고 구성 파일을 만듭니다.  
    >   
    >  SETUP.exe /UIMODE = Normal /ACTION = INSTALL  
  
2.  마법사의 안내에 따르면 **설치 준비 완료** 페이지가 표시됩니다. 구성 파일의 경로는 **설치 준비 완료** 페이지의 구성 파일 경로 섹션에 지정됩니다. 설치 하는 방법에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조 하세요 [설치 마법사에서 SQL Server 2014 설치 &#40;설치&#41;](install-sql-server-from-the-installation-wizard-setup.md)합니다.  
  
3.  설치를 실제로 완료하지는 않고 INI 파일을 생성하기 위해 설치를 취소합니다.  
  
    > [!NOTE]  
    >  설치 프로그램은 암호 등과 같은 기밀 정보를 제외하고 수행했던 동작에 적합한 모든 매개 변수를 기록합니다. /IAcceptSQLServerLicenseTerms 매개 변수도 구성 파일에 기록되지 않기 때문에 구성 파일을 수정하거나 명령 프롬프트에서 값을 제공해야 합니다. 자세한 내용은 [명령 프롬프트에서 SQL Server 2014 설치](install-sql-server-from-the-command-prompt.md)를 참조하세요. 또한 일반적으로 명령 프롬프트에서 값을 입력하지 않는 부울 매개 변수에 대한 값도 포함됩니다.  
  
## <a name="using-the-configuration-file-to-install-includessnoversionincludesssnoversion-mdmd"></a>구성 파일을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 구성 파일은 명령줄 설치에서만 사용할 수 있습니다.  
  
> [!NOTE]  
>  구성 파일을 변경해야 할 경우 구성 파일을 복사한 후 이 복사본을 변경하는 것이 좋습니다.  
  
#### <a name="how-to-use-a-configuration-file-to-install-a-stand-alone-includessnoversionincludesssnoversion-mdmd-instance"></a>구성 파일을 사용하여 독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 설치하는 방법  
  
-   명령 프롬프트에서 설치를 실행하고 *ConfigurationFile* 매개 변수를 사용하여 ConfigurationFile.ini를 입력합니다.  
  
#### <a name="how-to-use-a-configuration-file-to-prepare-and-complete-an-image-of-a-stand-alone-includessnoversionincludesssnoversion-mdmd-instance-sysprep"></a>구성 파일을 사용하여 독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스(SysPrep)의 이미지를 준비하고 완료하는 방법  
  
1.  같은 시스템에 하나 이상의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 준비하고 구성하려면  
  
    -   설치 센터의 **고급** 페이지에서 **독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이미지 준비**를 실행하고 이미지 준비 구성 파일을 캡처합니다.  
  
    -   템플릿과 동일한 이미지 준비 구성 파일을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 준비합니다.  
  
    -   설치 센터의 **고급** 페이지에서 **독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 준비 인스턴스의 이미지 완료**를 실행하여 시스템에서 준비 인스턴스를 구성합니다.  
  
2.  Windows SysPrep 도구를 사용하여 구성되지 않은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 준비 인스턴스를 포함한 운영 체제 이미지를 준비하려면  
  
    -   설치 센터의 고급 페이지에서 **독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이미지 준비**를 실행하고 이미지 준비 구성 파일을 캡처합니다.  
  
    -   설치 센터의 **고급** 페이지에서 **독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 준비 인스턴스의 이미지 완료**를 실행하지만 완료된 구성 파일을 캡처한 다음 **완료 준비** 페이지에서 취소합니다.  
  
    -   이미지 완료 구성 파일은 Windows 이미지와 함께 저장하여 준비 인스턴스의 구성을 자동화할 수 있습니다.  
  
#### <a name="how-to-install-a-includessnoversionincludesssnoversion-mdmd-failover-cluster-using-the-configuration-file"></a>구성 파일을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 설치하는 방법  
  
1.  통합 설치 옵션(한 노드에 하나의 노드 장애 조치(Failover) 클러스터를 만들고, 추가할 노드에서 AddNode를 실행하여 노드를 추가함):  
  
    -   "장애 조치(Failover) 클러스터 설치" 옵션을 실행하고 모든 설치 설정이 나열된 구성 파일을 캡처합니다.  
  
    -   *ConfigurationFile* 매개 변수를 입력하여 명령줄 장애 조치(failover) 클러스터 설치를 실행합니다.  
  
    -   추가할 노드에서 AddNode를 실행하여 기존 장애 조치(Failover) 클러스터에 적용되는 ConfigurationFile.ini 파일을 캡처합니다.  
  
    -   ConfigurationFile 매개 변수를 사용하여 동일한 구성 파일을 입력함으로써 장애 조치(Failover) 클러스터에 추가할 모든 노드에서 명령줄 AddNode를 실행합니다.  
  
2.  고급 설치 옵션(모든 장애 조치(Failover) 클러스터 노드에 장애 조치(Failover) 클러스터를 준비하고 모든 노드를 준비한 후 공유 디스크를 소유하는 노드에서 실행을 완료함):  
  
    -   노드 중 하나에서 **준비** 를 실행하고 ConfigurationFile.ini 파일을 캡처합니다.  
  
    -   동일한 ConfigurationFile.ini 파일을 입력하여 장애 조치(Failover) 클러스터를 위해 준비할 모든 노드에서 설치합니다.  
  
    -   모든 노드를 준비한 후 공유 디스크를 소유하는 노드에서 전체 장애 조치(Failover) 클러스터 작업을 실행하고 ConfigurationFile.ini 파일을 캡처합니다.  
  
    -   그런 다음 이 ConfigurationFile.ini 파일을 입력하여 장애 조치(Failover) 클러스터를 완료할 수 있습니다.  
  
#### <a name="how-to-add-or-remove-a-node-to-a-includessnoversionincludesssnoversion-mdmd-failover-cluster-using-the-configuration-file"></a>구성 파일을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 대해 노드를 추가하거나 제거하는 방법  
  
-   이전에 장애 조치(Failover) 클러스터에 대해 노드를 추가하거나 제거할 때 사용했던 구성 파일이 있을 경우 이 파일을 다시 사용하여 노드를 추가하거나 제거할 수 있습니다.  
  
#### <a name="how-to-upgrade-a-includessnoversionincludesssnoversion-mdmd-failover-cluster-using-the-configuration-file"></a>구성 파일을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 업그레이드하는 방법  
  
1.  패시브 노드에서 업그레이드를 실행하고 ConfigurationFile.ini 파일을 캡처합니다. 실제 업그레이드를 수행하거나, 실제 업그레이드를 수행하지 않고 종료 시 끝내는 방법을 사용할 수 있습니다.  
  
2.  업그레이드할 모든 추가 노드에서 ConfigurationFile.ini 파일을 입력하여 프로세스를 완료합니다.  
  
## <a name="sample-syntax"></a>예제 구문  
 다음은 구성 파일을 사용하는 방법을 보여 주는 예입니다.  
  
-   명령 프롬프트에 구성 파일을 지정하기  
  
```  
Setup.exe /ConfigurationFile=MyConfigurationFile.INI  
```  
  
-   구성 파일 대신 명령 프롬프트에 암호 지정하기  
  
```  
Setup.exe /SQLSVCPASSWORD="************" /AGTSVCPASSWORD="************" /ASSVCPASSWORD="************" /ISSVCPASSWORD="************" /RSSVCPASSWORD="************" /ConfigurationFile=MyConfigurationFile.INI  
```  
  
## <a name="see-also"></a>관련 항목  
 [명령 프롬프트에서 SQL Server 2014 설치](install-sql-server-from-the-command-prompt.md)   
 [SQL Server 장애 조치(Failover) 클러스터 설치](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)   
 [SQL Server 장애 조치(Failover) 클러스터 업그레이드](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)  
  
  
