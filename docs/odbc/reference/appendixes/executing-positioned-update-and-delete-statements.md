---
title: 위치 지정 업데이트 및 삭제 문을 실행 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2391c01d93c876562ab9d870ab0dba22bf74cea5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772051"
---
# <a name="executing-positioned-update-and-delete-statements"></a>위치 지정 업데이트 및 삭제 문 실행
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 응용 프로그램에 블록을 사용 하 여 데이터를 가져온 후 **SQLFetchScroll**를 업데이트 하거나 블록에서 데이터를 삭제할 수 있습니다. 위치 지정된 업데이트 또는 삭제, 응용 프로그램을 실행 합니다.  
  
1.  호출 **SQLSetPos** 를 업데이트 하거나 삭제할 행에 커서를 배치 합니다.  
  
2.  위치 지정된 update 또는 delete 문을 다음 구문 사용 하 여 생성합니다.  
  
     **업데이트** *테이블 이름*  
  
     **설정할** *열 식별자* **=** {*식* &#124; **NULL**}  
  
     [**하십시오** *열 식별자* **=** {*식* &#124; **NULL**}]  
  
     **WHERE CURRENT OF** *커서 이름*  
  
     **DELETE FROM** *테이블 이름* **WHERE CURRENT OF** *커서 이름*  
  
     생성 하는 가장 쉬운 방법은 합니다 **설정** 업데이트를 사용 하 여 각 열에 대 한 매개 변수 표식을 사용 하는 위치 지정된 update 문에 절은 **SQLBindParameter** 이러한 행 집합에 대 한 버퍼에 바인딩할는 업데이트할 행입니다. 이 경우 행 집합 버퍼의 C 데이터 형식과 같은 C 데이터 형식의 매개 변수가 됩니다.  
  
3.  위치 지정된 update 문이 실행 될 경우 현재 행에 대 한 행 집합 버퍼를 업데이트 합니다. 위치 지정된 update 문의 성공적으로 실행 한 후 커서 라이브러리는 현재 행의 각 열에서 값을 해당 캐시에 복사 합니다.  
  
    > [!CAUTION]  
    >  응용 프로그램 업데이트 되지 않는 경우 올바르게 행 집합 버퍼 위치 지정된 update 문을 실행 하기 전에, 캐시의 데이터가 생깁니다 문이 실행 된 후입니다.  
  
4.  위치 지정된 update 또는 delete 문은 커서에 연관 된 문 보다 다른 문을 사용 하 여 실행 합니다.  
  
    > [!CAUTION]  
    >  합니다 **여기서** 절 현재 행을 식별 하려면 커서 라이브러리에 의해 생성 된 모든 행을 식별 하 고, 다른 행을 식별 또는 둘 이상의 행을 식별 하지 못할 수 있습니다. 자세한 내용은 [검색 문을 생성](../../../odbc/reference/appendixes/constructing-searched-statements.md)합니다.  
  
 모든 배치 업데이트 및 delete 문은 커서 이름이 필요 합니다. 커서 이름을 지정 하려면 응용 프로그램 호출 **SQLSetCursorName** 커서가 열리기 전에 합니다. 드라이버에 의해 생성 된 커서 이름을 사용 하려면 응용 프로그램 호출 **SQLGetCursorName** 커서가 열린 후 합니다.  
  
 커서 뒤 라이브러리는 현재 위치 업데이트를 실행 하거나 delete 문, 상태 배열, 행 집합 버퍼 및 커서 라이브러리에 의해 유지 관리 하는 캐시는 다음 표에 나와 있는 값을 포함 합니다.  
  
|문 사용|행 상태 배열 값|값<br /><br /> 버퍼 행 집합|값<br /><br /> 캐시 버퍼|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|위치 지정 업데이트|SQL_ROW_UPDATED|새 값 [1]|새 값 [1]|  
|위치 지정된 delete|SQL_ROW_DELETED|이전 값|이전 값|  
  
 [1] 응용 프로그램 위치 지정된 update 문의 실행 하기 전에 행 집합 버퍼에서 값을 업데이트 해야 합니다. 위치 지정된 update 문을 실행 한 후 커서 라이브러리 행 집합 버퍼의 값을 해당 캐시에 복사 합니다.
