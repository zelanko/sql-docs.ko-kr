---
description: SQL 적합성 수준(Oracle용 ODBC 드라이버)
title: SQL 규칙 수준 (Oracle 용 ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- ODBC driver for Oracle [ODBC], conformance levels
ms.assetid: 077a6c6a-2c57-42c9-a4fd-4cf0e65cf7e2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78e98aed952ef8b15a4654be9f82e355d1b4177b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483426"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>SQL 적합성 수준(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 Oracle 용 ODBC 드라이버는 최소 SQL 문법 및 핵심 SQL 문법을 지원 하 고 SQL에 대 한 다음 ODBC 확장도 지원 합니다.  
  
-   날짜, 시간 및 타임 스탬프 데이터  
  
-   왼쪽 및 오른쪽 우선 외부 조인  
  
-   숫자 함수:  

    :::row:::
        :::column:::
            Abs  
            Ceiling  
            Cos  
            Exp  
            Floor  
        :::column-end:::
        :::column:::
            로그  
            Log10  
            Mod  
            Pi  
            전력  
        :::column-end:::
        :::column:::
            round  
            second  
            sign  
            sin  
            sqrt  
        :::column-end:::
        :::column:::
            tan  
            truncate  
        :::column-end:::
    :::row-end:::
    
-   날짜 함수:  

    :::row:::
        :::column:::
            Curdate  
            Curtime  
            Dayname  
            Dayofmonth  
        :::column-end:::
        :::column:::
            Dayofweek  
            Dayofyear  
            시간  
            월  
        :::column-end:::
        :::column:::
            monthname  
            minute  
            now  
            quarter  
        :::column-end:::
        :::column:::
            second  
            week  
            year  
        :::column-end:::
    :::row-end:::

-   문자열 함수:  

    :::row:::
        :::column:::
            ASCII  
            Char  
            Concat  
            Lcase  
        :::column-end:::
        :::column:::
            왼쪽  
            길이  
            Ltrim  
            바꾸기  
        :::column-end:::
        :::column:::
            오른쪽  
            rtrim  
            soundex  
            substring  
        :::column-end:::
        :::column:::
            ucase  
        :::column-end:::
    :::row-end:::

-   형식 변환 함수:  

    변환  

-   시스템 함수:  
  
    Ifnull  
    사용자
