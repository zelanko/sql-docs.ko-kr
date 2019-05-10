---
title: 게시 데이터 (MDS 추가 기능 Excel 용) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: ea84a9aa-aeec-411b-ab8d-bc1b14f864a3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: dd5046c9a307f498ffb585c99cba8044c7b18b3f
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65479029"
---
# <a name="publishing-data-mds-add-in-for-excel"></a>데이터 게시(Excel용 MDS 추가 기능)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서 데이터를 다른 사용자와 공유하려는 경우 데이터를 MDS 리포지토리에 게시합니다. 데이터가 게시되는 즉시 추가 기능의 다른 사용자가 다운로드할 수 있습니다.  
  
 데이터를 게시하면 사용자가 이전에 추가했거나 업데이트한 모든 데이터가 MDS 저장소에 게시됩니다. 삭제한 데이터가 게시되지 않았습니다. 데이터를 개별적으로 삭제해야 합니다. 자세한 내용은 [행 삭제&#40;Excel용 MDS 추가 기능&#41;](delete-a-row-mds-add-in-for-excel.md)를 참조하세요.  
  
> [!NOTE]  
>  게시는 새 엔터티를 만드는 방법으로 사용할 수 없습니다. 엔터티를 만드는 방법에 대한 자세한 내용은 [엔터티 만들기&#40;Excel용 MDS 추가 기능&#41;](create-an-entity-mds-add-in-for-excel.md)를 참조하세요.  
  
## <a name="when-multiple-users-publish-at-the-same-time"></a>동시에 여러 사용자가 게시하는 경우  
 여러 사용자가 동일 데이터에 업데이트를 게시할 수 있습니다. 각 사용자가 게시할 때마다 업데이트가 데이터베이스에 저장됩니다. 즉, 최신 업데이트된 데이터를 사용 중이 아닌 사용자도 자신이 게시를 수행할 때 값을 변경할 수 있습니다.  
  
 자신이 작성한 업데이트만 데이터베이스에 게시됩니다. 워크시트에서 오래된 데이터는 게시되지 않습니다.  
  
## <a name="transactions-and-annotations"></a>트랜잭션 및 주석  
 게시된 각 변경 내용은 트랜잭션으로 저장됩니다. 필요에 따라 트랜잭션에 변경 이유에 대해 설명하는 주석(설명)을 추가할 수 있습니다.  
  
-   삭제도 관리자가 다시 되돌릴 수 있는 트랜잭션으로 저장되지만 삭제에 대해서는 주석을 달 수 없습니다.  
  
-   변경 하는 경우는 **코드** 값 멤버에 대 한 트랜잭션으로 기록 되지 않습니다 및 멤버에 대 한 이전의 모든 트랜잭션을 사용할 수 없습니다.  
  
-   다른 사용자가 멤버에 대해 수행한 트랜잭션을 볼 수 있습니다. 또한 사용자에게 특정 특성에 대한 권한이 없더라도 멤버에 대해 자신이 수행한 모든 트랜잭션을 볼 수 있습니다.  
  
 멤버에 대한 모든 트랜잭션을 볼 수 있습니다. 자세한 내용은 [멤버에 대한 모든 주석 또는 트랜잭션 보기&#40;Excel용 MDS 추가 기능&#41;](view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  주석을 500자 이상으로 입력하면 주석이 자동으로 잘립니다.  
  
## <a name="business-rule-and-other-validation"></a>비즈니스 규칙 및 기타 유효성 검사  
 데이터를 게시할 때는 데이터를 MDS 저장소에 추가하기 전에 데이터가 정확한지 확인하기 위해 유효성 검사가 수행됩니다. 데이터가 지정된 조건에 맞지 않으면 저장소에 게시되지 않습니다. 자세한 내용은 [데이터 유효성 검사&#40;Excel용 MDS 추가 기능&#41;](validating-data-mds-add-in-for-excel.md)를 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|활성 워크시트에서 다시 MDS 저장소로 데이터를 게시합니다.|[Excel에서 MDS로 데이터를 게시 &#40;MDS 추가 기능에 Excel 용&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|MDS 저장소에서 행을 삭제하고 동시에 워크시트에서도 행을 삭제합니다.|[행 삭제&#40;Excel용 MDS 추가 기능&#41;](delete-a-row-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [데이터 새로 고침&#40;Excel용 MDS 추가 기능&#41;](refreshing-data-mds-add-in-for-excel.md)  
  
-   [Microsoft Excel용 Master Data Services 추가 기능](master-data-services-add-in-for-microsoft-excel.md)  
  
  
