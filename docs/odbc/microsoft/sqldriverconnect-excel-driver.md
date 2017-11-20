---
title: "SQLDriverConnect (Excel 드라이버) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Excel driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Excel Driver
ms.assetid: 285cb1ea-f461-4596-97f2-fc57af05dede
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eca660cf2c38539dbf4a0fa560bfc67a1b1be115
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect (Excel 드라이버)
> [!NOTE]  
>  이 항목에서는 Excel 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 **SQLDriverConnect** 데이터 소스 (DSN)을 만들지 않고 드라이버에 연결할 수 있습니다.  
  
 다음 키워드는 모든 드라이버에 대 한 연결 문자열에 지원: **DSN**, **DBQ**, 및 **FIL**합니다.  
  
 다음 표에서 각 드라이버에 연결 하는 데 필요한 최소 키워드를 보여 줍니다와 함께 사용 하는 키워드/값 쌍의 예가 나와 **SQLDriverConnect**합니다. DRIVERID 값의 전체 목록을 참조 하십시오. [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)합니다.  
  
> [!NOTE]  
>  Microsoft Excel 3.0 또는 4.0 driver DBQ 또는 DefaultDir 지정 하지 않으면 드라이버는 현재 디렉터리에 연결 됩니다.  
  
|드라이버|필요한 키워드|예|  
|------------|-----------------------|--------------|  
|3.0 또는 4.0 Microsoft Excel|드라이버를 DriverID|Driver = {Microsoft Excel Driver (*.xls)을 (를); DBQ = c:\temp; DriverID 278 =|  
|Microsoft Excel 5.0/7.0|드라이버를 DriverID, DBQ|Driver = {Microsoft Excel Driver (*.xls)을 (를); DBQ=c:\temp\sample.xls; DriverID = 22|  
|Microsoft Excel 97 이상|드라이버를 DriverID, DBQ|Driver = {Microsoft Excel Driver (*.xls)을 (를); DBQ=c:\temp\sample.xls; DriverID 790 =|

