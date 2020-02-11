---
title: 병합 복제를 위한 아티클 옵션 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], article options
- articles [SQL Server replication], merge replication options
ms.assetid: 670abd41-d204-4cd7-a371-7664e603a0ce
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7033db55df0dd9b25c3dee5accdd4259842a571b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62999615"
---
# <a name="article-options-for-merge-replication"></a>병합 복제를 위한 아티클 옵션
  애플리케이션의 요구에 맞게 복제 동작을 사용자 지정할 수 있는 여러 가지 병합 테이블 아티클 옵션이 있습니다. 병합 복제를 사용하여 다음을 수행할 수 있습니다.  
  
-   행 필터, 조인 필터 및 열 필터를 사용합니다. 테이블 아티클을 필터링하여 게시할 데이터 파티션을 만들 수 있습니다. 자세한 내용은 [게시된 데이터 필터링](../publish/filter-published-data.md)을 참조하세요.  
  
-   구독자의 변경 내용을 게시자로 업로드할지 여부를 지정합니다. 데이터의 일부 또는 전체가 구독자에서 읽기 전용이어야 하는 애플리케이션의 경우 다운로드 전용 아티클을 사용하면 성능상의 이점이 있습니다. 자세한 내용은 [다운로드 전용 아티클로 병합 복제 성능 최적화](optimize-merge-replication-performance-with-download-only-articles.md)를 참조하세요.  
  
-   복제 트리거 및 시스템 테이블에서 하나 이상의 아티클에 대한 삭제를 추적하지 않도록 지정합니다. 이 옵션은 많은 애플리케이션 시나리오에서 유용하게 사용됩니다. 복제할 필요가 없는 일괄 처리 삭제를 사용하는 시나리오도 여기에 포함됩니다. 자세한 내용은 [조건부 삭제 추적으로 병합 복제 성능 최적화](optimize-merge-replication-performance-with-conditional-delete-tracking.md)를 참조하세요.  
  
-   애플리케이션에 필요한 순서대로 아티클이 처리되도록 아티클의 처리 순서를 지정합니다. 자세한 내용은 [병합 복제 속성 지정](../publish/specify-merge-replication-properties.md)을 참조하세요.  
  
-   관련된 레코드 집합이 하나의 단위로 처리되도록 지정합니다. 기본적으로 병합 복제는 행 단위로 테이블 변경 내용을 처리합니다. 자세한 내용은 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](group-changes-to-related-rows-with-logical-records.md)를 참조하세요.  
  
-   같은 데이터를 토폴로지에 있는 두 개 이상의 노드에서 변경할 수 있는 경우에 충돌 감지 및 해결 기능을 사용합니다. 자세한 내용은 [병합 복제 충돌 감지 및 해결](advanced-merge-replication-conflict-detection-and-resolution.md)을 참조하세요.  
  
-   제약 조건 및 트리거를 구독자로 복사할지 여부와 같은 스키마 옵션을 지정합니다. 자세한 내용은 [스키마 옵션 지정](../publish/specify-schema-options.md)을 참조하세요.  
  
-   비즈니스 논리 처리기를 사용하여 동기화 중에 발생하는 여러 조건들에 응답할 수 있습니다. 이러한 조건으로는 데이터 변경, 충돌 및 오류가 포함됩니다. 자세한 내용은 [병합 동기화 중 비즈니스 논리 실행](execute-business-logic-during-merge-synchronization.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 및 데이터베이스 개체 게시](../publish/publish-data-and-database-objects.md)  
  
  
