---
title: ODBC Jet 오류 메시지 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages (ODBC driver for oracle)
ms.assetid: f8d2a8f2-0316-42c4-bc34-5367661634ae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85e0f9a8bc7015a0ad5b12ce46a6c94ab31ca43c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915811"
---
# <a name="odbc-jet-error-messages"></a>ODBC Jet 오류 메시지
데이터 원본에서 발생 하는 오류에 대 한 ODBC 드라이버에 ODBC 파일 라이브러리에 의해 반환 된 오류 메시지를 반환 합니다. ODBC 드라이버 또는 드라이버 관리자에서 발생 하는 오류에 대 한 오류 메시지 텍스트에 따라 드라이버는 SQLSTATE를 사용 하 여 연결 합니다.  
  
 오류 메시지의 형식이:  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 오류의 위치를 식별 하는 접두사에 대괄호 (). 드라이버 관리자에서 오류가 발생 하 *데이터 원본* 제공 되지 않습니다. 데이터 원본에서 오류가 발생 하는 경우는 [*공급 업체*] 및 [*ODBC 구성 요소*] 접두사의 공급 업체와 데이터 원본에서 오류를 수신 하는 ODBC 구성 요소 이름을 식별 합니다.  
  
 다음 표에서 드라이버 ISAM 드라이버 관리자에서 반환 된 오류 메시지를 보여 줍니다.  
  
|오류 메시지|오류 위치|  
|-------------------|--------------------|  
|[Microsoft] [ODBC 드라이버 관리자] *메시지 텍스트*|드라이버 관리자 (Odbc32.dll)|  
|[Microsoft] [ODBC *드라이버 이름*]*메시지 텍스트*|ISAM 드라이버 (드라이버 Isam 참조)|
