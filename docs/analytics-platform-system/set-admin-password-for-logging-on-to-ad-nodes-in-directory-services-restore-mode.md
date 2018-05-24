---
title: Active Directory 암호-분석 플랫폼 시스템 설정 | Microsoft Docs
description: 디렉터리 서비스 복원 모드 Analytics Platform System (APS)에서 Active Directory 노드 관리자 로그온 암호를 설정 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e74689216c1485fc0c11c588acb151269e2b5d2b
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm---analytics-platform-system"></a>AD 노드 디렉터리 서비스의 로그온 모드 (DSRM)-분석 플랫폼 시스템 복원 대 관리자 암호 설정
디렉터리 서비스 복원 모드 DSRM ()은 Active Directory 도메인 서비스 (AD DS)를 복구 하기 위한 부팅 모드입니다. AD DS를 복원 해야 하는 경우 또는 AD DS에 실패 한 어플라이언스 AD 노드에 로그온 사용 됩니다. DSRM에 대 한 암호 어플라이언스 하드웨어 공급 업체 사이트에서 설치 하는 동안 초기화 이며 기기 관리자가 변경할 수 있습니다. 분석 플랫폼 시스템에 두 개의 AD DS (도메인 컨트롤러); ***appliance_domain *-AD01** 및 ***appliance_domain *-AD02**합니다. 각 AD 기기 노드에 대 한 다음 단계를 사용 하 여 DSRM 암호를 변경 합니다.  
  
## <a name="HowToDSRM"></a>관리자 암호 재설정  
  
1.  어플라이언스 AD 노드에서 명령 프롬프트 창을 열고 ***appliance_domain *– AD*xx***가상 컴퓨터.  
  
2.  명령 프롬프트에 입력 `ntdsutil`합니다.  
  
3.  에 **ntdsutil** 메시지를 표시, 입력 `set dsrm password`합니다.  
  
4.  에 **관리자 암호 다시 설정:** 메시지를 표시, 입력 `reset password on server null`합니다.  
  
5.  프롬프트에서 새 암호를 입력 합니다.  
  
6.  각 기기 AD 가상 컴퓨터에 대 한 위의 1-5 단계를 반복 합니다.  
  
    > [!WARNING]  
    > 분석 플랫폼 시스템 도메인 관리자 또는 로컬 관리자 암호에 달러 기호 ($) 문자를 지원 하지 않습니다. 달러 기호를 포함 하는 암호의 유효성을 검사 되며 수 사용할 수 있지만 업그레이드 및 유지 관리 작업을 차단할 수 있습니다.  
  
> [!NOTE]  
> Active Directory 도메인 서비스 또는 가상 컴퓨터는 특정 AD 가상 컴퓨터에 대 한 손상 되 면 실행 **ReplaceVM** 영향을 받는 AD에 대 한 가상 컴퓨터는 권장된 조치 합니다. CSS에 문의 하 여 도움이 필요 없습니다.  
  
## <a name="see-also"></a>관련 항목:  
[암호 재설정 &#40;분석 플랫폼 시스템&#41;](password-reset.md)  
  
