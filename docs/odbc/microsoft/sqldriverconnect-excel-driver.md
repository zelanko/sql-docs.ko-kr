---
title: SQLDriverConnect (Excel 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Excel Driver
ms.assetid: 285cb1ea-f461-4596-97f2-fc57af05dede
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e38f2f513b7da2c9342470ba75e2ee11b3d7e52a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053898"
---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect(Excel 드라이버)
> [!NOTE]  
>  이 항목에서는 Excel 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 **SQLDriverConnect** 를 사용 하면 DSN (데이터 원본)을 만들지 않고도 드라이버에 연결할 수 있습니다.  
  
 모든 드라이버에 대 한 연결 문자열에서 지원 되는 키워드는 **DSN**, **Dbq**및 **FIL**입니다.  
  
 다음 표에서는 각 드라이버에 연결 하는 데 필요한 최소 키워드를 보여 주며, **SQLDriverConnect**에 사용 되는 키워드/값 쌍의 예를 제공 합니다. DRIVERID 값의 전체 목록은 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)를 참조 하세요.  
  
> [!NOTE]  
>  Microsoft Excel 3.0 또는 4.0 드라이버에 대해 DBQ 또는 DefaultDir를 지정 하지 않으면 드라이버가 현재 디렉터리에 연결 됩니다.  
  
|드라이버|필요한 키워드|예|  
|------------|-----------------------|--------------|  
|Microsoft Excel 3.0 또는 4.0|드라이버, DriverID|Driver = {Microsoft Excel Driver (* .xls)}; DBQ = c:\temp; DriverID = 278|  
|Microsoft Excel 5.0/7.0|드라이버, DriverID, DBQ|Driver = {Microsoft Excel Driver (* .xls)}; DBQ = c:\temp\sample.xls; DriverID = 22|  
|Microsoft Excel 97 이상|드라이버, DriverID, DBQ|Driver = {Microsoft Excel Driver (* .xls)}; DBQ = c:\temp\sample.xls; DriverID = 790|
