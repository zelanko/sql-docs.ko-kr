---
title: 버전 삭제(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- versions [Master Data Services], deleting
- deleting versions [Master Data Services]
ms.assetid: 2a4eeffe-8379-4744-ad44-c27d8c8ac9a8
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: d75d6719219a41dfc42071a82375a66bdd877a57
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62925032"
---
# <a name="delete-a-version-master-data-services"></a>버전 삭제(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 버전에 연결된 마스터 데이터가 더 이상 필요하지 않은 경우 해당 버전을 삭제할 수 있습니다. 버전을 삭제한 후에는 연결된 마스터 데이터를 검색할 수 없습니다.  
  
> [!WARNING]  
>  모델에 버전이 하나뿐인 경우 해당 버전을 삭제하면 모델을 사용할 수 없게 됩니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에서 mdm.viw_SYSTEM_SCHEMA_VERSION 뷰를 보고 mds.udpVersionDelete 저장 프로시저를 실행할 수 있는 권한이 있어야 합니다. 자세한 내용은 [데이터베이스 개체 보안&#40;Master Data Services&#41;](database-object-security-master-data-services.md)을 참조하세요.  
  
### <a name="to-delete-a-version"></a>버전을 삭제하려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 을 열고 [!INCLUDE[ssDE](../includes/ssde-md.md)] 데이터베이스의 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 인스턴스에 연결합니다.  
  
2.  mdm.viw_SYSTEM_SCHEMA_VERSION 뷰를 엽니다.  
  
3.  삭제할 모델 버전을 찾아 **ID** 필드의 값을 복사합니다.  
  
4.  새 쿼리를 만듭니다.  
  
5.  다음 텍스트를 입력합니다. 여기서 *version_ID* 를 2단계에서 복사한 값으로 바꿉니다.  
  
    ```  
    EXEC [mdm].[udpVersionDelete] @Version_ID='version_ID'  
    ```  
  
6.  쿼리를 실행합니다.  
  
    > [!NOTE]  
    >  웹 애플리케이션에서 변경 내용을 반영할 때까지 몇 분간 기다려야 할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [버전&#40;Master Data Services&#41;](../../2014/master-data-services/versions-master-data-services.md)   
 [버전 복사&#40;Master Data Services&#41;](../../2014/master-data-services/copy-a-version-master-data-services.md)  
  
  
