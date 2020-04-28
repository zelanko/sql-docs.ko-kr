---
title: 암호 Active Directory 설정
description: AP (Analytics Platform System)의 디렉터리 서비스 복원 모드에서 Active Directory 노드 관리자 로그온 암호를 설정 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6bbbf42106602a25b03072a9c9abfb04f04d3c49
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400332"
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm---analytics-platform-system"></a>DSRM (디렉터리 서비스 복원 모드)-분석 플랫폼 시스템에서 AD 노드에 로그온 하기 위한 관리자 암호 설정
DSRM (디렉터리 서비스 복원 모드)은 Active Directory Domain Services (AD DS)를 복구 하거나 복구 하는 부팅 모드입니다. AD DS 실패 하거나 AD DS 복원 해야 하는 경우 어플라이언스 AD 노드에 로그온 하는 데 사용 됩니다. DSRM의 암호는 하드웨어 공급 업체 사이트에서 어플라이언스를 설정 하는 동안 초기화 되었으며, 어플라이언스 관리자가 변경 해야 합니다. 분석 플랫폼 시스템에는 두 개의 AD DS (도메인 컨트롤러)가 있습니다. ** _appliance_domain_AD01** and AD02 ** _appliance_domain_**. 각 어플라이언스 AD 노드에 대해 다음 단계를 사용 하 여 DSRM 암호를 변경 합니다.  
  
## <a name="to-reset-the-administrator-password"></a><a name="HowToDSRM"></a>관리자 암호를 다시 설정 하려면  
  
1.  어플라이언스 AD 노드에서 <strong> _appliance_domain_AD_xx_</strong>가상 컴퓨터에 대 한 명령 프롬프트 창을 엽니다.  
  
2.  명령 프롬프트에서 `ntdsutil`를 입력합니다.  
  
3.  **Ntdsutil** 프롬프트에서을 입력 `set dsrm password`합니다.  
  
4.  **관리자 암호 다시 설정:** 프롬프트에서을 입력 `reset password on server null`합니다.  
  
5.  프롬프트에 새 암호를 입력 합니다.  
  
6.  각 어플라이언스 AD 가상 컴퓨터에 대해 위의 1-5 단계를 반복 합니다.  
  
    > [!WARNING]  
    > 분석 플랫폼 시스템은 도메인 관리자 또는 로컬 관리자 암호에 달러 기호 문자 ($)를 지원 하지 않습니다. 달러 기호를 포함 하는 암호는 유효성을 검사 하 고 사용할 수 있지만 업그레이드 및 유지 관리 작업을 차단할 수 있습니다.  
  
> [!NOTE]  
> Active Directory Domain Services 또는 가상 컴퓨터가 특정 AD 가상 컴퓨터에 대해 손상 된 경우 영향을 받는 AD 가상 컴퓨터에 대해 **ReplaceVM** 를 실행 하는 것이 좋습니다. 도움이 필요 하면 CSS에 문의 하세요.  
  
## <a name="see-also"></a>참고 항목  
[암호 재설정 &#40;분석 플랫폼 시스템&#41;](password-reset.md)  
  
