---
title: ODBC 드라이버 서브키 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], drivers subkey
- registry entries for components [ODBC], drivers subkey
- drivers subkey [ODBC]
ms.assetid: 8edbf68f-d05d-4d77-92f6-e9500008f520
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dd1f8d3293e35a543cce6b5079d9c6e10a331a88
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304034"
---
# <a name="odbc-drivers-subkey"></a>ODBC 드라이버 하위 키
ODBC 드라이버 하위 키 아래의 값은 설치된 드라이버를 나열합니다. 이러한 값의 형식은 다음 표에 나와 있습니다.  
  
|속성|데이터 형식|데이터|  
|----------|---------------|----------|  
|*드라이버 설명*|REG_SZ|**설치**|  
  
 *드라이버 설명* 이름은 드라이버 개발자가 정의합니다. 일반적으로 드라이버와 연결된 DBMS의 이름입니다.  
  
 예를 들어 서식이 지정된 텍스트 파일 및 SQL Server에 드라이버가 설치되었다고 가정합니다. ODBC 드라이버 하위 키 아래의 값은 다음과 같은 것일 수 있습니다.  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
