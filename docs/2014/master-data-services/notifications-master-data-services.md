---
title: 알림(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- notifications [Master Data Services]
- notifications [Master Data Services], about notifications
- e-mail [Master Data Services]
- e-mail [Master Data Services], about e-mail notifications
ms.assetid: d7ad32d5-9fe5-48fd-8c61-0b00c0aff082
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 54f8cdc55322144414be11dd837bd723b4ed3c10
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65478977"
---
# <a name="notifications-master-data-services"></a>알림(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]비즈니스 규칙 유효성 검사에 실패 하거나 모델 버전의 상태가 변경 될 때 전자 메일 알림을 보내도록 구성할 수 있습니다.  
  
## <a name="how-notifications-are-sent"></a>알림 전송 방법  
 
  [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]에서 알림을 구성합니다. 알림은 데이터베이스를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 호스팅하는 인스턴스에서 데이터베이스 메일를 사용 하 여 전자 메일 메시지를 보냅니다. 데이터베이스 메일에 대한 자세한 내용은 [온라인 설명서에서](../relational-databases/database-mail/database-mail-configuration-objects.md) 데이터베이스 메일 구성 개체 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 참조하세요.  
  
## <a name="when-notifications-are-sent"></a>알림을 보내는 경우  
 알림이 구성된 후 다음 인스턴스에 자동화된 전자 메일 알림을 보낼 수 있습니다.  
  
|인스턴스|Description|  
|--------------|-----------------|  
|데이터가 비즈니스 규칙 유효성 검사를 통과하지 못할 경우|특성 값이 비즈니스 규칙 유효성 검사를 통과하지 못하는 경우 전자 메일을 보내도록 개별 비즈니스 규칙을 구성해야 합니다. 자세한 내용은 [알림을 보내도록 비즈니스 규칙 구성&#40;Master Data Services&#41;](configure-business-rules-to-send-notifications-master-data-services.md)에서 알림을 구성합니다.|  
|모델 버전 상태가 변경될 경우|모델 버전의 상태가 변경될 때마다 모델 관리자인 사용자가 알림을 자동으로 받습니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.|  
  
## <a name="system-settings"></a>시스템 설정  
 
  [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 에는 알림에 영향을 주는 설정이 있습니다. 이러한 설정은 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 에서 조정하거나 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스의 시스템 설정 테이블에서 직접 조정할 수 있습니다. 자세한 내용은 [시스템 설정&#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 에서 전자 메일을 알림을 보내도록 구성합니다.|[전자 메일 알림 &#40;MDS(Master Data Services)&#41;구성](../../2014/master-data-services/configure-email-notifications-master-data-services.md)|  
|특성 값 변경 시 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 에서 알림을 보내도록 구성합니다.|[알림을 보내도록 비즈니스 규칙 구성 &#40;MDS(Master Data Services)&#41;](configure-business-rules-to-send-notifications-master-data-services.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [비즈니스 규칙 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
-   [버전 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/versions-master-data-services.md)  
  
-   [전자 메일 알림 문제 해결 (MDS(Master Data Services))](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-email-notifications-master-data-services.aspx)  
  
  
