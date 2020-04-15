---
title: SQLDriverConnect (엑셀 드라이버) | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1108206bf38183887540b114fda5a1e913aa67d9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307124"
---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect(Excel 드라이버)
> [!NOTE]  
>  이 항목에서는 Excel 드라이버 관련 정보를 제공합니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 **SQLDriverConnect를** 사용하면 DSN(데이터 원본)을 만들지 않고도 드라이버에 연결할 수 있습니다.  
  
 **DSN,** **DBQ**및 **FIL**: 다음 키워드는 모든 드라이버에 대한 연결 문자열에서 지원됩니다.  
  
 다음 표에서는 각 드라이버에 연결하는 데 필요한 최소 키워드를 보여 주며 **SQLDriverConnect**에 사용되는 키워드/값 쌍의 예를 제공합니다. DRIVERID 값의 전체 목록은 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)를 참조하십시오.  
  
> [!NOTE]  
>  Microsoft Excel 3.0 또는 4.0 드라이버에 대해 DBQ 또는 DefaultDir을 지정하지 않으면 드라이버가 현재 디렉터리에 연결됩니다.  
  
|드라이버|필요한 키워드|예|  
|------------|-----------------------|--------------|  
|마이크로 소프트 엑셀 3.0 또는 4.0|드라이버, 드라이버 ID|드라이버={마이크로소프트 엑셀 드라이버(*.xls)}; DBQ=c:\temp; 드라이버 ID=278|  
|마이크로 소프트 엑셀 5.0 / 7.0|드라이버, 드라이버 ID, DBQ|드라이버={마이크로소프트 엑셀 드라이버(*.xls)}; DBQ=c:\temp\sample.xls; 드라이버 ID=22|  
|마이크로 소프트 엑셀 97 이상|드라이버, 드라이버 ID, DBQ|드라이버={마이크로소프트 엑셀 드라이버(*.xls)}; DBQ=c:\temp\sample.xls; 드라이버 ID=790|
