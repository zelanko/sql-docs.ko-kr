---
title: 도메인 관리자-Analytics Platform System 만들기 | Microsoft Docs
description: 일부 작업에는 분석 플랫폼 시스템 도메인 관리자 권한이 필요합니다. 추가 어플라이언스 도메인 관리자를 만드는 방법을 설명 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 51ed729cda33b5d68a4d115c71f712e2b81d1a65
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961097"
---
# <a name="create-an-aps-domain-administrator"></a>APS 도메인 관리자 만들기
일부 작업에는 분석 플랫폼 시스템 도메인 관리자 권한이 필요합니다. 추가 어플라이언스 도메인 관리자를 만드는 방법을 설명 합니다.  
  
## <a name="create-a-domain-administrator"></a>도메인 관리자 만들기  
모든 AP 노드를 실행 하는 사용자를 구성 하려면 충분 한 권한이 있어야 합니다 **AP Configuration Manager** (`dwconfig.exe`)의 멤버 여야 합니다를 **Domain Admins** 그룹입니다. 시작 하 고 AP 서비스 중지를 사용자의 구성원 이어야 합니다 **PdwControlNodeAccess** 그룹입니다.  
  
#### <a name="to-add-a-user-to-the-domain-admins-group"></a>Domain Admins 그룹에 사용자를 추가 하려면  
  
1.  로그 활성 AD 노드로 **(_어플라이언스\_도메인_-AD01** 하거나  **_어플라이언스\_도메인_-AD02**) 기존 어플라이언스 도메인 관리자 계정을 사용합니다.  
  
2.  시작 메뉴에서 **실행**을 클릭합니다. 에 **엽니다** 상자에 입력 **dsa.msc**합니다. **확인**을 클릭합니다.  
  
3.  에 **Active Directory 사용자 및 컴퓨터** 프로그램을 마우스 오른쪽 단추로 클릭 **사용자**를 가리킵니다 **새로 만들기**를 클릭 하 고 **사용자**.  
  
4.  에 **새 개체-사용자** 대화 상자에서 새 사용자에 대 한 설명은 완료 하 고 클릭 **다음**합니다.  
  
    암호 대화 상자를 완료 하 고 클릭 **다음**합니다.  
  
    > [!WARNING]  
    > SQL Server PDW는 도메인 관리자 또는 로컬 관리자 암호에 달러 기호 ($)를 지원 하지 않습니다. 달러 기호를 포함 하는 암호는 유효한 및 사용할 수 있지만 업그레이드 및 유지 관리 작업을 차단할 수 있습니다.  
  
    새 사용자 설명을 확인 한 다음 클릭 **완료**합니다.  
  
5.  사용자 목록의 사용자 속성 대화 상자를 열려면 새 사용자를 두 번 클릭 합니다.  
  
6.  에 **소속** 탭을 클릭 **추가**합니다.  
  
    형식 **Domain Admins; PdwControlNodeAccess** 을 클릭 한 다음 **이름 확인**합니다. **확인**을 클릭합니다.  
  
    새 사용자를 추가 합니다 **Domain Admins** 그룹 및 **PdwControlNodeAccess** 그룹입니다. **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
[Configuration Manager 시작 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
  
