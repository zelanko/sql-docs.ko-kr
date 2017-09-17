---
title: "행 상태 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- row status [ODBC]
- cache [ODBC]
ms.assetid: 0f0b1fb6-f697-4ced-811c-2908e210bc71
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8f164b8269e1150cdf7a85e486bcc3fd93a9411f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="row-status"></a>행 상태
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 커서 라이브러리 행 상태에 대 한 캐시의 버퍼를 만듭니다. 커서 라이브러리는이 버퍼에서 행 상태 배열이 (SQL_ATTR_ROW_STATUS_PTR 문 특성으로 지정)에 대 한 값을 검색 합니다. 각 행에 대해 커서 라이브러리가이 버퍼를 설정합니다.  
  
-   Sql_row_deleted가 배치를 실행 하는 경우에 행에는 문을 삭제 합니다.  
  
-   사용 하 여 데이터 소스에서 행을 검색 하는 오류가 발생 하면 SQL_ROW_ERROR **SQLFetch**합니다.  
  
-   성공적으로 사용 하 여 데이터 소스에서 행을 인출할 때 SQL_ROW_SUCCESS **SQLFetch**합니다.  
  
-   행에 위치 지정된 update 문을 실행할 때 SQL_ROW_UPDATED 합니다.
