---
title: 이진 형식으로 데이터 전송 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44bf8de8ea4c33a20a6159c5702db0b7eaee9eed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735049"
---
# <a name="transferring-data-in-its-binary-form"></a>이진 형식으로 데이터 전송
안전 하 게 응용 프로그램 같은 DBMS 및 하드웨어 플랫폼을 사용 하는 두 개의 데이터 원본 간에 데이터 (지정 된 DBMS에서 사용 하는 내부 형식)를 전송할 수 있습니다. 특정 데이터에 대 한 원본 및 대상 데이터 원본에 동일한 SQL 데이터 형식 이어야 합니다. C 데이터 형식은 SQL_C_BINARY입니다.  
  
 응용 프로그램을 호출할 때 **SQLFetch**를 **SQLFetchScroll**, 또는 **SQLGetData** 드라이버 데이터에서 데이터를 검색 데이터 소스에서 데이터를 검색 하려면 원본 및 SQL_C_BINARY 형식의 저장소 위치로 변환 하지 않고 전송 합니다. 응용 프로그램을 호출할 때 **SQLBulkOperations**, **SQLExecute**를 **SQLExecDirect**를 **SQLPutData, 또는 SQLSetPos** 데이터를 전송할 수 대상 데이터 원본 드라이버 저장소 위치에서 데이터를 검색 하 고, 변환, 대상 데이터 원본 없이 전송 합니다.  
  
> [!NOTE]  
>  이 방식으로 (이진 데이터)를 제외한 모든 데이터를 전송 하는 응용 프로그램 Dbms 간에 상호 운용 되지는 않습니다.  
  
 **SQLCopyDesc** 복사할 행 바인딩 원본 DBMS에서에서 대상 DBMS에서에서 매개 변수 바인딩을 사용할 수 있습니다.
