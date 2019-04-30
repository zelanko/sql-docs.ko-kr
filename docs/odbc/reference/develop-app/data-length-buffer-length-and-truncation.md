---
title: 데이터 길이, 버퍼 길이 및 잘라내기 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 1ed2e5ca1fdaba97dde64329c5e8e1b692f43158
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267752"
---
# <a name="data-length-buffer-length-and-truncation"></a>데이터 길이, 버퍼 길이 및 잘라내기
합니다 *데이터 길이* 이 데이터의 바이트 길이 응용 프로그램의 데이터 버퍼에 저장 됩니다 하는 대로 아닙니다. 데이터 원본에 저장 됩니다. 데이터는 흔히 데이터 원본에 보다 데이터 버퍼에서 다른 형식에 저장 되므로 이러한 구분은 중요 합니다. 따라서 데이터 원본에 전송 되는 데이터를 데이터 소스의 형식으로 변환 하기 전에 데이터의 바이트 길이 이것이입니다. 데이터 원본에서 검색 되는 데이터에 대 한 데이터 버퍼의 형식으로 또는 그 잘림을 모두 수행 하기 전에 변환 된 데이터의 바이트 길이입니다.  
  
 정수 또는 날짜 구조와 같은 고정 길이 데이터에 대 한 데이터의 바이트 길이가 항상 데이터 형식의 크기입니다. 일반적으로 응용 프로그램에는 데이터 형식의 크기는 데이터 버퍼를 할당 합니다. 응용 프로그램을 더 작은 버퍼를 할당 하면에 데이터 버퍼는 데이터 형식의 크기 이며 더 작은 버퍼에 맞게 데이터를 잘라내지 않습니다 드라이버 가정 하기 때문에 결과가 정의 되지 않습니다. 더 큰 버퍼를 할당 하는 응용 프로그램에 추가 공백이 사용 되지 않습니다.  
  
 문자 또는 이진 데이터와 같은 가변 길이 데이터에 대 한 별개 이며 종종 다른 버퍼의 바이트 길이 보다 데이터의 바이트 길이 인식 하는 것이 반드시 합니다. 이러한 두 길이의 관계에 설명 되어는 [버퍼](../../../odbc/reference/develop-app/buffers.md) 섹션입니다. 데이터의 바이트 길이 버퍼의 바이트 길이 보다 큰 경우 드라이버는 인출된 버퍼의 바이트 길이 데이터를 자릅니다 하 고 SQL_SUCCESS_WITH_INFO sqlstate 01004 (데이터 잘림)를 반환 합니다. 그러나 반환 된 바이트 길이가 잘리지 않은 데이터의 길이입니다.  
  
 예를 들어, 응용 프로그램 이진 데이터 버퍼에 대 한 50 바이트를 할당 합니다. 드라이버에 10 바이트의 이진 데이터를 반환 하는 경우 해당 10 바이트 버퍼에 반환 합니다. 데이터의 바이트 길이가 10 및 버퍼의 바이트 길이 50 개입니다. 드라이버의 60 바이트의 이진 데이터 반환, 50 바이트 데이터를 자릅니다, 그리고 버퍼에 해당 바이트를 반환 하 고 SQL_SUCCESS_WITH_INFO를 반환 합니다. 데이터의 바이트 길이 (자르기 전에 길이), 60이 고 버퍼의 바이트 길이 여전히 50입니다.  
  
 잘라 각 열에 대 한 진단 레코드가 생성 됩니다. 이러한 레코드를 만들려면 드라이버 및 처리 하도록 응용 프로그램 시간이 걸리기 때문에 잘림이 성능이 저하 될 수 있습니다. 일반적으로 응용 프로그램이 불가능할 수 있습니다 긴 데이터를 작업할 때 하지만 충분히 큰 버퍼를 할당 하 여이 문제를 방지할 수 있습니다. 응용 프로그램 경우에 따라 더 큰 버퍼를 할당할 수 있습니다 및 데이터를 다시 가져오도록 데이터 잘림이 발생할 경우 이 모든 경우에는 그렇지 않습니다. 호출 하 여 데이터를 가져오는 동안 잘림이 발생 하는 경우 **SQLGetData**, 응용 프로그램을 호출 하지 않아도 **SQLGetData** 이미 반환 된 데이터에 대 한; 자세한 내용은 참조 [시작 Long 데이터](../../../odbc/reference/develop-app/getting-long-data.md)입니다.
