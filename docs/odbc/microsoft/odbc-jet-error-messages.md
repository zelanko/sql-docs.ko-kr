---
title: ODBC 제트 오류 메시지 | 마이크로 소프트 문서
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
ms.openlocfilehash: e8fa6e672b69c7791e66dc3919e6fcd22b7c3de7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293113"
---
# <a name="odbc-jet-error-messages"></a>ODBC Jet 오류 메시지
데이터 원본에서 발생하는 오류의 경우 ODBC 드라이버는 ODBC 파일 라이브러리에서 반환된 오류 메시지를 반환합니다. ODBC 드라이버 또는 드라이버 관리자에서 발생하는 오류의 경우 드라이버는 SQLSTATE와 연결된 텍스트를 기반으로 오류 메시지를 반환합니다.  
  
 오류 메시지에는 다음과 같은 형식이 있습니다.  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 괄호([])의 접두사는 오류의 위치를 식별합니다. 드라이버 관리자에서 오류가 발생하면 *데이터 원본이* 제공되지 않습니다. 데이터 원본에서 오류가 발생하면 *[공급업체]* 및 *[ODBC 구성 요소]* 접두사는 데이터 원본에서 오류를 받은 ODBC 구성 요소의 공급업체와 이름을 식별합니다.  
  
 다음 표에서는 드라이버 관리자 및 드라이버 ISAM에서 반환된 오류 메시지를 보여 주며 있습니다.  
  
|오류 메시지|오류 위치|  
|-------------------|--------------------|  
|[마이크로 소프트] [ODBC 드라이버 매니저] *메시지 텍스트*|운전자 관리자(Odbc32.dll)|  
|[마이크로 소프트] 【 ODBC *드라이버 이름*】 *메시지 텍스트*|드라이버 ISAM(드라이버 ISAM 참조)|
