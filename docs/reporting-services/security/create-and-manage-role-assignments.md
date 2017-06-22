---
title: "역할 할당 생성 및 관리 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing role assignments
- roles [Reporting Services], assignments
- security [Reporting Services], role assignments
- modifying role assignments
- deleting role assignments
ms.assetid: 086d0987-b43c-4834-8372-e08fb4b432f8
caps.latest.revision: 39
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8c07e836a48774cbf9c0c5441fde9d5df854fdcb
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="create-and-manage-role-assignments"></a>역할 할당 생성 및 관리
  *역할 할당* 은 사용자 또는 그룹이 특정 보고서 서버 항목에 액세스하거나 작업을 수행할 수 있는지 여부를 결정하는 보안 정책입니다. 역할 할당은 단일 사용자 또는 그룹 계정 이름과 하나 이상의 역할 정의로 구성됩니다.  
  
 역할 할당의 범위는 *항목 수준* 또는 *시스템 수준*입니다.  
  
-   항목 수준 역할 할당은 항상 보고서 서버 폴더 계층에 있는 특정 항목 또는 분기의 컨텍스트에서 만들어집니다. 특정 폴더 또는 항목으로 이동하여 해당 역할 할당을 만듭니다.  
  
-   시스템 수준 역할 할당은 보고서 서버 사이트 전체에 영향을 주는 태스크를 수행할 수 있는 기능을 선택한 사용자에게 제공합니다. 이러한 태스크에는 공유 일정 만들기, 작업 관리, 보고서 작성기에서 보고서 처리, 속성 설정 등이 있습니다. 시스템 수준 보안은 보고서 서버 폴더 계층에 있는 항목에 대한 액세스를 제공하지 않습니다.  
  
## <a name="creating-an-item-level-role-assignment"></a>항목 수준 역할 할당 만들기  
 역할 할당을 만들거나 관리하려면 보고서 관리자를 사용하여 보안을 설정할 항목의 보안 속성 페이지를 엽니다.  
  
 보고서 서버에 액세스해야 하는 각 사용자 또는 그룹 계정에 대해 별도의 역할 할당을 만들어야 합니다. 계정이 보고서 서버를 포함하지 않는 도메인에 있는 경우 해당 도메인 이름을 포함합니다. 계정을 지정한 후 하나 이상의 역할 정의를 선택할 수 있습니다. 역할 정의는 계속 추가할 수 있습니다. 특정 사용자 또는 그룹에 대한 할당에서는 모든 정의에 포함되어 있는 태스크를 모두 지원합니다.  
  
 광범위한 액세스 권한을 설정하려면 폴더 계층에서 높은 수준의 항목(예: 루트 노드 홈)을 선택해야 합니다. 그런 다음 후속 역할 할당을 만들어 폴더 계층의 특정 영역을 잠글 수 있습니다.  
  
 역할 할당을 만들려면 보고서 서버 컴퓨터에서 사용자가 로컬 관리자 그룹의 멤버여야 합니다. 다른 사용자를 **내용 관리자** 역할에 할당하여 책임을 위임할 수 있습니다.  
  
 자세한 내용은 [사용자에게 보고서 서버에 대한 액세스 권한 부여&#40;보고서 관리자&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md)입니다.  
  
## <a name="creating-a-system-level-role-assignment"></a>시스템 수준 역할 할당 만들기  
 시스템 수준 역할 할당을 만들거나 관리하려면 보고서 관리자를 사용하여 사이트 설정 페이지를 엽니다.  
  
 시스템 수준 역할 할당과 항목 수준 역할 할당은 함께 있어야 합니다. 즉, 항목 수준 역할 할당이 있는 각 사용자 또는 그룹에 대해 시스템 수준 역할 할당을 만들어야 합니다.  
  
 시스템 수준 역할 할당에는 다양한 범위의 사용 권한이 포함되지만 항목 수준 역할 할당의 일부인 사용 권한은 포함되지 않습니다. 컴퓨터의 시스템 사용 권한과는 반대로 보고 서버의 시스템 역할은 사용 가능한 모든 작업 집합을 포함하는 가장 중요한 사용 권한을 제공하지 않습니다. 대신 시스템 수준 역할 할당은 범위가 보고서 서버 사이트로 제한되는 태스크 집합입니다. 시스템 역할 할당을 통해 제공되는 사용 권한은 사용자가 홈 페이지의 이미지 또는 제목과 같은 응용 프로그램 속성을 볼 수 있는지 여부, 공유 일정을 보거나 관리할 수 있는지 여부 또는 보고서 작성기를 사용할 수 있는지 여부를 결정합니다.  
  
 자세한 내용은 [사용자에게 보고서 서버에 대한 액세스 권한 부여&#40;보고서 관리자&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md) 및 [미리 정의된 역할](../../reporting-services/security/role-definitions-predefined-roles.md)입니다.  
  
## <a name="modifying-a-role-assignment"></a>역할 할당 수정  
 언제든지 역할 할당을 수정할 수 있습니다. 역할 할당을 저장하면 변경 내용이 적용됩니다. 사용자 세션에는 역할 할당 변경 사항이 적용되지 않습니다. 한 사용자가 보고서를 열어 둔 상태에서 액세스를 거부하도록 역할 할당을 수정한 경우에도 해당 사용자는 세션이 열려 있는 동안에는 보고서를 계속 사용할 수 있습니다.  
  
 이미 역할 할당의 일부인 그룹에 사용자 계정을 추가하면 해당 사용자 계정이 그룹 계정 정책을 통해 항목에 액세스할 수 있을 때까지 지연이 발생합니다. 이러한 지연은 인터넷 정보 서비스(IIS)의 인증 토큰 캐싱으로 인해 발생합니다. 토큰을 새로 고칠 때까지 기다리거나(일반적으로 대기 시간은 15분) IIS를 다시 설정하여 캐시를 즉시 업데이트할 수 있습니다.  
  
 역할 할당은 한 번에 하나씩만 수정할 수 있습니다. 전역 찾기 및 바꾸기 작업을 수행하여 역할 정의 이름 또는 역할 할당 설정을 변경하거나 특정 사용자 또는 그룹이 포함된 모든 역할 할당을 찾을 수 없습니다.  
  
## <a name="deleting-a-role-assignment"></a>역할 할당 삭제  
 삭제할 각 할당에 해당하는 확인란을 선택한 다음 **삭제**를 클릭하여 역할 할당을 삭제할 수 있습니다. **부모 보안으로 되돌리기**를 클릭하여 역할 할당을 삭제할 수도 있습니다. 이 단추를 클릭하면 항목에 대한 기존 역할 할당이 삭제되고 부모 항목을 통해 제공되는 역할 할당이 대신 사용됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [사용자에게 보고서 서버에 대한 액세스 권한 부여&#40;보고서 관리자&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md)   
 [역할 할당 수정 또는 삭제&#40;보고서 관리자&#41;](../../reporting-services/security/role-assignments-modify-or-delete.md)   
 [역할 할당](../../reporting-services/security/role-assignments.md)   
 [역할 정의](../../reporting-services/security/role-definitions.md)   
 [미리 정의된 역할](../../reporting-services/security/role-definitions-predefined-roles.md)   
 [기본 모드 보고서 서버에 대한 사용 권한 부여](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
