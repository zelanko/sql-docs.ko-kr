---
title: ODBC 정적 커서 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], static
- static cursors [ODBC]
ms.assetid: 28cb324c-e1c3-4b5c-bc3e-54df87037317
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b99566c473e88684e8b092a5ac9fc899e7dce177
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282450"
---
# <a name="odbc-static-cursors"></a>ODBC 정적 커서
정적 커서는 결과 집합이 정적인 것처럼 보이는 커서입니다. 일반적으로 커서를 연 후 결과 집합의 멤버 자격, 순서 또는 값에 대한 변경 내용을 검색하지 않습니다. 예를 들어 정적 커서가 행을 가져오고 다른 응용 프로그램이 해당 행을 업데이트한다고 가정합니다. 정적 커서가 행을 다시 가져오는 경우 다른 응용 프로그램에서 변경한 변경에도 불구하고 표시되는 값은 변경되지 않습니다.  
  
 정적 커서는 이 작업을 수행할 필요는 없지만 자체 업데이트, 삭제 및 삽입을 검색할 수 있습니다. 특정 정적 커서가 이러한 변경 내용을 감지하는지 여부는 **SQLGetInfo**의 SQL_STATIC_SENSITIVITY 옵션을 통해 보고됩니다. 정적 커서는 다른 업데이트, 삭제 및 삽입을 감지하지 않습니다.  
  
 SQL_ATTR_ROW_STATUS_PTR 문 특성에 의해 지정된 행 상태 배열은 모든 행에 대한 SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO 또는 SQL_ROW_ERROR 포함할 수 있습니다. 커서가 이러한 변경 내용을 감지할 수 있다고 가정하여 커서에 의해 업데이트, 삭제 또는 삽입된 행에 대해 SQL_ROW_UPDATED, SQL_ROW_DELETED 또는 SQL_ROW_ADDED 반환합니다.  
  
 정적 커서는 일반적으로 결과 집합의 행을 잠그거나 결과 집합의 복사본 또는 스냅숏을 만들어 구현합니다. 행을 잠그는 것은 비교적 쉽지만 동시성을 크게 줄이는 단점이 있습니다. 복사본을 만들면 동시성이 높아지고 커서가 복사본을 수정하여 자체 업데이트, 삭제 및 삽입을 추적할 수 있습니다. 그러나 복사본을 만드는 데 비용이 더 많이 들며 다른 사용자가 데이터를 변경하므로 기본 데이터와 다를 수 있습니다.
