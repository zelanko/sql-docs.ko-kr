---
title: "데이터 길이, 버퍼 길이 및 잘림 | Microsoft Docs"
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
- data buffers [ODBC], length
- data length [ODBC]
- truncating data [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 2825c6e7-b9ff-42fe-84fc-7fb39728ac5d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 616dc403fdd23f3233bde4a5db19dd58b6d94cf1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="data-length-buffer-length-and-truncation"></a>데이터 길이, 버퍼 길이 및 잘림
*데이터 길이* 작업은 데이터의 바이트 길이 응용 프로그램의 데이터 버퍼에 저장 될 것으로 그다지 데이터 원본에 저장 됩니다. 데이터 원본에 보다 데이터 버퍼에 서로 다른 형식에는 데이터는 대개 저장 되므로 이러한 구분은 중요 합니다. 따라서 데이터 원본에 전송 되는 데이터, 데이터 원본 형식으로 변환 하기 전에 데이터의 바이트 길이 이것이입니다. 데이터 원본에서 검색 중인 데이터, 데이터 버퍼 종류와 잘림을 모두 수행 되기 전의 변환 후 데이터의 바이트 길이입니다.  
  
 정수 또는 날짜 구조와 같은 고정 길이 데이터에 대 한 데이터의 바이트 길이 항상 데이터 형식의 크기입니다. 일반적으로 응용 프로그램 데이터 형식의 크기는 데이터 버퍼를 할당 합니다. 응용 프로그램에서 더 작은 버퍼를 할당 하는 경우에 데이터 버퍼는 데이터 형식의 크기 및 더 작은 버퍼에 맞게 데이터를 자르지 않는 드라이버 가정 하기 때문에 그 결과가 정의 되지 않습니다. 응용 프로그램에서 더 큰 버퍼를 할당 하는 경우에 추가 공간이 사용 되지 않습니다.  
  
 문자 또는 이진 데이터와 같은 가변 길이 데이터는 데이터의 바이트 길이와 별도로 및 버퍼의 바이트 길이 보다 종종 다른 임을 인식 하는 것이 중요 합니다. 이러한 두 길이의 관계에 설명 된 [버퍼](../../../odbc/reference/develop-app/buffers.md) 섹션. 데이터의 바이트 길이 버퍼의 바이트 길이 보다 큰 경우 드라이버는 인출 된 데이터 버퍼의 바이트 길이를 자릅니다 하 고 (데이터 잘림) sqlstate 01004 SQL_SUCCESS_WITH_INFO를 반환 합니다. 그러나 반환 된 바이트 길이 잘리지 않은 데이터의 길이입니다.  
  
 예를 들어 응용 프로그램이 이진 데이터 버퍼에 대 한 50 바이트를 할당 합니다. 드라이버의 이진 데이터의 10 바이트, 버퍼에 해당 10 바이트를 반환 합니다. 데이터의 바이트 길이 10, 및 버퍼의 바이트 길이 50입니다. 드라이버의 이진 데이터의 60 바이트, 50 바이트에 데이터를 자릅니다, 그리고 버퍼에 해당 바이트를 반환 하 고 SQL_SUCCESS_WITH_INFO를 반환 합니다. 데이터의 바이트 길이 60 (잘림 전에 길이) 하 고 버퍼의 바이트 길이 여전히 50입니다.  
  
 잘렸습니다. 각 열에 대 한 진단 레코드가 생성 됩니다. 이러한 레코드를 만들려면 드라이버에 대 한 및 처리 하도록 응용 프로그램에 대 한 시간을 사용 하기 때문에 잘림이 성능이 저하 될 수 있습니다. 일반적으로 응용 프로그램이 수는 없습니다 한 long 데이터를 작업할 때 있지만 충분히 큰 버퍼를 할당 하 여이 문제를 방지할 수 있습니다. 응용 프로그램 경우가 더 큰 버퍼를 할당할 수 있습니다 및에서 데이터를 반드시 다시 반입 데이터 잘림이 발생할 경우 모든 경우에 아닙니다. 에 대 한 호출을 사용 하 여 데이터를 가져오는 동안 잘림이 발생 하는 경우 **SQLGetData**, 응용 프로그램을 호출 하지 않아도 **SQLGetData** 반환 되었습니다. 이미 데이터에 대 한;에 대 한 자세한 내용은 참조 [가져오기 Long 데이터](../../../odbc/reference/develop-app/getting-long-data.md)합니다.
