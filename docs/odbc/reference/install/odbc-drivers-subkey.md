---
title: ODBC 드라이버 하위 키 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304034"
---
# <a name="odbc-drivers-subkey"></a>ODBC 드라이버 하위 키
ODBC 드라이버 하위 키 아래에 있는 값에는 설치 된 드라이버가 나열 됩니다. 이러한 값의 형식은 다음 표에 나와 있습니다.  
  
|Name|데이터 형식|데이터|  
|----------|---------------|----------|  
|*드라이버-설명*|REG_SZ|**설치됨**|  
  
 드라이버 *설명* 이름은 드라이버 개발자에 의해 정의 됩니다. 일반적으로 드라이버와 연결 된 DBMS의 이름입니다.  
  
 예를 들어, 서식이 지정 된 텍스트 파일에 대 한 드라이버를 설치 하 고 SQL Server 합니다. ODBC 드라이버 하위 키 아래의 값은 다음과 같을 수 있습니다.  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
