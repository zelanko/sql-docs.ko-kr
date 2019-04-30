---
title: SQLDriverConnect (Paradox 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLDriverConnect
ms.assetid: c2ba486e-5e01-4e67-adb1-68511f5f0206
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bae4a842729c8d302731ebf5fec22abb817f4c75
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63238375"
---
# <a name="sqldriverconnect-paradox-driver"></a>SQLDriverConnect(Paradox 드라이버)
> [!NOTE]  
>  이 항목에서는 Paradox 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 **SQLDriverConnect** 데이터 소스 (DSN)를 만들지 않고 드라이버에 연결할 수 있습니다.  
  
 다음 키워드는 모든 드라이버에 대 한 연결 문자열에 지원 됩니다. **DSN**하십시오 **DBQ**, 및 **FIL**합니다.  
  
 합니다 **PWD** 키워드도 지원 됩니다. PWD 키워드는 특수 문자를 포함 하지 않아야 (SQL_SPECIAL_CHARACTERS의를 참조 하세요 **SQLGetInfo** 반환 값).  
  
 암호로 보호 된 파일을 연 후에 사용자를 다른 사용자에 게 동일한 파일을 열에 허용 되지 않습니다.  
  
 다음 표에서 각 드라이버에 연결 하는 데 필요한 최소 키워드를 보여 줍니다 하 고 사용 하는 키워드/값 쌍의 예가 **SQLDriverConnect**합니다. DRIVERID 값의 전체 목록을 참조 하세요 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.  
  
> [!NOTE]  
>  DBQ 또는 DefaultDir Paradox 드라이버에 대 한 지정 하지 않으면 드라이버는 현재 디렉터리에 연결 됩니다.  
  
|드라이버|필요한 키워드|예제|  
|------------|-----------------------|-------------|  
|Paradox|Driver, DriverID|Driver={Microsoft Paradox Driver (*.db )}; DBQ=c:\temp;DriverID=26|
