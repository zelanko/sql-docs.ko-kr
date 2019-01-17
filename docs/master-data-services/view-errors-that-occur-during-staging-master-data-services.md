---
title: 준비 과정에서 발생하는 오류 보기(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- staging process [Master Data Services], viewing errors
ms.assetid: 6d2bff84-624b-47fc-a4a5-d9ea01d13412
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 9f4e66d45a7116f20d4903da21508d0d22c6da61
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52817675"
---
# <a name="view-errors-that-occur-during-staging-master-data-services"></a>준비 과정에서 발생하는 오류 보기(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 준비 프로세스 동안 발생하는 오류를 볼 수 있습니다. [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에는 오류를 표시하는 두 개의 뷰가 있습니다.  
  
-   stg.viw_name_MemberErrorDetails 뷰는 리프 또는 통합 멤버 업데이트를 표시합니다.  
  
-   stg.viw_name_RelationshipErrorDetails 뷰는 계층 관계 업데이트를 표시합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에서 stg.viw_name_MemberErrorDetails 또는 stg.viw_name_RelationshipErrorDetails 뷰에 대한 SELECT 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
### <a name="to-view-staging-errors"></a>준비 오류를 보려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 을 열고 [!INCLUDE[ssDE](../includes/ssde-md.md)] 데이터베이스의 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 인스턴스에 연결합니다.  
  
2.  새 쿼리를 엽니다.  
  
3.  다음 텍스트를 입력하여 준비 테이블의 이름을 예를 들어 viw_Product_MemberErrorDetails 등으로 바꿉니다.  
  
     `SELECT * FROM stg.viw_name_MemberErrorDetails`  
  
4.  쿼리를 실행합니다. 오류 세부 정보가 **ErrorDescription** 필드에 표시됩니다.  
  
## <a name="next-steps"></a>Next Steps  
 오류 메시지에 대한 자세한 내용은 [준비 프로세스 오류&#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [개요: 테이블에서 데이터 가져오기&#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [준비 프로세스 문제 해결(Master Data Services)](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-the-staging-process-master-data-services.aspx)  
  
  
