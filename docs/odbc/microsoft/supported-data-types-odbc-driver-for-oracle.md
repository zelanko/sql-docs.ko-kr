---
title: 지원 되는 데이터 형식 (Oracle 용 ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: 21d5f8d9-a3aa-4aa4-bc37-ff8bc90c0870
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 219a6d2e837280ca3220382bea56d2ab610ce87a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270891"
---
# <a name="supported-data-types-odbc-driver-for-oracle"></a>지원되는 데이터 형식(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 Oracle 용 ODBC 드라이버는 모든 Oracle 7.3 데이터 형식을 지원합니다 그러나 여기에 나열 된 새 열고 Oracle8 데이터 형식 지원 되지 않습니다.  
  
|데이터 형식|Oracle 7.3|열고 Oracle8|  
|---------------|----------------|-------------|  
|BFILE|n/a|지원되지 않음|  
|BLOB|n/a|지원되지 않음|  
|CHAR|지원됨|지원됨|  
|CLOB|n/a|지원되지 않음|  
|DATE|지원됨|지원됨|  
|FLOAT|지원됨|지원됨|  
|INTEGER|지원됨|지원됨|  
|LONG|지원됨|지원됨|  
|LONG RAW|지원됨|지원됨|  
|NCHAR|n/a|지원되지 않음|  
|NCLOB|n/a|지원되지 않음|  
|NUMBER|지원됨|지원됨|  
|NVARCHAR2|n/a|지원되지 않음|  
|RAW|지원됨|지원됨|  
|VARCHAR2|지원됨|지원됨|  
|MLSLABEL|지원되지 않습니다.|지원되지 않습니다.|  
  
> [!NOTE]  
>  VARCHAR 열 크기를 허용 하는 방법에 대 한 자세한 내용은 참조 [VARCHAR 열 크기](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) 이 가이드에서.
