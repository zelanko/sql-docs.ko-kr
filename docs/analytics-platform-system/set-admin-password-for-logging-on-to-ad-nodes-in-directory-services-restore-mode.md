---
title: Analytics Platform System Active Directory 암호-설정 | Microsoft Docs
description: 디렉터리 서비스 복원 모드에서 Analytics Platform System (APS)에서 Active Directory 노드 관리자 로그온 암호를 설정 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3df6203a4d98bace5d23a92e70a596a34dedb60e
ms.sourcegitcommit: 170c275ece5969ff0c8c413987c4f2062459db21
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/11/2019
ms.locfileid: "54226450"
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm---analytics-platform-system"></a>디렉터리 서비스의 AD 노드에 로그온 복원 모드 (DSRM)-Analytics Platform System 대 한 관리자 암호 설정
디렉터리 서비스 복원 모드 (DSRM)에 Active Directory Domain Services (AD DS)를 복구 하기에 대 한 부팅 모드입니다. AD DS를 복원 해야 하는 경우 또는 AD DS에 실패 한 어플라이언스 AD 노드에 로그온 하는 것이 됩니다. DSRM 암호 어플라이언스 하드웨어 공급 업체 사이트에서 설치 하는 동안 초기화 된 및 어플라이언스 관리자가 변경 해야 합니다. Analytics Platform System에 두 개의 AD DS (도메인 컨트롤러);  **_appliance_domain_-AD01** 하 고  **_appliance_domain_-AD02**합니다. 각 AD 어플라이언스 노드에 대해 다음 단계를 사용 하 여 DSRM 암호를 변경 합니다.  
  
## <a name="HowToDSRM"></a>관리자 암호를 재설정 하려면  
  
1.  어플라이언스 AD 노드에서 명령 프롬프트 창을 열고  <strong>_appliance_domain_-AD_xx_</strong>가상 머신.  
  
2.  명령 프롬프트에서 `ntdsutil`를 입력합니다.  
  
3.  에 **ntdsutil** 프롬프트에 입력 `set dsrm password`합니다.  
  
4.  에 **관리자 암호 다시 설정 합니다.** 프롬프트에 입력 `reset password on server null`합니다.  
  
5.  프롬프트에서 새 암호를 입력 합니다.  
  
6.  각 AD 어플라이언스 가상 머신에 대 한 위의 1 ~ 5 단계를 반복 합니다.  
  
    > [!WARNING]  
    > Analytics Platform System은 도메인 관리자 또는 로컬 관리자 암호에 달러 기호 ($)를 지원 하지 않습니다. 달러 기호를 포함 하는 암호의 유효성을 검사 되며 되어야 사용할 수 있지만 업그레이드 및 유지 관리 작업을 차단할 수 있습니다.  
  
> [!NOTE]  
> Active Directory Domain Services 또는 가상 컴퓨터는 특정 AD 가상 컴퓨터에 대 한 손상 되 면 실행 중인 **ReplaceVM** 영향을 받는 AD 가상 컴퓨터는 권장 되는 정정 작업입니다. CSS에 문의 하 여 도움이 필요 없습니다.  
  
## <a name="see-also"></a>관련 항목  
[암호 재설정 &#40;Analytics Platform System&#41;](password-reset.md)  
  
