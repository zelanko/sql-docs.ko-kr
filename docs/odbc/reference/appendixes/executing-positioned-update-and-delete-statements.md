---
title: Update 및 Delete 문을 배치 실행 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- ODBC cursor library [ODBC], positioned update or delete
ms.assetid: 1d64f309-2a6e-4ad1-a6b5-e81145549c56
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e7099999311d565af4eeff5943306c927d81f3b9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="executing-positioned-update-and-delete-statements"></a>위치 지정된 Update 및 Delete 문을 실행합니다.
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 응용 프로그램에 사용 하 여 데이터 블록을 인출 된 후 **SQLFetchScroll**, 블록의 데이터를 삭제 하거나 업데이트할 수 있습니다. 한 위치 지정된 업데이트 또는 삭제, 응용 프로그램을 실행 합니다.  
  
1.  호출 **SQLSetPos** 를 업데이트 하거나 삭제할 행에 커서를 배치 합니다.  
  
2.  위치 지정된 update 또는 delete 문의 다음 구문으로 생성합니다.  
  
     **업데이트** *테이블 이름*  
  
     **설정** *열 식별자* **=** {*식* &#124; **NULL**}  
  
     [**,** *열 식별자* **=** {*식* &#124; **NULL**}]  
  
     **WHERE CURRENT OF** *커서 이름*  
  
     **DELETE FROM** *테이블 이름* **WHERE CURRENT OF** *커서 이름*  
  
     생성 하는 가장 쉬운 방법은 **설정** 위치 지정된 update 문에 절을 업데이트 하 고 사용 하 여 각 열에 대 한 매개 변수 표식을 사용 하는 것 **SQLBindParameter** 에 대 한 행 집합 버퍼에 바인딩하는 행을 업데이트 합니다. 이 경우 행 집합 버퍼의 C 데이터 형식과 동일 매개 변수의 C 데이터 형식이 됩니다.  
  
3.  위치 지정된 update 문이 실행 될 경우 현재 행에 대 한 행 집합 버퍼를 업데이트 합니다. 위치 지정된 update 문의 성공적으로 실행 한 후 커서 라이브러리는 현재 행의 각 열에서 값의 캐시에 복사 합니다.  
  
    > [!CAUTION]  
    >  응용 프로그램 업데이트 되지 않는 경우 제대로 행 집합 버퍼 위치 지정된 update 문을 실행 하기 전에, 캐시의 데이터가 잘못 됩니다는 문이 실행 된 후입니다.  
  
4.  위치 지정된 update 또는 delete 문은 커서와 관련 된 문 보다 다른 문을 사용 하 여 실행 합니다.  
  
    > [!CAUTION]  
    >  **여기서** 절 현재 행을 식별 하는 커서 라이브러리에서 생성 된 모든 행을 식별 하 고, 다른 행을 식별 또는 둘 이상의 행을 식별 되지 않을 수 있습니다. 자세한 내용은 참조 [검색 문을 생성](../../../odbc/reference/appendixes/constructing-searched-statements.md)합니다.  
  
 모든 업데이트를 배치 하 고 delete 문은 커서 이름이 필요 합니다. 응용 프로그램이 커서 이름을 지정 하려면 호출 **SQLSetCursorName** 커서를 열기 전에 합니다. 드라이버에 의해 생성 된 커서 이름을 사용 하려면 응용 프로그램이 호출 **SQLGetCursorName** 커서가 열린 후 합니다.  
  
 Delete 문, 상태 배열, 행 집합 버퍼 및 커서 라이브러리에서 유지 관리 하는 캐시는 다음 표에 표시 된 값이 포함 또는 커서 뒤 라이브러리 위치 지정된 업데이트를 실행 합니다.  
  
|문 사용|행 상태 배열이 값|값<br /><br /> 버퍼 행 집합|값<br /><br /> 캐시 버퍼|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|위치 지정 업데이트|SQL_ROW_UPDATED|새 값 [1]|새 값 [1]|  
|위치 지정된 delete|SQL_ROW_DELETED|이전 값|이전 값|  
  
 [1] 응용 프로그램 위치 지정된 update 문의 실행 하기 전에 행 집합 버퍼의 값을 업데이트 해야 합니다. 을 위치 지정된 update 문을 실행 한 후 커서 라이브러리는 행 집합 버퍼의 값을 캐시 복사 합니다.
