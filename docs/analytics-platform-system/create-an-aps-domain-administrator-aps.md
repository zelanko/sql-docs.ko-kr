---
title: 도메인 관리자 만들기
description: 일부 작업을 수행 하려면 분석 플랫폼 시스템 도메인 관리자 권한이 필요 합니다. 추가 어플라이언스 도메인 관리자를 만드는 방법을 설명 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 1a0d50e485f0e8f48de11b2e5a3c27c9f9be047e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401228"
---
# <a name="create-an-aps-domain-administrator"></a>APS 도메인 관리자 만들기
일부 작업을 수행 하려면 분석 플랫폼 시스템 도메인 관리자 권한이 필요 합니다. 추가 어플라이언스 도메인 관리자를 만드는 방법을 설명 합니다.  
  
## <a name="create-a-domain-administrator"></a>도메인 관리자 만들기  
모든 ap 노드를 구성할 수 있는 충분 한 권한을 보유 하려면 **aps Configuration Manager** (`dwconfig.exe`)를 실행 하는 사용자가 **domain Admins** 그룹의 구성원 이어야 합니다. APS 서비스를 시작 및 중지 하려면 사용자가 **Pdwcontrolnodeaccess** 그룹의 멤버 여야 합니다.  
  
#### <a name="to-add-a-user-to-the-domain-admins-group"></a>Domain Admins 그룹에 사용자를 추가 하려면  
  
1.  기존 어플라이언스 도메인 관리자 계정을 사용 하 여 활성 AD 노드 **(_어플라이언스\_도메인_-AD01** 또는 ** _어플라이언스\_도메인_-AD02**)에 로그인 합니다.  
  
2.  시작 메뉴에서 **실행**을 클릭합니다. **열기** 상자에 **dsa.msc**를 입력 합니다. **확인**을 클릭합니다.  
  
3.  **사용자 및 컴퓨터 Active Directory** 프로그램에서 **사용자**를 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**를 가리킨 다음 **사용자**를 클릭 합니다.  
  
4.  **새 개체-사용자** 대화 상자에서 새 사용자에 대 한 설명을 입력 하 고 **다음**을 클릭 합니다.  
  
    암호 대화 상자를 완료 하 고 **다음**을 클릭 합니다.  
  
    > [!WARNING]  
    > SQL Server PDW은 도메인 관리자 또는 로컬 관리자 암호에서 달러 기호 문자 ($)를 지원 하지 않습니다. 달러 기호를 포함 하는 암호는 유효 하 고 사용할 수 있지만 업그레이드 및 유지 관리 작업을 차단할 수 있습니다.  
  
    새 사용자 설명을 확인 하 고 **마침**을 클릭 합니다.  
  
5.  사용자 목록에서 새 사용자를 두 번 클릭 하 여 사용자 속성 대화 상자를 엽니다.  
  
6.  
  **소속 그룹** 탭에서 **추가**를 클릭합니다.  
  
    Domain Admins를 입력 합니다 **. PdwControlNodeAccess** 를 클릭 한 다음 **이름 확인**을 클릭 합니다. **확인**을 클릭합니다.  
  
    그러면 새 사용자가 **Domain Admins** 그룹 및 **Pdwcontrolnodeaccess** 그룹에 추가 됩니다. **확인**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
[Configuration Manager &#40;Analytics Platform System을 시작&#41;](launch-the-configuration-manager.md)  
  
