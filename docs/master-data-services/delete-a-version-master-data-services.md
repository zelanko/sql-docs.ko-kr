---
title: "삭제 (Master Data Services) 버전 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- versions [Master Data Services], deleting
- deleting versions [Master Data Services]
ms.assetid: 2a4eeffe-8379-4744-ad44-c27d8c8ac9a8
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bf3a315d60bed733bd2d72cd6ba2317a8ab84ae5
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="delete-a-version-master-data-services"></a>버전 삭제(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 버전에 연결된 마스터 데이터가 더 이상 필요하지 않은 경우 해당 버전을 삭제할 수 있습니다. 버전을 삭제한 후에는 연결된 마스터 데이터를 검색할 수 없습니다.  
  
> [!WARNING]  
>  모델에 버전이 하나뿐인 경우 해당 버전을 삭제하면 모델을 사용할 수 없게 됩니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에서 mdm.viw_SYSTEM_SCHEMA_VERSION 뷰를 보고 mds.udpVersionDelete 저장 프로시저를 실행할 수 있는 권한이 있어야 합니다. 자세한 내용은 [데이터베이스 개체 보안&#40;Master Data Services&#41;](../master-data-services/database-object-security-master-data-services.md)을 참조하세요.  
  
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
    >  웹 응용 프로그램에서 변경 내용을 반영할 때까지 몇 분간 기다려야 할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [버전 &#40; Master Data services&#41;](../master-data-services/versions-master-data-services.md)   
 [버전 &#40; 복사 Master Data services&#41;](../master-data-services/copy-a-version-master-data-services.md)  
  
  
