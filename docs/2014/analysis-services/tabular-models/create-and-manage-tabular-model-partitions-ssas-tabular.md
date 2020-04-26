---
title: 테이블 형식 모델 파티션 만들기 및 관리 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: dab72cf0-95bc-4b63-95dc-505b5cd881c1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 72c5b69aee10d8ac1342b3f037d76ab6ef5fc36c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/25/2020
ms.locfileid: "66067396"
---
# <a name="create-and-manage-tabular-model-partitions-ssas-tabular"></a>테이블 형식 모델 파티션 만들기 및 관리(SSAS 테이블 형식)
  파티션은 테이블을 논리적 부분으로 나눕니다. 각 파티션은 다른 파티션과 별개로 처리(새로 고침)할 수 있습니다. 모델 제작 중에 모델에 대해 정의한 파티션은 배포된 모델에서 복제됩니다. 배포된 후에는 **의** 파티션 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 대화 상자를 사용하거나 스크립트를 사용하여 해당 파티션을 관리할 수 있습니다. 이 항목에서 제공하는 태스크에서는 배포된 모델에 대해 파티션을 만들고 관리하는 방법을 설명합니다.  
  
 이 항목에는 다음 태스크가 포함됩니다.  
  
-   [새 파티션을 만들려면](#bkmk_create_new)  
  
-   [파티션을 복사하려면](#bkmk_copy)  
  
-   [두 개 이상의 파티션을 병합 하려면](#bkmk_merge)  
  
-   [파티션을 삭제하려면](#bkmk_delete)  
  
## <a name="tasks"></a>작업  
 배포된 테이블 형식 모델 데이터베이스에 대해 파티션을 만들고 관리하려면 **의** 파티션 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]대화 상자를 사용합니다. **파티션** 대화 상자를 보려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 테이블을 마우스 오른쪽 단추로 클릭한 다음 **파티션**을 클릭합니다.  
  
###  <a name="to-create-a-new-partition"></a><a name="bkmk_create_new"></a>새 파티션을 만들려면  
  
1.  **파티션** 대화 상자에서 **새로 만들기** 단추를 클릭합니다.  
  
2.  **파티션 이름**에 파티션의 이름을 입력합니다. 기본적으로 기본 파티션의 이름은 새 파티션마다 증분 번호로 지정됩니다.  
  
3.  **SQL 문**에서 파티션에 포함할 열과 절을 정의하는 SQL 쿼리 문을 쿼리 창에 입력하거나 붙여넣습니다.  
  
4.  문의 유효성을 검사하려면 **구문 검사**를 클릭합니다.  
  
###  <a name="to-copy-a-partition"></a><a name="bkmk_copy"></a>파티션을 복사 하려면  
  
1.  **파티션** 대화 상자의 **파티션** 목록에서 복사할 파티션을 선택한 다음 **복사** 단추를 클릭합니다.  
  
2.  **파티션 이름**에 파티션의 새 이름을 입력합니다.  
  
3.  **SQL 문**에서 SQL 쿼리 문을 편집합니다.  
  
###  <a name="to-merge-two-or-more-partitions"></a><a name="bkmk_merge"></a> 두 개 이상의 파티션을 병합하려면  
  
-   **파티션** 대화 상자의 **파티션** 목록에서 Ctrl+클릭을 사용하여 병합할 파티션을 선택한 다음 **병합** 단추를 클릭합니다.  
  
> [!IMPORTANT]  
>  파티션을 병합해도 파티션 메타데이터가 업데이트되지는 않습니다. 처리 작업으로 병합된 파티션의 모든 데이터가 처리되도록 관리자가 결과 파티션에 대해 SQL 문을 수정해야 합니다.  
  
###  <a name="to-delete-a-partition"></a><a name="bkmk_delete"></a>파티션을 삭제 하려면  
  
-   **파티션** 대화 상자의 **파티션** 목록에서 삭제할 파티션을 선택한 다음 **삭제** 단추를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 형식 모델 파티션이 SSAS 테이블 형식&#41;을 &#40;](partitions-ssas-tabular.md)   
 [테이블 형식 모델 파티션 처리&#40;SSAS 테이블 형식&#41;](process-tabular-model-partitions-ssas-tabular.md)  
  
  
