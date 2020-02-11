---
title: 위치 지정 업데이트 및 Delete 문 실행 | Microsoft Docs
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
ms.openlocfilehash: 2c69f784c2ce7c29cb49c81bf23f34a9cad12089
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67913626"
---
# <a name="executing-positioned-update-and-delete-statements"></a>위치 지정 업데이트 및 삭제 문 실행
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 응용 프로그램에서 **Sqlfetchscroll**을 사용 하 여 데이터 블록을 가져온 후에는 블록의 데이터를 업데이트 하거나 삭제할 수 있습니다. 위치 지정 업데이트 또는 삭제를 실행 하려면 응용 프로그램은 다음과 같습니다.  
  
1.  **SQLSetPos** 를 호출 하 여 업데이트 하거나 삭제할 행에 커서를 놓습니다.  
  
2.  다음 구문을 사용 하 여 위치 지정 update 또는 delete 문을 생성 합니다.  
  
     **** *테이블 이름* 업데이트  
  
     **** *열 식별자* **=** {*expression* &#124; **NULL**} 설정  
  
     [**,** *열 식별자* **=** {*expression* &#124; **NULL**}]  
  
     **현재** *커서 이름*  
  
     테이블 **에서 삭제** *-이름* **현재** *커서 이름* 입니다.  
  
     위치 지정 update 문에서 **SET** 절을 생성 하는 가장 쉬운 방법은 업데이트 되는 각 열에 대해 매개 변수 표식을 사용 하 고 **SQLBindParameter** 를 사용 하 여 이러한 열을 업데이트할 행의 행 집합 버퍼에 바인딩하는 것입니다. 이 경우 매개 변수의 C 데이터 형식은 행 집합 버퍼의 C 데이터 형식과 동일 하 게 됩니다.  
  
3.  현재 행에 대해 위치 지정 update 문을 실행 하는 경우 해당 행 집합 버퍼를 업데이트 합니다. 위치 지정 update 문을 성공적으로 실행 한 후 커서 라이브러리는 현재 행의 각 열에 있는 값을 캐시에 복사 합니다.  
  
    > [!CAUTION]  
    >  위치 지정 update 문을 실행 하기 전에 응용 프로그램에서 행 집합 버퍼를 올바르게 업데이트 하지 않으면 문이 실행 된 후 캐시의 데이터가 잘못 됩니다.  
  
4.  커서와 연결 된 문과 다른 문을 사용 하 여 위치 지정 update 또는 delete 문을 실행 합니다.  
  
    > [!CAUTION]  
    >  현재 행을 식별 하기 위해 커서 라이브러리로 생성 된 **where** 절은 행을 식별 하거나 다른 행을 식별 하거나 둘 이상의 행을 식별 하는 데 실패할 수 있습니다. 자세한 내용은 [검색 문 생성](../../../odbc/reference/appendixes/constructing-searched-statements.md)을 참조 하세요.  
  
 모든 위치 지정 update 및 delete 문에는 커서 이름이 필요 합니다. 커서 이름을 지정 하기 위해 응용 프로그램은 커서가 열리기 전에 **SQLSetCursorName** 를 호출 합니다. 드라이버가 생성 한 커서 이름을 사용 하기 위해 응용 프로그램은 커서가 열린 후 **SQLGetCursorName** 를 호출 합니다.  
  
 커서 라이브러리가 위치 지정 update 또는 delete 문을 실행 한 후에는 커서 라이브러리에 의해 유지 관리 되는 상태 배열, 행 집합 버퍼 및 캐시에 다음 표에 표시 된 값이 포함 됩니다.  
  
|문 사용 됨|행 상태 배열 값|값<br /><br /> 행 집합 버퍼|값<br /><br /> 캐시 버퍼|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|위치 지정 업데이트|SQL_ROW_UPDATED|새 값 [1]|새 값 [1]|  
|배치 되는 삭제|SQL_ROW_DELETED|이전 값|이전 값|  
  
 [1] 응용 프로그램은 위치 지정 update 문을 실행 하기 전에 행 집합 버퍼의 값을 업데이트 해야 합니다. 위치 지정 update 문을 실행 한 후 커서 라이브러리는 행 집합 버퍼의 값을 캐시에 복사 합니다.
