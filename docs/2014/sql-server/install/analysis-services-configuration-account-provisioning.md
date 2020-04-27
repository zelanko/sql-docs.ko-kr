---
title: Analysis Services 구성-계정 프로 비전 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services configuration
- account provisioning
ms.assetid: 169b1af2-6fe2-467f-8ca4-919f24c620ce
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: 033c1ec1b0ad478e525f3ea9e8f172c5e5e31eef
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66096803"
---
# <a name="analysis-services-configuration---account-provisioning"></a>Analysis Services 구성 - 계정 프로비전
  이 페이지를 사용하여 서버 모드를 설정하고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 제한 없이 액세스해야 하는 사용자나 서비스에 관리 권한을 부여할 수 있습니다. 설치 마법사에서는 로컬 Windows Group BUILTIN\Administrators를 설치할 인스턴스의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버 관리자 역할에 자동으로 추가하지 않습니다. 로컬 Administrators 그룹을 서버 관리자 역할에 추가하려면 해당 그룹을 명시적으로 지정해야 합니다.  
  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 설치 시에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 팜에서 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 서버 배포를 담당하는 SharePoint 팜 관리자 또는 서비스 관리자에게 관리 권한을 부여해야 합니다. 설치 및 서비스 계정 [!INCLUDE[ssGeminiMTS](../../includes/ssgeminimts-md.md)] 요구 사항에 대 한 자세한 내용은 [SharePoint를 사용 하 &#40;SQL Server BI 기능 설치 PowerPivot 및 Reporting Services&#41;](../../../2014/sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)를 참조 하세요.  
  
## <a name="options"></a>옵션  
 **서버 모드** - 서버 모드는 서버에 배포할 수 있는 Analysis Services 데이터베이스의 유형을 지정합니다. 서버 모드는 설치 중에 결정되며 나중에 수정할 수 없습니다. 각 모드는 함께 사용할 수 없습니다. 즉, 기존의 OLAP 및 테이블 형식 모델 솔루션을 모두 지원하려면 각각 서로 다른 모드에 맞게 구성된 두 개의 Analysis Services 인스턴스가 필요합니다.  
  
 **관리자 지정** - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 서버 관리자를 한 명 이상 지정해야 합니다. 지정한 사용자 또는 그룹은 설치할 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 서버 관리자 역할 멤버가 됩니다. 이러한 사용자 또는 그룹은 소프트웨어를 설치할 컴퓨터와 동일한 도메인의 Windows 도메인 사용자 계정이어야 합니다.  
  
> [!NOTE]  
>  UAC(사용자 계정 컨트롤)는 관리 동작이나 애플리케이션을 실행하려면 관리자가 승인을 해야 하는 Windows 보안 기능입니다. UAC는 기본적으로 설정되므로, 높은 권한을 필요로 하는 특정 작업을 허용하라는 메시지가 표시됩니다. UAC를 구성하여 기본 동작을 변경하거나 특정 프로그램에 대해 UAC를 사용자 지정할 수 있습니다. UAC 및 UAC 구성에 대 한 자세한 내용은 [사용자 계정 컨트롤 단계별 가이드](https://go.microsoft.com/fwlink/?linkid=196350) 및 [사용자 계정 컨트롤 (위키백과)](https://go.microsoft.com/fwlink/?linkid=196351)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services&#41;&#40;서비스 계정 구성](../../../2014/analysis-services/instances/configure-service-accounts-analysis-services.md)   
 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  
