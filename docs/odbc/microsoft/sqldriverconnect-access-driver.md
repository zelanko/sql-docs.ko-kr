---
title: SQLDriverConnect (Access 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Access Driver
ms.assetid: 9d133e9b-7545-464d-aa3c-677fa7e2a41d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9a71874c91e48c25072fbfed8f66a312d65b4697
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63048477"
---
# <a name="sqldriverconnect-access-driver"></a>SQLDriverConnect(Access 드라이버)
> [!NOTE]  
>  이 항목에서는 액세스 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 **SQLDriverConnect** 데이터 소스 (DSN)를 만들지 않고 드라이버에 연결할 수 있습니다.  
  
 다음 키워드는 모든 드라이버에 대 한 연결 문자열에 지원 됩니다. **DSN**하십시오 **DBQ**, 및 **FIL**합니다.  
  
 합니다 **UID** 하 고 **PWD** 키워드 에서도 지원 됩니다.  
  
 PWD 키워드는 특수 문자를 포함 하지 않아야 (SQL_SPECIAL_CHARACTERS의를 참조 하세요 **SQLGetInfo** 반환 값).  
  
 다음 표에서 각 드라이버에 연결 하는 데 필요한 최소 키워드를 보여 줍니다 하 고 사용 하는 키워드/값 쌍의 예가 **SQLDriverConnect**합니다. DRIVERID 값의 전체 목록을 참조 하세요 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)합니다.  
  
|드라이버|필요한 키워드|예|  
|------------|-----------------------|--------------|  
|Microsoft Access|Driver, DBQ|Driver={Microsoft Access Driver (*.mdb)}; DBQ=c:\\\temp\\\sample.mdb|
