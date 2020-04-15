---
title: 바이너리 형태로 데이터 전송 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], transferring in binary form
- transferring data in binary form [ODBC]
- binary data transfers [ODBC]
ms.assetid: 4b12a9de-51d0-416a-87f4-9bf84959cad9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 53531ff4a3b2e1441fabf22ec7a3ce12b15540eb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301415"
---
# <a name="transferring-data-in-its-binary-form"></a>이진 형식으로 데이터 전송
응용 프로그램은 동일한 DBMS 및 하드웨어 플랫폼을 사용하는 두 데이터 원본 간에 지정된 DBMS에서 사용하는 내부 양식으로 데이터를 안전하게 전송할 수 있습니다. 지정된 데이터의 경우 SQL 데이터 형식은 원본 및 대상 데이터 원본에서 동일해야 합니다. C 데이터 형식이 SQL_C_BINARY.  
  
 응용 프로그램이 **SQLFetch,** **SQLFetchScroll**또는 **SQLGetData를** 호출하여 원본 데이터 원본에서 데이터를 검색하면 드라이버는 데이터 원본에서 데이터를 검색하고 변환하지 않고 형식 SQL_C_BINARY 저장소 위치로 전송합니다. 응용 프로그램이 **SQLBulkOperations,** **SQLExEcDirect**, **SQLPutData 또는 SQLSetPos를** 호출하여 데이터를 대상 데이터 원본으로 보내면 드라이버는 저장소 위치에서 데이터를 검색하여 변환하지 않고 대상 데이터 원본으로 전송합니다. **SQLExecute**  
  
> [!NOTE]  
>  이러한 방식으로 데이터를 전송하는 응용 프로그램(이진 데이터 제외)은 DBMS 간에 상호 운용되지 않습니다.  
  
 **SQLCopyDesc는** 원본 DBMS에서 대상 DBMS의 매개 변수 바인딩에 행 바인딩을 복사하는 데 사용할 수 있습니다.
