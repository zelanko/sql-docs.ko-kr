---
title: SQLDriverConnect (Paradox 드라이버) | Microsoft Docs
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
- SQLDriverConnect function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLDriverConnect
ms.assetid: c2ba486e-5e01-4e67-adb1-68511f5f0206
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6f34d1cd8d17c077a4879cf8dd39331533e3b0c5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqldriverconnect-paradox-driver"></a>SQLDriverConnect (Paradox 드라이버)
> [!NOTE]  
>  이 항목에서는 Paradox 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 **SQLDriverConnect** 데이터 소스 (DSN)을 만들지 않고 드라이버에 연결할 수 있습니다.  
  
 다음 키워드는 모든 드라이버에 대 한 연결 문자열에 지원: **DSN**, **DBQ**, 및 **FIL**합니다.  
  
 **PWD** 키워드도 지원 됩니다. PWD 키워드 특수 문자가 포함 되지 않습니다 (에서 SQL_SPECIAL_CHARACTERS 참조 **SQLGetInfo** 반환 된 값).  
  
 암호로 보호 된 파일을 연 후에 사용자가을 다른 사용자에 게 동일한 파일을 열도록 허용 되지 않습니다.  
  
 다음 표에서 각 드라이버에 연결 하는 데 필요한 최소 키워드를 보여 줍니다와 함께 사용 하는 키워드/값 쌍의 예가 나와 **SQLDriverConnect**합니다. DRIVERID 값의 전체 목록을 참조 하십시오. [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.  
  
> [!NOTE]  
>  DBQ 또는 DefaultDir Paradox 드라이버에 대 한 지정 하지 않으면 드라이버는 현재 디렉터리에 연결 됩니다.  
  
|드라이버|필요한 키워드|예제|  
|------------|-----------------------|-------------|  
|Paradox|드라이버를 DriverID|Driver={Microsoft Paradox Driver (*.db )}; DBQ=c:\temp;DriverID=26|
