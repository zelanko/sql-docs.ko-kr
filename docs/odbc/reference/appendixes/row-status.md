---
title: 행 상태 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- row status [ODBC]
- cache [ODBC]
ms.assetid: 0f0b1fb6-f697-4ced-811c-2908e210bc71
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d4ae4169dc3f2a491663f4a86c564cfee5c2f4d6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305102"
---
# <a name="row-status"></a>행 상태
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 커서 라이브러리는 행 상태에 대한 캐시에 버퍼를 만듭니다. 커서 라이브러리는 이 버퍼에서 행 상태 배열(SQL_ATTR_ROW_STATUS_PTR 문 특성으로 지정됨)에 대한 값을 검색합니다. 각 행에 대해 커서 라이브러리는 이 버퍼를 다음과 같은 것으로 설정합니다.  
  
-   행에 위치 지정 된 delete 문을 실행할 때 SQL_ROW_DELETED.  
  
-   SQL_ROW_ERROR 데이터 원본에서 행을 검색하는 오류가 발생하면 **SQLFetch**.  
  
-   **SQL_ROW_SUCCESS SQLFetch**.  
  
-   행에 위치 된 업데이트 문을 실행 하는 경우 SQL_ROW_UPDATED 합니다.
