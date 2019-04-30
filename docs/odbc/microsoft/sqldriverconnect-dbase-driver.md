---
title: SQLDriverConnect (dBASE 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], dBASE Driver
ms.assetid: c837aa31-068e-4fa3-bc00-aae09bec21de
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e4eeaa7ba710814bfeb8c5b4f5aa0dbd2d30ef7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63060956"
---
# <a name="sqldriverconnect-dbase-driver"></a>SQLDriverConnect(dBASE 드라이버)
> [!NOTE]  
>  이 항목에서는 dBASE 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 **SQLDriverConnect** 데이터 소스 (DSN)를 만들지 않고 드라이버에 연결할 수 있습니다.  
  
 다음 키워드는 모든 드라이버에 대 한 연결 문자열에 지원 됩니다. **DSN**하십시오 **DBQ**, 및 **FIL**합니다.  
  
 Paradox 드라이버를 사용 하면 사용자가 암호로 보호 된 파일을 연 후, 다른 사용자에 게 동일한 파일을 열에 허용 되지 않습니다.  
  
 다음 표에서 각 드라이버에 연결 하는 데 필요한 최소 키워드를 보여 줍니다 하 고 사용 하는 키워드/값 쌍의 예가 **SQLDriverConnect**합니다. DRIVERID 값의 전체 목록을 참조 하세요 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)합니다.  
  
> [!NOTE]  
>  DBQ 또는 DefaultDir는 dBASEdriver에 대 한 지정 하지 않으면 드라이버는 현재 디렉터리에 연결 됩니다.  
  
|드라이버|필요한 키워드|예|  
|------------|-----------------------|--------------|  
|dBASE|Driver, DriverID|Driver={Microsoft dBASE Driver (*.dbf)}; DBQ=c:\temp; DriverID=277|
