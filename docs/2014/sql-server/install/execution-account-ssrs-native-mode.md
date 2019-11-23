---
title: 실행 계정 (SSRS 기본 모드) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.executionaccount.F1
ms.assetid: 440b5a09-5fd4-4c3a-b510-f3c33cbf1c82
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 0eff6dca788744b93d2d6d4a0a7175764e263f71
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952540"
---
# <a name="execution-account-ssrs-native-mode"></a>실행 계정(SSRS 기본 모드)
  이 페이지를 사용하여 무인 모드 처리용으로 사용할 계정을 구성할 수 있습니다. 이 계정은 다음과 같이 다른 자격 증명 원본을 사용할 수 없는 특별한 환경에서 사용됩니다.  
  
-   보고서 서버가 자격 증명이 필요 없는 데이터 원본에 연결하는 경우 자격 증명이 필요 없는 데이터 원본의 예로는 XML 문서와 일부 클라이언트 쪽 애플리케이션이 있습니다.  
  
-   보고서 서버가 보고서에서 참조하는 외부 이미지 파일 또는 기타 리소스를 검색하기 위해 다른 서버에 연결하는 경우  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.  
  
 이 계정 설정은 선택 사항이지만 설정하지 않은 경우 외부 이미지 및 일부 데이터 원본에 대한 연결을 사용하는 데 제한이 따릅니다. 외부 이미지 파일을 검색할 때 보고서 서버는 익명 연결을 설정할 수 있는지 여부를 확인합니다. 연결이 암호로 보호된 경우 보고서 서버는 무인 보고서 처리 계정을 사용하여 원격 서버에 연결합니다. 보고서에 대한 데이터를 검색할 때 데이터 원본 연결이 자격 증명 유형을 **없음** 으로 지정한 경우 보고서 서버는 현재 사용자를 가장하거나, 사용자에게 자격 증명을 요청하거나, 저장된 자격 증명을 사용하거나, 무인 처리 계정을 사용합니다. 보고서 서버는 다른 컴퓨터에 연결할 때 해당 서비스 계정 자격 증명을 위임 또는 가장할 수 없으므로 사용 가능한 다른 자격 증명이 없는 경우 무인 처리 계정을 사용해야 합니다.  
  
 서비스 계정을 실행하는 데 사용되는 계정과 다른 계정을 지정해야 합니다. 이 계정을 구성할 경우 해당 계정은 RSReportServer.config 파일에 암호화된 값으로 저장됩니다. 스케일 아웃 배포에서 보고서 서버를 실행하는 경우 이 계정은 각 보고서 서버에서 같은 방식으로 구성해야 합니다.  
  
 Windows 사용자 계정을 사용할 수 있습니다. 최상의 결과를 얻으려면 다른 컴퓨터와의 연결을 지원하는 네트워크 로그온 권한과 읽기 권한을 가진 계정을 선택합니다. 보고서에서 사용하려는 모든 외부 이미지 또는 데이터 파일에 대해 읽기 권한을 갖고 있어야 합니다. 모든 보고서 데이터 원본과 외부 이미지가 보고서 서버 컴퓨터에 저장되어 있지 않으면 로컬 계정을 지정하지 마세요. 이 계정은 무인 보고서 처리에만 사용합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)]을 사용하는 경우 보고서에서 외부 이미지를 참조하고 해당 이미지 파일에 액세스하는 데 사용 권한이 필요할 때만 이 계정을 구성하면 됩니다. SQL Server Express는 원격 서버에 대한 데이터 원본 연결을 지원하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2012 버전에서 지원하는 기능](https://go.microsoft.com/fwlink/?linkid=232473)을 참조하세요.  
  
 이 페이지를 열려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 시작하고 탐색 창에서 **실행 계정** 에 연결합니다. 자세한 내용은 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **실행 계정 지정**  
 계정을 지정하려면 선택합니다.  
  
 **계정**  
 Windows 도메인 사용자 계정을 입력합니다. *\<domain>\\<user account\>* 형식을 사용합니다.  
  
 **암호**  
 암호를 입력합니다.  
  
 **암호 확인**  
 암호를 다시 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 구성 관리자 F1 도움말 항목 &#40;SSRS 기본 모드&#41; ](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [암호화된 보고서 서버 데이터 저장&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [무인 실행 계정 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)  
  
  
