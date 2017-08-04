---
title: "(Master Data Services)를 준비 하는 동안 발생 하는 오류 보기 | Microsoft Docs"
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
- staging process [Master Data Services], viewing errors
ms.assetid: 6d2bff84-624b-47fc-a4a5-d9ea01d13412
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3a5ecc701aa1eab2162c41724b3a7a3319d8eb68
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="view-errors-that-occur-during-staging-master-data-services"></a>준비 과정에서 발생하는 오류 보기(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 준비 프로세스 동안 발생하는 오류를 볼 수 있습니다. [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에는 오류를 표시하는 두 개의 뷰가 있습니다.  
  
-   stg.viw_name_MemberErrorDetails 뷰는 리프 또는 통합 멤버 업데이트를 표시합니다.  
  
-   stg.viw_name_RelationshipErrorDetails 뷰는 계층 관계 업데이트를 표시합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에서 stg.viw_name_MemberErrorDetails 또는 stg.viw_name_RelationshipErrorDetails 뷰에 대한 SELECT 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
### <a name="to-view-staging-errors"></a>준비 오류를 보려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 을 열고 [!INCLUDE[ssDE](../includes/ssde-md.md)] 데이터베이스의 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 인스턴스에 연결합니다.  
  
2.  새 쿼리를 엽니다.  
  
3.  다음 텍스트를 입력하여 준비 테이블의 이름을 예를 들어 viw_Product_MemberErrorDetails 등으로 바꿉니다.  
  
     `SELECT * FROM stg.viw_name_MemberErrorDetails`  
  
4.  쿼리를 실행합니다. 오류 세부 정보가 **ErrorDescription** 필드에 표시됩니다.  
  
## <a name="next-steps"></a>다음 단계  
 오류 메시지에 대한 자세한 내용은 [준비 프로세스 오류&#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [개요: 테이블에서 데이터 가져오기&#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [준비 프로세스 문제 해결(Master Data Services)](http://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-the-staging-process-master-data-services.aspx)  
  
  
