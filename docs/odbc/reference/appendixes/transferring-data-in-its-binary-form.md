---
title: 이진에서 데이터를 전송 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], transferring in binary form
- transferring data in binary form [ODBC]
- binary data transfers [ODBC]
ms.assetid: 4b12a9de-51d0-416a-87f4-9bf84959cad9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d2d1227af9eeb303bc0d9bc56733e6bda9b5325c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="transferring-data-in-its-binary-form"></a>Binary에서 데이터 전송
안전 하 게 응용 프로그램 같은 DBMS와 하드웨어 플랫폼을 사용 하는 두 개의 데이터 원본 간에 데이터 (지정 된 DBMS에 의해 사용 되는 내부 형식)를 전송할 수 있습니다. 지정된 된 데이터 부분에 대 한 원본 및 대상 데이터 원본에서 동일한 SQL 데이터 형식 이어야 합니다. C 데이터 형식은 SQL_C_BINARY 합니다.  
  
 응용 프로그램 호출 하는 경우 **SQLFetch**, **SQLFetchScroll**, 또는 **SQLGetData** 원본 데이터 원본에서 데이터를 검색 하는 드라이버는 데이터에서 데이터를 검색 원본 및 SQL_C_BINARY 형식의 저장소 위치를 변환 하지 않고 전송 합니다. 응용 프로그램 호출 하는 경우 **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPutData, 또는 SQLSetPos** 데이터를 전송할 수 대상 데이터 원본 드라이버는 저장 위치에서 데이터를 검색 하 고 대상 데이터 원본에 변환 하지 않고,를 이동 합니다.  
  
> [!NOTE]  
>  이런이 방식으로 모든 데이터 (이진 데이터 제외)를 전송 하는 응용 프로그램 Dbms 간에 상호 운용 되지는 않습니다.  
  
 **SQLCopyDesc** 원본 DBMS에서에서 대상 DBMS에서에서 매개 변수 바인딩의 행 바인딩을 복사할 데 사용할 수 있습니다.
