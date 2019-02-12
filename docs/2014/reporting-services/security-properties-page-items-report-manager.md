---
title: 보안 속성 페이지, 항목 (보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 351b8503-354f-4b1b-a7ac-f1245d978da0
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 9b38c5820a1680726b3c69d2e09c1d29600a71b4
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024474"
---
# <a name="security-properties-page-items-report-manager"></a>보안 속성 페이지, 항목(보고서 관리자)
  보안 속성 페이지를 사용하여 폴더, 보고서, 모델, 리소스 및 공유 데이터 원본에 대한 액세스를 지정하는 보안 설정을 보거나 수정할 수 있습니다. 이 페이지는 보안 권한이 있는 항목에 대해 사용할 수 있습니다.  
  
 항목에 대한 액세스는 그룹 또는 사용자가 수행할 수 있는 태스크를 지정하는 역할 할당을 통해 정의됩니다. 역할 할당은 하나의 사용자 또는 그룹 이름과 태스크 모음을 지정하는 하나 이상의 역할 정의로 구성됩니다.  
  
 보안 설정은 루트 폴더의 하위 폴더 및 모든 항목으로 상속됩니다. 상속된 보안을 명시적으로 해제하지 않는 한 하위 폴더와 항목은 부모 항목의 보안 컨텍스트를 상속 받습니다. 계층의 가운데에 있는 폴더의 보안 정책을 다시 정의하면 하위 폴더를 포함한 모든 자식 항목에 새 보안 설정이 적용됩니다.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
###### <a name="to-open-the-security-page-for-an-item"></a>항목의 보안 페이지를 열려면  
  
1.  보고서 관리자를 열고 보안 설정을 구성하려는 항목을 찾습니다.  
  
2.  항목 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 다음 단계 중 하나를 수행하십시오.  
  
    -   **보안**을 클릭합니다. 항목의 보안 속성 페이지가 열립니다.  
  
    -   **관리** 를 클릭하여 항목의 일반 속성 페이지를 연 다음 **보안** 탭을 선택합니다.  
  
 **항목 보안 편집**  
 현재 항목에 대한 보안 정의 방법을 변경하려면 클릭합니다. 폴더의 보안을 편집하면 변경 내용은 현재 폴더와 모든 하위 폴더의 내용에 적용됩니다.  
  
 이 단추는 홈 폴더에는 사용할 수 없습니다.  
  
 항목 보안을 편집하는 경우 다음과 같은 단추를 사용할 수 있습니다.  
  
 **Delete**  
 삭제할 그룹 또는 사용자 이름 옆의 확인란을 선택하고 **삭제**를 클릭합니다. 역할 할당이 하나뿐이거나 보고서 서버의 보안 기준을 정의하는 기본 제공 역할 할당(예: "Built-in\Administrators")인 경우에는 역할 할당을 삭제할 수 없습니다. 역할 할당을 삭제해도 그룹 또는 사용자 계정이나 역할 정의는 삭제되지 않습니다.  
  
 **새 역할 할당**  
 현재 항목의 추가 역할 할당을 만드는 데 사용되는 새 역할 할당 페이지를 열려면 클릭합니다. 자세한 내용은 참조 하세요. [새 역할 할당: 역할 할당 편집 페이지 &#40;보고서 관리자&#41;](../../2014/reporting-services/new-role-assignment-edit-role-assignment-page-report-manager.md)합니다.  
  
 **부모 보안으로 되돌리기**  
 보안 설정을 직속 부모 폴더의 보안 설정으로 되돌리려면 클릭합니다. 보고서 서버 폴더 계층 구조 전체에서 상속이 손상되지 않은 경우에는 최상위 폴더(홈)의 보안 설정이 사용됩니다.  
  
 **그룹 또는 사용자**  
 현재 항목에 대한 기존 역할 할당의 일부인 그룹 및 사용자를 나열합니다. 현재 폴더의 기존 역할 할당은 이 열에 표시되는 그룹과 사용자에 대해 정의됩니다. 그룹 또는 사용자 이름을 클릭하여 역할 할당의 세부 사항을 보거나 편집할 수 있습니다.  
  
 **Roles**  
 기존 역할 할당에 속하는 하나 이상의 역할 정의를 나열합니다. 그룹 또는 사용자 계정에 여러 역할이 할당되어 있으면 해당 그룹 또는 사용자는 이러한 역할에 속한 모든 태스크를 수행할 수 있습니다. 역할에 연결되어 있는 태스크를 보려면 SQL Server Management Studio를 사용하여 각 역할 정의의 태스크를 확인합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 관리자 F1 도움말](../../2014/reporting-services/report-manager-f1-help.md)   
 [미리 정의된 역할](security/role-definitions-predefined-roles.md)   
 [기본 모드 보고서 서버에 대한 사용 권한 부여](security/granting-permissions-on-a-native-mode-report-server.md)   
 [역할 할당](security/role-assignments.md)   
 [역할 정의](security/role-definitions.md)  
  
  
