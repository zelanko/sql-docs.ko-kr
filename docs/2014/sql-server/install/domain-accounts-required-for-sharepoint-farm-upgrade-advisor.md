---
title: SharePoint 팜에 필요한 도메인 계정 (업그레이드 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 90cd6d3e-a271-4cb8-81f2-fc555b2d3cab
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: c4079ea4213d7ecbec0165c32c82b3449bbb5aee
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952515"
---
# <a name="domain-accounts-required-for-sharepoint-farm-upgrade-advisor"></a>SharePoint 팜에 도메인 계정이 필요함(업그레이드 관리자)
  팜 환경용으로 구성되는 SharePoint 제품에서는 도메인 계정을 사용해야 합니다.  
  
||  
|-|  
|SharePoint 모드를[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **[!INCLUDE[applies](../../includes/applies-md.md)]** .|  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssRS](../../includes/ssrs.md)]  
  
### <a name="description"></a>설명  
 팜 환경용으로 구성되는 SharePoint 제품에서는 서비스 및 데이터베이스 연결에 도메인 계정을 사용해야 합니다. 여기에는 Reporting Services 서비스 계정으로 지정한 계정이 포함됩니다.  
  
 Reporting Services에 대해 도메인 사용자 계정을 사용하지 않는 경우 문제가 표시되는 위치는 SharePoint 2010 중앙 관리 페이지뿐입니다. Reporting Services 통합을 구성하려고 하면 다음과 같은 오류 메시지가 표시됩니다.  
  
 "보고서 서버가 SharePoint 팜 설치에서 지원되지 않는 기본 제공 NT AUTHORITY\NETWORK SERVICE 계정으로 실행되고 있습니다. 도메인 계정으로 실행되도록 보고서 서버를 다시 구성하십시오."  
  
## <a name="corrective-action"></a>수정 동작  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 이전 버전의 경우 Reporting Services 구성 관리자를 사용 하 여 보고서 서버 서비스 계정으로 할당 된 계정을 변경 합니다.  
  
#### <a name="to-change-the-service-account-from-configuration-manager"></a>구성 관리자에서 서비스 계정을 변경하려면  
  
1.  **시작** 메뉴에서 **모든 프로그램**을 선택 하 고 **Microsoft SQL Server 2008 R2**를 클릭 합니다.  
  
2.  **구성 도구**를 선택 하 고 **Reporting Services 구성 관리자**를 클릭 합니다.  
  
3.  Configuration Manager에서 **서비스 계정** 탭을 선택 합니다.  
  
4.  **다른 계정 사용** 을 선택 하 고 도메인 계정에 대 한 자격 증명을 입력 합니다.  
  
5.  **적용**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 서버 서비스 계정 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
  
  
