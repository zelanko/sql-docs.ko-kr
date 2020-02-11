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
ms.openlocfilehash: a62bad0e69a8bf8b5365575f97e4791cbbf270d6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057115"
---
# <a name="row-status"></a>행 상태
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 커서 라이브러리는 행 상태에 대해 캐시에 버퍼를 만듭니다. 커서 라이브러리는이 버퍼에서 행 상태 배열 (SQL_ATTR_ROW_STATUS_PTR statement 특성으로 지정)에 대 한 값을 검색 합니다. 각 행에 대해 커서 라이브러리는 다음 버퍼를로 설정 합니다.  
  
-   행에서 배치 된 delete 문을 실행할 때 SQL_ROW_DELETED 합니다.  
  
-   **Sqlfetch**를 사용 하 여 데이터 원본에서 행을 검색 하는 동안 오류가 발생 하는 경우를 SQL_ROW_ERROR 합니다.  
  
-   **Sqlfetch**를 사용 하 여 데이터 원본에서 행을 성공적으로 인출할 때 SQL_ROW_SUCCESS 합니다.  
  
-   행에서 위치 지정 update 문을 실행할 때 SQL_ROW_UPDATED 합니다.
