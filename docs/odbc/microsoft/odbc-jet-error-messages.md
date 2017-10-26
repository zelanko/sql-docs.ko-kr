---
title: "ODBC Jet 오류 메시지 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- error messages (ODBC driver for oracle)
ms.assetid: f8d2a8f2-0316-42c4-bc34-5367661634ae
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0fad2aab1020cb7a56c00a2b78c1d2c46a41c422
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-jet-error-messages"></a>ODBC Jet 오류 메시지
데이터 소스에서 발생 하는 오류에 대 한 ODBC 드라이버는 ODBC 파일 라이브러리에서를 반환 하는 오류 메시지를 반환 합니다. ODBC 드라이버 또는 드라이버 관리자에서 발생 하는 오류에 대 한 오류 메시지 텍스트에 따라 드라이버 반환 SQLSTATE 연관 됩니다.  
  
 오류 메시지는 다음과 같은 형식에 포함:  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 대괄호 ()는 접두사는 오류가 발생 한 위치를 식별합니다. 오류가 발생 하는 드라이버 관리자에서 *데이터 소스* 제공 되지 않습니다. 데이터 원본에서 오류가 발생 하는 경우는 [*공급 업체*] 및 [*ODBC 구성 요소*] 공급 업체 및 데이터 원본에서 오류를 받았는지를 ODBC 구성 요소 이름 접두사를 식별 합니다.  
  
 다음 표에서 드라이버 관리자와 ISAM 드라이버에서 반환 된 오류 메시지를 보여 줍니다.  
  
|오류 메시지입니다.|오류 위치|  
|-------------------|--------------------|  
|[Microsoft] [ODBC 드라이버 관리자] *메시지 텍스트*|드라이버 관리자 (Odbc32.dll)|  
|[Microsoft] [ODBC *드라이버 이름*]*메시지 텍스트*|ISAM 드라이버 (드라이버 Isam 참조)|

