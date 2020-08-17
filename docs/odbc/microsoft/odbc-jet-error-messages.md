---
description: ODBC Jet 오류 메시지
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19f7d4b00c9e6b206ecd563083c0fcf16ced55e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340719"
---
# <a name="odbc-jet-error-messages"></a>ODBC Jet 오류 메시지
데이터 원본에서 발생 하는 오류의 경우 odbc 드라이버는 ODBC 파일 라이브러리에 의해 반환 된 오류 메시지를 반환 합니다. ODBC 드라이버 또는 드라이버 관리자에서 발생 하는 오류의 경우 드라이버는 SQLSTATE와 연결 된 텍스트를 기반으로 오류 메시지를 반환 합니다.  
  
 오류 메시지의 형식은 다음과 같습니다.  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 대괄호 ([]) 안의 접두사는 오류의 위치를 식별 합니다. 드라이버 관리자에서 오류가 발생 하면 *데이터 원본이* 제공 되지 않습니다. 데이터 원본에서 오류가 발생 하는 경우 [*vendor*] 및 [*ODBC-component*] 접두사는 데이터 원본에서 오류를 수신 하는 ODBC 구성 요소의 공급 업체 및 이름을 식별 합니다.  
  
 다음 표에서는 드라이버 관리자와 드라이버 ISAM에서 반환 하는 오류 메시지를 보여 줍니다.  
  
|오류 메시지|오류 위치|  
|-------------------|--------------------|  
|Microsoft [ODBC 드라이버 관리자] *메시지 텍스트*|드라이버 관리자 (Odbc32.dll)|  
|Microsoft [ODBC *드라이버-이름*] *메시지 텍스트*|드라이버 ISAM (드라이버 ISAMs 참조)|
