---
title: "비즈니스 규칙 확장(Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4c18be5f-a3fa-45a8-9be6-0f45f58bbc9e
caps.latest.revision: 16
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: e83f09094cde9a2643913fceae32d1f6a07a7c09
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="business-rules-extension-master-data-services"></a>비즈니스 규칙 확장(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 사용자 정의 SQL 스크립트를 미리 정의된 조건과 동작의 확장으로 적용할 수 있습니다.  
  
> [!NOTE]  
>  모든 스크립트는 [usr] 스키마에서 정의해야 합니다.  
  
 다음 기준을 충족하는 SQL 함수를 비즈니스 규칙 조건으로 사용할 수 있습니다.  
  
-   반환 값 형식이 BIT여야 합니다.  
  
-   매개 변수 형식으로는 다음과 같은 형식만 지원됩니다.  
  
    -   NVARCHAR  
  
    -   DATETIME2  
  
    -   DECIMAL(전체 자릿수, 소수 자릿수)  
  
         전체 자릿수는 38이어야 합니다.  
  
         소수 자릿수 값은 0에서 7 사이여야 합니다.  
  
 다음 구문을 사용하는 SQL 저장 프로시저를 비즈니스 규칙 동작으로 사용할 수 있습니다.  
  
```  
CREATE PROCEDURE [usr].[YourAction]  
       (         
            @MemberIdList mdm.[MemberId] READONLY,  
            @ModelName NVARCHAR(MAX),  
            @VersionName NVARCHAR(MAX),  
            @EntityName NVARCHAR(MAX),  
            @BusinessRuleName NVARCHAR(MAX)  
        )    
      AS BEGIN    
       ...     
       END  
  
```  
  
 사용자 정의 스크립트는 배포 패키지에 추가되지 않습니다. 패키지를 배포하기 전에 대상 Master Data Services 데이터베이스가 비즈니스 규칙에 사용되는 모든 스크립트를 포함하고 있는지 확인하세요.  
  
 스크립트 작업은 다음 권한이 있는 mds_br_user로 실행됩니다.  
  
|||  
|-|-|  
|**스키마**|**Permissions**|  
|mdm|SELECT|  
|stg|SELECT, UPDATE, DELETE, EXECUTE, INSERT|  
|usr|FULL|  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   시스템 관리 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
-   사용자 정의 스크립트를 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에 추가해야 합니다.  
  
## <a name="create-a-business-rule-to-take-a-user-defined-script-as-a-condition-or-as-an-action"></a>사용자 정의 스크립트를 조건이나 동작으로 사용하는 비즈니스 규칙 만들기  
  
1.  마스터 데이터 관리자에서 **시스템 관리자**를 클릭합니다.  
  
2.  메뉴 모음에서 **관리** 를 가리키고 **비즈니스 규칙**을 클릭합니다.  
  
3.  **비즈니스 규칙** 페이지의 **모델** 드롭다운 목록에서 모델을 선택합니다.  
  
4.  **엔터티** 드롭다운 목록에서 엔터티를 선택합니다.  
  
5.  **멤버 유형** 드롭다운 목록에서 비즈니스 규칙을 적용할 멤버 유형을 선택합니다.  
  
6.  **추가**를 클릭합니다.  
  
7.  다음 단계를 수행하여 사용자 지정 스크립트를 조건으로 만듭니다.  
  
    1.  **If** 블록 아래에서 **추가** 단추를 클릭합니다. 그러면 패널이 표시됩니다.  
  
    2.  **연산자** 드롭다운 목록의 **사용자 정의 스크립트** 에서 사용자 정의 함수를 선택합니다.  
  
    3.  사용자 정의 함수의 모든 매개 변수가 표시됩니다.  
  
    4.  각 매개 변수에 값을 할당합니다.  
  
    5.  **저장**을 클릭합니다.  
  
8.  다음 단계를 수행하여 사용자 지정 스크립트를 동작으로 지정합니다.  
  
    1.  **Then** 블록 아래에서 **추가** 단추를 클릭합니다. 그러면 패널이 표시됩니다.  
  
    2.  **연산자** 드롭다운 목록의 **사용자 정의 스크립트** 에서 사용자 정의 함수를 선택합니다.  
  
    3.  **저장**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [비즈니스 규칙&#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [비즈니스 규칙 조건&#40;Master Data Services&#41;](../master-data-services/business-rule-conditions-master-data-services.md)   
 [비즈니스 규칙 동작&#40;Master Data Services&#41;](../master-data-services/business-rule-actions-master-data-services.md)  
  
  

