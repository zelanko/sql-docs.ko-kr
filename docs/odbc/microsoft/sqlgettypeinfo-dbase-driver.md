---
title: SQLGetTypeInfo (dBASE 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLGetTypeInfo
ms.assetid: 6e9ce02b-97c7-4c1a-91e0-829df7459c84
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 711652e22318d089b02fe8e79cb592f0a42dfff9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81295133"
---
# <a name="sqlgettypeinfo-dbase-driver"></a>SQLGetTypeInfo(dBASE 드라이버)
> [!NOTE]  
>  이 항목에서는 dBASE 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 **SQLGetTypeInfo** 에서 생성 된 테이블에 반환 되는 형식 (TYPE_NAME)의 이름은 데이터 원본에서 가장 일반적으로 사용 되는 이름입니다.  
  
 바이트, 카운터, Double, Single, Long 및 Short 데이터 형식에 대 한 검색 가능 열에 SQL_ALL_EXCEPT_LIKE 반환 됩니다. ODBC 정식 변환 함수를 사용 하 여 값을 문자로 변환한 다음 비교를 수행 하 여 이와 같은 기능을 수행할 수 있습니다.
