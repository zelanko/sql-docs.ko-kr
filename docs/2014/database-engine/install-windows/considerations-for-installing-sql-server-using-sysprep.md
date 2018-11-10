---
title: SysPrep을 사용하여 SQL Server 설치 시 고려 사항 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: e1792eeb-2874-4653-b20e-3063f4eb4e5d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 396f26f617ec64aa1d2c46f4c4b600a824a2f278
ms.sourcegitcommit: 87f29b23d5ab174248dab5d558830eeca2a6a0a4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51018938"
---
# <a name="considerations-for-installing-sql-server-using-sysprep"></a>SysPrep을 사용하여 SQL Server 설치 시 고려 사항
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep을 사용하여 컴퓨터에 독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 준비하고 나중에 구성을 완료할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep은 두 단계로 된 과정을 통해 독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 구성합니다. 단계는 다음과 같습니다.  
  
-   [이미지 준비](#BKMK_PrepareImage)  
  
     이 단계에서는 준비 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 컴퓨터, 네트워크 또는 계정 관련 정보를 구성하지 않고 제품 바이너리가 설치된 후 설치 프로세스를 중지합니다.  
  
-   [이미지 완료](#BKMK_CompleteImage)  
  
     이 단계에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]준비 인스턴스의 구성을 완료할 수 있습니다. 이 단계를 실행하는 동안 컴퓨터, 네트워크 및 계정 관련 정보를 제공할 수 있습니다.  
  
 설치 하는 방법에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep을 사용 하 여 [SysPrep을 사용 하 여 SQL Server 2014 설치](install-sql-server-using-sysprep.md)합니다.  
  
## <a name="common-uses-for-includessnoversionincludesssnoversion-mdmd-sysprep"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep의 일반적인 용도  
 다음과 같은 방법으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep 기능을 사용할 수 있습니다.  
  
-   이미지 준비 단계를 사용하면 구성되지 않은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 같은 컴퓨터에서 하나 이상 준비할 수 있습니다. 이러한 준비 인스턴스는 같은 컴퓨터에서 이미지 완료 단계를 통해 구성할 수 있습니다.  
  
-   준비 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 구성 파일을 캡처한 다음, 이 파일을 사용하여 여러 컴퓨터에서 구성되지 않은 추가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 준비하고, 나중에 이러한 인스턴스를 구성할 수 있습니다.  
  
-   Windows 시스템 준비 도구(또는 Windows SysPrep)와 함께 사용하면 구성되지 않은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 준비 인스턴스를 포함하여 원본 컴퓨터에서 운영 체제 이미지를 만들 수 있습니다. 그런 다음 이 운영 체제 이미지를 여러 컴퓨터에 배포할 수 있습니다. 운영 체제 구성을 완료한 후에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치의 이미지 완료 단계를 사용하여 준비 인스턴스를 구성할 수 있습니다.  
  
     Windows SysPrep 도구는 Windows 운영 체제 이미지를 준비하는 데 사용됩니다. 이 도구는 조직에 배포할 운영 체제의 사용자 지정 이미지를 캡처하는 데 사용됩니다. SysPrep 및 그 사용법에 대한 자세한 내용은 [Sysprep이란?](http://go.microsoft.com/fwlink/?LinkId=143546)을 참조하십시오.  
  
## <a name="installation-media-considerations"></a>설치 미디어 고려 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]전체 버전을 사용하는 경우 다음 사항을 고려하십시오.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Express Edition 이외 버전:  
  
    -   이미지 준비 단계에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Evaluation Edition을 사용하여 제품 바이너리를 설치합니다. 인스턴스가 완료되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전은 이미지 완료 단계에서 제공한 제품 ID에 따라 달라집니다.  
  
    -   Evaluation Edition 제품 ID를 제공하는 경우에는 준비 인스턴스가 완료되면 평가 기간이 180일 후 만료로 설정됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Express Edition:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express Edition 인스턴스를 준비하려면 Express 설치 미디어를 사용합니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express Edition의 준비 인스턴스에 대해서는 제품 ID를 지정할 수 없습니다.  
  
## <a name="supported-includessnoversionincludesssnoversion-mdmd-installations"></a>지원되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 의 SysPrep은 도구를 비롯하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 모든 기능을 지원합니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 이전 버전을 함께 설치하기 위해 여러 인스턴스를 준비할 수 있습니다. 이러한 인스턴스의 기능은 SysPrep을 지원해야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 이미지 준비 단계의 끝에 자동으로 설치 및 완료됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Writer는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 준비할 때 자동으로 준비되고, 이미지 완료 단계에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 완료할 때 함께 완료됩니다.  
  
 지원 되는 버전에 대 한 자세한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]준비 인스턴스를 구성하는 동안 버전 업그레이드를 수행할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express Edition에 대해서는 이 옵션이 지원되지 않습니다.  
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep은 명령줄에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 설치를 지원합니다.  
  
## <a name="includessnoversionincludesssnoversion-mdmd-sysprep-limitations"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep 제한 사항  
 준비 인스턴스 복구는 지원되지 않습니다. 이미지 준비 또는 이미지 완료 단계에서 설치가 실패하면 제거를 실행해야 합니다.  
  
##  <a name="BKMK_PrepareImage"></a> 이미지 준비  
 이미지 준비 단계에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품 및 기능을 설치하지만 설치를 구성하지는 않습니다.  
  
 이 단계에서는 설치할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품 설치 파일의 설치 위치를 지정할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 센터 **의** 고급 **페이지에서** SysPrep 배포를 위한 독립 실행형 인스턴스의 이미지 준비 **를 사용하거나 명령 프롬프트를 통해** 인스턴스를 준비할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 같은 컴퓨터에서 여러 개 준비한 후 나중에 완료할 수 있습니다.  
  
-   기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]준비 인스턴스에서 SysPrep 설치에 대해 지원되는 기능을 추가하거나 제거할 수 있습니다.  
  
 인스턴스가 준비된 후에는 **준비 인스턴스의 구성을 완료할 수 있도록** 시작 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]메뉴의 바로 가기를 사용할 수 있습니다.  
  
##  <a name="BKMK_CompleteImage"></a> 이미지 완료  
 다음 방법 중 하나를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 준비 인스턴스를 완료할 수 있습니다.  
  
-   시작 메뉴의 바로 가기를 사용합니다.  
  
-   **설치 센터** 의 **고급** 페이지에서 **독립 실행형 준비 인스턴스의 이미지 완료**단계에 액세스합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md)  
  
  
