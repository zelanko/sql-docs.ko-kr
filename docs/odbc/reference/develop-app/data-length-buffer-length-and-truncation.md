---
title: 데이터 길이, 버퍼 길이 및 잘림 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2e7b8d1e60cd83594509c2ab5cbc24e04546eca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305235"
---
# <a name="data-length-buffer-length-and-truncation"></a>데이터 길이, 버퍼 길이 및 잘라내기
*데이터 길이는* 데이터 원본에 저장되는 것이 아니라 응용 프로그램의 데이터 버퍼에 저장되는 데이터의 바이트 길이입니다. 이러한 구분은 데이터가 데이터 원본과 데이터 버퍼의 다른 형식에 저장되는 경우가 많기 때문에 중요합니다. 따라서 데이터 원본으로 전송되는 데이터의 경우 데이터 원본의 유형으로 변환하기 전에 데이터의 바이트 길이입니다. 데이터 원본에서 검색되는 데이터의 경우 데이터 버퍼의 유형으로 변환한 후 잘림이 완료되기 전에 데이터의 바이트 길이입니다.  
  
 정수 또는 날짜 구조와 같은 고정 길이 데이터의 경우 데이터의 바이트 길이는 항상 데이터 형식의 크기입니다. 일반적으로 응용 프로그램은 데이터 형식의 크기인 데이터 버퍼를 할당합니다. 응용 프로그램이 더 작은 버퍼를 할당하는 경우 드라이버는 데이터 버퍼가 데이터 형식의 크기라고 가정하고 더 작은 버퍼에 맞게 데이터를 잘리지 않으므로 결과가 정의되지 않습니다. 응용 프로그램에서 더 큰 버퍼를 할당하는 경우 추가 공간은 사용되지 않습니다.  
  
 문자 또는 이진 데이터와 같은 가변 길이 데이터의 경우 데이터의 바이트 길이가 버퍼의 바이트 길이와 분리되어 있고 종종 다른 경우가 많다는 것을 인식하는 것이 중요합니다. 이러한 두 길이의 관계는 버퍼 섹션에 설명되어 [있습니다.](../../../odbc/reference/develop-app/buffers.md) 데이터의 바이트 길이가 버퍼의 바이트 길이보다 큰 경우 드라이버는 가져온 데이터를 버퍼의 바이트 길이로 잘리고 SQLSTATE 01004(데이터가 잘린 데이터)를 사용하여 SQL_SUCCESS_WITH_INFO 반환합니다. 그러나 반환된 바이트 길이는 잘린 되지 않은 데이터의 길이입니다.  
  
 예를 들어 응용 프로그램이 이진 데이터 버퍼에 50바이트를 할당한다고 가정합니다. 드라이버에 반환할 이진 데이터가 10바이트 인 경우 버퍼에서 10바이트를 반환합니다. 데이터의 바이트 길이는 10이고 버퍼의 바이트 길이는 50입니다. 드라이버에 반환할 60바이트의 이진 데이터가 있는 경우 데이터를 50바이트로 트렁킨 다음 버퍼에서 해당 바이트를 반환하고 SQL_SUCCESS_WITH_INFO 반환합니다. 데이터의 바이트 길이는 60(잘림하기 전의 길이)이며 버퍼의 바이트 길이는 여전히 50입니다.  
  
 잘린 각 열에 대해 진단 레코드가 만들어집니다. 드라이버가 이러한 레코드를 만들고 응용 프로그램이 레코드를 처리하는 데 시간이 걸리기 때문에 잘림하면 성능이 저하될 수 있습니다. 일반적으로 응용 프로그램은 긴 데이터로 작업할 때 불가능할 수 있지만 충분한 버퍼를 할당하여 이 문제를 방지할 수 있습니다. 데이터 잘림이 발생하면 응용 프로그램에서 더 큰 버퍼를 할당하고 데이터를 다시 가져올 수 있습니다. 모든 경우에 사실이 아닙니다. **SQLGetData를**호출하는 동안 잘림이 발생하는 경우 응용 프로그램은 이미 반환된 데이터에 대해 **SQLGetData를** 호출할 필요가 없습니다. 자세한 내용은 [긴 데이터 얻기](../../../odbc/reference/develop-app/getting-long-data.md)를 참조하십시오.
