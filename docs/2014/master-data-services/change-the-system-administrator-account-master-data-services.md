---
title: 시스템 관리자 계정 (Master Data Services) 변경 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- administrators [Master Data Services], changing
ms.assetid: cf30312e-4338-49a7-90f0-6e4f7b431ff8
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: a0e9a79120b4f184fb7acf07eeaf46101740a173
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089955"
---
# <a name="change-the-system-administrator-account-master-data-services"></a>시스템 관리자 계정 변경(Master Data Services)
  로 지정 된 사용자 계정을 변경할 수 있습니다는 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 시스템 관리자입니다.  
  
> [!WARNING]  
>  이 절차를 완료하면 이전 시스템 관리자의 사용자 계정이 삭제됩니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   새 관리자의 사용자 이름을 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 사용자 목록에 추가해야 합니다. 자세한 내용은 참조 [사용자 추가 &#40;Master Data Services&#41;](add-a-user-master-data-services.md)합니다.  
  
-   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에서 mdm.tblUser를 보고 mdm.udpSecurityMemberProcessRebuildModel 저장 프로시저를 실행할 수 있는 사용 권한이 있어야 합니다. 자세한 내용은 [데이터베이스 개체 보안&#40;Master Data Services&#41;](../../2014/master-data-services/database-object-security-master-data-services.md)을 참조하세요.  
  
### <a name="to-change-the-administrator-account"></a>관리자 계정을 변경하려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 을 열고 [!INCLUDE[ssDE](../includes/ssde-md.md)] 데이터베이스의 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 인스턴스에 연결합니다.  
  
2.  Mdm.tblUser에서 새 관리자 되며의 값을 복사 하는 사용자를 찾습니다는 `SID` 열입니다.  
  
3.  새 쿼리를 만듭니다.  
  
4.  다음 텍스트를 입력 바꾸기 *DOMAIN\user_name* 새 관리자의 사용자 이름으로 및 *SID* 2 단계에서 복사한 값이 사용 됩니다.  
  
    ```  
    EXEC [mdm].[udpSecuritySetAdministrator] @UserName='DOMAIN\user_name', @SID = 'SID', @PromoteNonAdmin = 1  
    ```  
  
5.  쿼리를 실행합니다.  
  
## <a name="see-also"></a>관련 항목  
 [관리자가 &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)  
  
  