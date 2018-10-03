---
title: SQLFreeConnect 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLFreeConnect
- SQLFreeConnect function [ODBC], mapping
ms.assetid: 8a844538-93c0-4709-bab6-35c45e771d80
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ef90025a129bc624377bfe7891f122a838180a51
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47695661"
---
# <a name="sqlfreeconnect-mapping"></a>SQLFreeConnect 매핑
응용 프로그램을 호출할 때 **SQLFreeConnect** 는 ODBC 3 *.x* 드라이버에 대 한 호출  
  
```  
SQLFreeConnect(hdbc)   
```  
  
 매핑되는  
  
```  
SQLFreeHandle(SQL_HANDLE_DBC,Handle)  
```  
  
 사용 하 여 합니다 *처리할* 인수는 값으로 설정 *hdbc*합니다.
