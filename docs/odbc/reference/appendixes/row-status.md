---
title: 행 상태 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ce45314cef92404fe14a43e033c14d6a272e1bf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63262484"
---
# <a name="row-status"></a>행 상태
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 커서 라이브러리 캐시 행 상태에 있는 버퍼를 만듭니다. 커서 라이브러리는이 버퍼에서 행 상태 배열 (SQL_ATTR_ROW_STATUS_PTR 문 특성을 사용 하 여 지정 됨)에 대 한 값을 검색 합니다. 각 행에 대 한 커서 라이브러리는이 버퍼를 설정 합니다.  
  
-   Sql_row_deleted가 배치를 실행할 때 문이 행을 삭제 합니다.  
  
-   사용 하 여 데이터 원본에서 행을 검색 하는 오류가 발생 하면 SQL_ROW_ERROR **SQLFetch**합니다.  
  
-   성공적으로 사용 하 여 데이터 원본의 행을 인출할 때 SQL_ROW_SUCCESS **SQLFetch**합니다.  
  
-   행 위치 지정된 update 문을 실행할 때 SQL_ROW_UPDATED 합니다.
