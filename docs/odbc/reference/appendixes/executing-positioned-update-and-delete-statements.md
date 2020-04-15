---
title: 위치 업데이트 및 삭제 명령문 실행 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- ODBC cursor library [ODBC], positioned update or delete
ms.assetid: 1d64f309-2a6e-4ad1-a6b5-e81145549c56
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96a1aa891ef8ba26c6c239cf35e62a8f36018e65
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307004"
---
# <a name="executing-positioned-update-and-delete-statements"></a>위치 지정 업데이트 및 삭제 문 실행
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 응용 프로그램이 **SQLFetchScroll를**사용하여 데이터 블록을 가져온 후 블록의 데이터를 업데이트하거나 삭제할 수 있습니다. 위치 가 있는 업데이트를 실행하거나 삭제하려면 응용 프로그램을 다음을 수행합니다.  
  
1.  **SQLSetPos를** 호출하여 업데이트하거나 삭제할 행의 커서를 배치합니다.  
  
2.  위치 가 있는 업데이트를 구성하거나 다음 구문으로 문을 삭제합니다.  
  
     **테이블** *이름* 업데이트  
  
     **SET** *열 식별자* **=** {*NULL}* &#124; 식 **NULL**  
  
     [**[ 열** *식별자* **=** {*식* &#124; **NULL**}]  
  
     **여기서** *커서 이름의* 현재  
  
     *커서* 이름의 **현재 테이블** *이름에서* **삭제**  
  
     위치 가 있는 업데이트 문에서 **SET** 절을 생성하는 가장 쉬운 방법은 업데이트할 각 열에 대한 매개 변수 마커를 사용하고 **SQLBindParameter를** 사용하여 업데이트할 행의 행 집합 버퍼에 바인딩하는 것입니다. 이 경우 매개 변수의 C 데이터 형식은 행 집합 버퍼의 C 데이터 형식과 동일합니다.  
  
3.  위치 가 있는 업데이트 문을 실행 하는 경우 현재 행에 대 한 행 집합 버퍼를 업데이트 합니다. 위치 가 있는 업데이트 문을 성공적으로 실행한 후 커서 라이브러리는 현재 행의 각 열에서 해당 캐시에 값을 복사합니다.  
  
    > [!CAUTION]  
    >  응용 프로그램이 위치 가 있는 업데이트 문을 실행하기 전에 행 집합 버퍼를 올바르게 업데이트하지 않으면 문이 실행된 후 캐시의 데이터가 올바르지 않습니다.  
  
4.  커서와 연결된 문과 다른 문을 사용하여 위치 가 있는 업데이트 또는 delete 문을 실행합니다.  
  
    > [!CAUTION]  
    >  현재 행을 식별하기 위해 커서 라이브러리에서 생성한 **WHERE** 절은 행을 식별하거나 다른 행을 식별하거나 두 개 이상의 행을 식별하지 못할 수 있습니다. 자세한 내용은 [검색된 명령문 생성](../../../odbc/reference/appendixes/constructing-searched-statements.md)을 참조하십시오.  
  
 위치가 있는 모든 업데이트 및 삭제 문은 커서 이름이 필요합니다. 커서 이름을 지정하려면 커서가 열리기 전에 응용 프로그램에서 **SQLSetCursorName을** 호출합니다. 드라이버에서 생성된 커서 이름을 사용하려면 커서가 열린 후 응용 프로그램에서 **SQLGetCursorName을** 호출합니다.  
  
 커서 라이브러리가 위치 업데이트 또는 delete 문을 실행한 후 커서 라이브러리에서 유지 관리하는 상태 배열, 행 집합 버퍼 및 캐시에는 다음 표에 표시된 값이 포함됩니다.  
  
|사용된 명령문|행 상태 배열의 값|에서 값<br /><br /> 행 집합 버퍼|에서 값<br /><br /> 캐시 버퍼|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|위치 지정 업데이트|SQL_ROW_UPDATED|새 값[1]|새 값[1]|  
|위치 삭제|SQL_ROW_DELETED|이전 값|이전 값|  
  
 [1] 응용 프로그램은 위치 가 있는 업데이트 문을 실행하기 전에 행 집합 버퍼의 값을 업데이트해야 합니다. 위치 업데이트 문을 실행한 후 커서 라이브러리는 행 집합 버퍼의 값을 캐시에 복사합니다.
