---
title: 데이터 길이, 버퍼 길이 및 잘림 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- data length [ODBC]
- truncating data [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 2825c6e7-b9ff-42fe-84fc-7fb39728ac5d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8586157237db1158587e3c39f1320b78d8251fb5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081475"
---
# <a name="data-length-buffer-length-and-truncation"></a>데이터 길이, 버퍼 길이 및 잘라내기
데이터 *길이* 는 데이터 원본에 저장 되는 것이 아니라 응용 프로그램의 데이터 버퍼에 저장 되는 데이터의 바이트 길이입니다. 데이터는 데이터 원본에 있는 데이터 버퍼의 다른 형식에 저장 되는 경우가 많으므로 이러한 구분은 중요 합니다. 따라서 데이터 원본으로 데이터를 전송 하려면 데이터 원본의 형식으로 변환 하기 전의 데이터 바이트 길이입니다. 데이터 원본에서 검색 되는 데이터의 경우 데이터 버퍼의 형식으로 변환한 후 잘림이 수행 되기 전에 데이터의 바이트 길이입니다.  
  
 정수 또는 날짜 구조와 같은 고정 길이 데이터의 경우 데이터의 바이트 길이는 항상 데이터 형식의 크기입니다. 일반적으로 응용 프로그램은 데이터 형식의 크기인 데이터 버퍼를 할당 합니다. 응용 프로그램에서 더 작은 버퍼를 할당 하는 경우 드라이버는 데이터 버퍼를 데이터 형식의 크기로 가정 하 고 더 작은 버퍼에 맞게 데이터를 자르지 않기 때문에 결과가 정의 되지 않습니다. 응용 프로그램이 더 큰 버퍼를 할당 하는 경우 추가 공간은 사용 되지 않습니다.  
  
 문자 또는 이진 데이터와 같은 가변 길이 데이터의 경우에는 데이터의 바이트 길이가 버퍼의 바이트 길이와는 다른 것을 인식 하는 것이 중요 합니다. 이러한 두 길이의 관계는 [버퍼](../../../odbc/reference/develop-app/buffers.md) 섹션에 설명 되어 있습니다. 데이터의 바이트 길이가 버퍼의 바이트 길이 보다 크면 드라이버가 인출 된 데이터를 버퍼의 바이트 길이로 자르고 SQLSTATE 01004 (데이터 잘림)를 사용 하 여 SQL_SUCCESS_WITH_INFO을 반환 합니다. 그러나 반환 된 바이트 길이는 잘린 데이터의 길이입니다.  
  
 예를 들어 응용 프로그램이 이진 데이터 버퍼에 대해 50 바이트를 할당 한다고 가정 합니다. 드라이버가 반환할 이진 데이터의 10 바이트를 포함 하는 경우 버퍼에 10 바이트를 반환 합니다. 데이터의 바이트 길이는 10이 고 버퍼의 바이트 길이는 50입니다. 드라이버가 반환할 60 바이트의 이진 데이터를 포함 하는 경우 데이터를 50 바이트로 자르고, 버퍼에서 해당 바이트를 반환 하 고 SQL_SUCCESS_WITH_INFO 반환 합니다. 데이터의 바이트 길이는 60 (잘림 전의 길이)이 고 버퍼의 바이트 길이는 여전히 50입니다.  
  
 잘린 각 열에 대해 진단 레코드가 만들어집니다. 드라이버가 이러한 레코드를 만들고 응용 프로그램에서 처리 하는 데 시간이 걸리기 때문에 잘림로 인해 성능이 저하 될 수 있습니다. 일반적으로 응용 프로그램은 긴 버퍼를 할당 하 여이 문제를 방지할 수 있지만 긴 데이터로 작업 하는 경우에는 불가능 합니다. 데이터 잘림이 발생할 경우 응용 프로그램은 경우에 따라 더 큰 버퍼를 할당 하 고 데이터를 다시 페치 수 있습니다. 이는 모든 경우에는 적용 되지 않습니다. **Sqlgetdata**를 호출 하 여 데이터를 가져오는 동안 잘림이 발생 하는 경우 응용 프로그램은 이미 반환 된 데이터에 대해 **SQLGetData** 를 호출 하지 않아도 됩니다. 자세한 내용은 [Long 데이터 가져오기](../../../odbc/reference/develop-app/getting-long-data.md)를 참조 하세요.
