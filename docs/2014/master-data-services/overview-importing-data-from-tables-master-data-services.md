---
title: 데이터 가져오기 (MDS(Master Data Services)) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- staging process [Master Data Services], about staging process
- importing data [Master Data Services]
- staging process [Master Data Services]
ms.assetid: 181d1e22-379c-45d1-b03c-e1e22ff14164
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3d1ad35a40e4218bfef44daeec01ee03fc0c7c78
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175992"
---
# <a name="data-import-master-data-services"></a>데이터 가져오기(Master Data Services)
  
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 데이터에 대한 모델을 만들면 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에서 데이터 추가를 시작하고 데이터를 변경할 수 있습니다.   
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 준비 표, 저장 프로시저 및 마스터 데이터 관리자를 사용할 수 있습니다.

 를 사용 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]하 여 데이터를 MDS 리포지토리 ([!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스)에 추가할 수도 있습니다. [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] 자세한 내용은 [Excel용 MDS 추가 기능&#41;&#40;게시 데이터 ](microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)를 참조 하세요.

 데이터를 추가 및 업데이트할 때 다음을 수행할 수 있습니다.

-   멤버 로드 및 업데이트, 특성 값 업데이트

-   멤버 비활성화 및 삭제

-   명시적 계층 멤버 이동

 데이터를 추가하고 업데이트하는 절차에는 다음의 주요 작업이 포함됩니다.

1.  
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스의 준비 표에 데이터를 로드합니다.

2.  준비 표의 데이터를 적절한 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 표에 로드합니다.

     준비 저장 프로시저나 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 를 사용하여 데이터를 로드합니다.

> [!NOTE]
>  
  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]에서는 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 준비 프로세스에 대한 지원이 제공되지 않습니다.

## <a name="deactivating-and-deleting-members"></a>멤버 비활성화 및 삭제
 비활성화하면 멤버를 다시 활성화할 수 없습니다. 멤버를 다시 활성화하는 경우 계층 및 컬렉션에서 해당 특성 및 멤버 자격이 복원됩니다. 모든 이전 트랜잭션은 그대로 유지됩니다. 관리자는 마스터 데이터 관리자의 **버전 관리** 기능 영역에서 비활성화 트랜잭션을 볼 수 있습니다.

 삭제는 멤버를 영구적으로 시스템에서 삭제합니다. 멤버의 모든 트랜잭션, 모든 관계 및 모든 특성이 영구적으로 삭제됩니다.

> [!NOTE]
>  준비를 사용하여 멤버를 다시 활성화할 수 없습니다. 마스터 데이터 관리자에서 수동으로 수행해야 합니다. 자세한 내용은 [멤버 또는 컬렉션 다시 활성화&#40;Master Data Services&#41;](reactivate-a-member-or-collection-master-data-services.md)를 참조하세요.
> 
>  준비를 사용하여 컬렉션을 삭제하거나 비활성화할 수 없습니다. 컬렉션을 수동으로 비활성화하는 방법에 대한 자세한 내용은 [멤버 또는 컬렉션 삭제&#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-member-or-collection-master-data-services.md)를 참조하세요.

## <a name="moving-explicit-hierarchy-members"></a>명시적 계층 멤버 이동
 명시적 계층에서 멤버 위치를 대량으로 이동할 때 다음을 지정할 수 있습니다.

-   통합 멤버의 부모 자격을 가지는 통합 멤버

-   리프 멤버의 부모 자격을 가지는 통합 멤버

-   리프 또는 통합 멤버의 형제 자격을 가지는 리프 멤버

-   리프 또는 통합 멤버의 형제 자격을 가지는 통합 멤버

## <a name="staging-tables-and-stored-procedures"></a>준비 표 및 저장 프로시저
 
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에는 보유한 데이터로 채울 수 있는 다음 유형의 준비 표가 포함되어 있습니다.

-   [리프 멤버 준비 테이블 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/leaf-member-staging-table-master-data-services.md)

-   [통합 멤버 준비 테이블 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/consolidated-member-staging-table-master-data-services.md)

-   [관계 준비 테이블 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/relationship-staging-table-master-data-services.md)

 모델의 각 엔터티에 대해 준비 표가 있습니다. 표 이름은 해당 엔터티 및 리프 멤버 등의 엔터티 형식을 나타냅니다. 다음 이미지는 통화, 고객 및 제품 엔터티에 대한 준비 표를 보여 줍니다.

 ![MDS 데이터베이스의 준비 테이블](../../2014/master-data-services/media/mds-stagingtables.png "MDS 데이터베이스의 준비 테이블")

 표의 이름은 엔터티를 만들 때 지정되며 변경할 수 없습니다. 준비 테이블 이름에 _1이나 기타 번호가 포함되면 엔터티 작성 시 해당 이름의 다른 테이블이 이미 있는 것입니다.

 
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 는 다음 유형의 준비 저장 프로시저를 포함합니다.

-   stg.udp_\<name>_Leaf

-   stg.udp_\<name>_Consolidated

-   stg.udp_\<name>_Relationship

 모델의 각 엔터티에는 리프 멤버, 통합 멤버 및 관계 준비 표에 해당하는 3개의 저장 프로시저가 있습니다.  다음 이미지는 통화, 고객 및 제품 엔터티에 대한 준비 저장 프로시저를 보여 줍니다.

 ![MDS 데이터베이스의 저장 프로시저를 준비](../../2014/master-data-services/media/mds-stagingstoredprocedures.png "MDS 데이터베이스의 저장 프로시저를 준비")

 저장 프로시저에 대한 자세한 내용은 [준비 저장 프로시저&#40;Master Data Services&#41;](../../2014/master-data-services/staging-stored-procedure-master-data-services.md)를 참조하세요.

## <a name="logging-transactions"></a>트랜잭션 로깅
 데이터 또는 관계를 가져오거나 업데이트할 때 발생하는 모든 트랜잭션을 로깅할 수 있습니다. 이러한 로깅은 저장 프로시저 옵션을 통해 설정합니다. 
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]를 사용하여 준비 프로세스를 시작하는 경우에는 로깅이 발생하지 않습니다.

 
  [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]의 **준비 트랜잭션 기록** 설정은 이 데이터 준비 방법에 적용되지 않습니다.

## <a name="related-content"></a>관련 내용

-   [유효성 검사 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/validation-master-data-services.md)

-   [비즈니스 규칙 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/business-rules-master-data-services.md)


