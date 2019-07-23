---
title: '방법: 오류 수정 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 0d504e00-4ff0-4fdf-b874-85280bbd8668
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ba41850e214de60da9a7e64f328939e4660a9367
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035176"
---
# <a name="how-to-fix-errors"></a>방법: 오류 수정
오류 목록 창에는 모든 배포 또는 빌드 오류가 표시됩니다. 데이터베이스 엔터티와 해당 정의를 편집하는 경우 Transact\-SQL 편집기나 테이블 디자이너에서 수행한 편집 작업으로 인해 발생한 구문 및 의미 오류도 이 목록에 표시됩니다. 오류 목록은 여러 탭에서 스크립트를 편집할 때 동적으로 업데이트됩니다. 그러면 식별된 오류에 따라 보다 세부적으로 문제를 해결할 수 있습니다.  
  
> [!WARNING]  
> 다음 절차에서는 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md) 및 [프로젝트 기반 오프라인 데이터베이스 개발](../ssdt/project-oriented-offline-database-development.md) 섹션의 절차에서 만들어진 엔터티를 사용합니다.  
  
### <a name="to-fix-errors"></a>오류를 수정하려면  
  
1.  **솔루션 탐색기**에서 **Product** 테이블(Product.sql)을 마우스 오른쪽 단추로 클릭하고 **디자이너 보기**를 선택합니다.  
  
2.  디자이너의 열 표에서 **ShelflLife** 열을 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택하여 이 열을 테이블에서 삭제합니다.  
  
3.  화면 아래쪽의 **오류 목록** 창에 다음 팝업과 비슷한 경고 및 오류가 즉시 표시됩니다.  
  
**경고 SQL71502: 함수: 개체에 대한 확인되지 않은 참조가 [dbo].[GetProductsBySupplier]에 포함되어 있습니다. 개체가 없거나, [dbo].[Product].[p]::[ShelfLife] 또는 [dbo].[Product].[ShelfLife].Error SQL71501 개체를 참조할 수 있기 때문에 참조가 모호합니다. 오류 제약 조건: [dbo].[CK_Product_ShelfLife]에 [dbo].[Product].[ShelfLife] 개체에 대한 확인되지 않은 참조가 있습니다.**  
  
4.  **오류 목록**을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴를 사용하여 결과를 정렬하고 표시할 항목과 각 항목에 대해 표시할 정보 열을 필터링할 수 있습니다.  
  
    식별된 첫 번째 경고를 두 번 클릭한 다음 해당 내용에 따라 경고를 생성한 스크립트 파일로 이동합니다. 문제가 있는 코드 섹션은 강조 표시됩니다. 이 예에서는 이전에 만든 테이블 반환 함수의 `RETURN` 및 `SELECT` 문 모두에서 `ShelfLife` 열을 사용하는 것이 문제의 원인입니다.  
  
5.  Transact\-SQL 편집기에서 함수의 `ShelfLife`를 제거합니다.  
  
6.  비슷한 방법으로 CHECK 제약 조건을 제거하여 두 번째 오류를 수정합니다.  
  
7.  문제를 해결하는 즉시 해당 경고 및 오류가 **오류 목록**에서 사라집니다.  
  
## <a name="see-also"></a>참고 항목  
[Transact-SQL 편집기를 사용하여 스크립트 편집 및 실행](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)  
  
