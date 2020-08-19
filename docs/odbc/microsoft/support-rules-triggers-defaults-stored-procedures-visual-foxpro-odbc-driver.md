---
description: 규칙, 트리거, 기본값 및 저장 프로시저 지원(Visual FoxPro ODBC 드라이버)
title: 규칙, 트리거, 기본값 및 저장 프로시저에 대 한 지원 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], stored procedures
- FoxPro ODBC driver [ODBC], commands and functions
- commands for FoxPro ODBC driver [ODBC]
- FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], triggers
- stored procedures [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], rules
- FoxPro commands and functions [ODBC]
- rules [ODBC]
- Visual FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], rules
- functions [ODBC], Visual FoxPro
- default values [ODBC]
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro ODBC driver [ODBC], triggers
- FoxPro ODBC driver [ODBC], stored procedures
- Visual FoxPro commands and functions [ODBC]
ms.assetid: e449de20-d6ca-4902-9f8e-814eb6e86650
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56b1a2e50f26da8ce5ef581f8eda7c6a96afd741
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449115"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>규칙, 트리거, 기본값 및 저장 프로시저 지원(Visual FoxPro ODBC 드라이버)
Visual foxpro 규칙, 트리거, 기본값 또는 저장 프로시저는 Visual FoxPro ODBC 드라이버를 사용 하 여 만들 수 없습니다. 그러나 응용 프로그램은 데이터베이스에 저장 된 Visual FoxPro 데이터를 삽입, 업데이트 또는 삭제할 때 기존 규칙, 트리거, 기본값 또는 저장 프로시저와 상호 작용할 수 있습니다.  
  
 다음 표에서는 명령 또는 함수가 규칙, 트리거, 기본값 또는 저장 프로시저에 있는 경우 Visual FoxPro ODBC 드라이버에서 지 원하는 Visual FoxPro 명령 및 함수를 나열 합니다.  
  
 응용 프로그램이 규칙, 트리거, 기본값 또는 저장 프로시저가 다른 Visual FoxPro 명령이 나 함수를 호출 하는 데이터와 상호 작용 하는 경우 드라이버에서 오류를 생성 합니다. 드라이버에서 지원 하지 않는 명령 및 함수 목록은 [지원 되지 않는 Visual FoxPro 명령 및 함수](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md) 를 참조 하세요.  
  
> [!TIP]  
>  드라이버에서 호출할 때 실행할 명령을 결정 하는 조건부 코드를 규칙, 트리거 또는 저장 프로시저에 삽입 하려는 경우 **VERSION ()** 함수를 사용할 수 있습니다. **VERSION ()** 함수는 *\<version>* 드라이버에서 호출 될 때 "Visual FoxPro ODBC 드라이버"를 반환 합니다.  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>규칙, 트리거, 기본값 및 저장 프로시저에서 지원 되는 Visual FoxPro 명령 및 함수  

:::row:::
    :::column:::
        $ 연산자  
        % 연산자  
    :::column-end:::
    :::column:::
        & 명령  
        && 명령  
    :::column-end:::
    :::column:::
        \* 명령  
        = 명령  
    :::column-end:::
:::row-end:::

## <a name="a"></a>A  

:::row:::
    :::column:::
        ABS () 함수  
        ACOPY () 함수  
        ACOS () 함수  
        ADATABASES () 함수  
        ADBOBJECTS () 함수  
        테이블 추가 명령  
        ADEL () 함수  
        AELEMENT () 함수  
        AERROR () 함수  
        AFIELDS () 함수  
        AINS () 함수  
        ALEN () 함수  
        ALIAS () 함수  
    :::column-end:::
    :::column:::
        ALLTRIM () 함수  
        ALTER TABLE - SQL 명령  
        AND 연산자  
        추가 명령  
        명령에서 추가  
        배열에서 추가 명령  
        일반 명령 추가  
        메모 추가 명령  
        프로시저 추가 명령  
        ASC () 함수  
        ASCAN () 함수  
        ASIN () 함수  
        ASORT () 함수  
    :::column-end:::
    :::column:::
        ASUBSCRIPT () 함수  
        AT () 함수  
        AT_C () 함수  
        ATAN () 함수  
        ATC () 함수  
        ATCC () 함수  
        ATCLINE () 함수  
        ATLINE () 함수  
        ATN2 () 함수  
        AUSED () 함수  
        평균 명령  
    :::column-end:::
:::row-end:::

## <a name="b"></a>b  

:::row:::
    :::column:::
        BEGIN TRANSACTION 명령  
        BETWEEN () 함수  
        BITAND () 함수  
        BITCLEAR () 함수  
        BITLSHIFT () 함수  
    :::column-end:::
    :::column:::
        BITNOT () 함수  
        BITOR () 함수  
        BITRSHIFT () 함수  
        BITSET () 함수  
        BITTEST () 함수  
    :::column-end:::
    :::column:::
        BITXOR () 함수  
        빈 명령  
        BOF () 함수  
    :::column-end:::
:::row-end:::

## <a name="c"></a>C  

:::row:::
    :::column:::
        CALCULATE 명령  
        후보 () 함수  
        CDOW () 함수  
        CDX () 함수  
        천장 () 함수  
        CHR () 함수  
        CHRTRAN () 함수  
        CHRTRANC () 함수  
        닫기 명령  
        CMONTH () 함수  
    :::column-end:::
    :::column:::
        CONTINUE 명령  
        인덱스 복사 명령  
        프로시저 복사 명령  
        구조 복사 명령  
        구조 복사 확장 명령  
        태그 복사 명령  
        복사 명령  
        배열에 복사 명령  
        COS () 함수  
        COUNT 명령  
    :::column-end:::
    :::column:::
        CPCONVERT () 함수  
        CPCURRENT () 함수  
        CPDBF () 함수  
        CTOD () 함수  
        CTOT () 함수  
        CURSORGETPROP () 함수  
        CURSORSETPROP () 함수  
        CURVAL () 함수  
    :::column-end:::
:::row-end:::

## <a name="d"></a>D  

:::row:::
    :::column:::
        DATE () 함수  
        DATETIME () 함수  
        DAY () 함수  
        DBC () 함수  
        DBF () 함수  
        DBGETPROP () 함수  
        DBUSED () 함수  
        DELETE - SQL 명령  
    :::column-end:::
    :::column:::
        DELETE 명령  
        DELETE TAG 명령  
        DELETED () 함수  
        내림차순 () 함수  
        차 () 함수  
        차원 명령  
        DISKSPACE () 함수  
        AMY () 함수  
    :::column-end:::
    :::column:::
        DO 명령  
        DO CASE ... ENDCASE 명령  
        수행 하는 동안 ... ENDDO 명령  
        DOW () 함수  
        ETOC () 함수  
        DTOR () 함수  
        DTO () 함수  
        DTOT () 함수  
    :::column-end:::
:::row-end:::

## <a name="e"></a>E  

:::row:::
    :::column:::
        EMPTY () 함수  
        END TRANSACTION 명령  
        EOF () 함수  
    :::column-end:::
    :::column:::
        ERROR () 함수  
        EVALUATE () 함수  
        끝내기 명령  
    :::column-end:::
    :::column:::
        EXP () 함수  
    :::column-end:::
:::row-end:::

## <a name="f"></a>F  

:::row:::
    :::column:::
        FCOUNT () 함수  
        FDATE () 함수  
        FIELD () 함수  
        FILE () 함수  
        FILTER () 함수  
        FLDLIST () 함수  
    :::column-end:::
    :::column:::
        FLOCK () 함수  
        FLOOR () 함수  
        플러시 명령  
        FOR () 함수  
        ... ENDFOR 명령  
        FOUND () 함수  
    :::column-end:::
    :::column:::
        FREE 테이블 명령  
        FSIZE () 함수  
        FTIME () 함수  
        FULLPATH () 함수  
        함수 명령  
        FV () 함수  
    :::column-end:::
:::row-end:::

## <a name="g"></a>G  

:::row:::
    :::column:::
        수집 명령  
        GETCP () 함수  
        GETENV () 함수  
    :::column-end:::
    :::column:::
        GETFLDSTATE () 함수  
        GETNEXTMODIFIED () 함수  
        GO/GOTO 명령  
    :::column-end:::
    :::column:::
        GOMONTH () 함수  
    :::column-end:::
:::row-end:::

## <a name="h"></a>H  

:::row:::
    :::column:::
        HEADER () 함수
    :::column-end:::
    :::column:::
        HOUR () 함수
    :::column-end:::
:::row-end:::

## <a name="i"></a>I  

:::row:::
    :::column:::
        IDXCOLLATE () 함수  
        ... ENDIF 명령  
        IIF () 함수  
        INDBC () 함수  
        INDEX 명령  
        INLIST () 함수  
    :::column-end:::
    :::column:::
        SQL 명령 삽입  
        INT () 함수  
        ISALPHA () 함수  
        ISBLANK () 함수  
        ISDIGIT () 함수  
        ISEXCLUSIVE () 함수  
    :::column-end:::
    :::column:::
        ISLEADBYTE () 함수  
        ISLOWER () 함수  
        ISNULL () 함수  
        ISREADONLY () 함수  
        ISUPPER () 함수  
    :::column-end:::
:::row-end:::

## <a name="k"></a>K  

:::row:::
    :::column:::
        KEY () 함수
    :::column-end:::
    :::column:::
        KEYMATCH () 함수
    :::column-end:::
:::row-end:::

## <a name="l"></a>L  

:::row:::
    :::column:::
        LEFT () 함수  
        왼쪽 c () 함수  
        LEN () 함수  
        LENC () 함수  
        LIKE () 함수  
        LIKEC () 함수  
    :::column-end:::
    :::column:::
        LOCAL 명령  
        찾기 명령  
        LOCK () 함수  
        LOG () 함수  
        LOG10 () 함수  
        LOOKUP () 함수  
    :::column-end:::
    :::column:::
        LOWER () 함수  
        LPARAMETERS 명령  
        LTRIM () 함수  
        LUPDATE () 함수  
    :::column-end:::
:::row-end:::

## <a name="m"></a>M  

:::row:::
    :::column:::
        MAX () 함수  
        MDX () 함수  
        MDY () 함수  
        MEMLINES () 함수  
    :::column-end:::
    :::column:::
        MESSAGE () 함수  
        MIN () 함수  
        MINUTE () 함수  
        _MLINE 시스템 메모리 변수  
    :::column-end:::
    :::column:::
        MLINE () 함수  
        MOD () 함수  
        MONTH () 함수  
        MTON () 함수  
    :::column-end:::
:::row-end:::

## <a name="n"></a>N  

:::row:::
    :::column:::
        NDX () 함수  
        정규화 () 함수  
    :::column-end:::
    :::column:::
        NOT 연산자  
        NOTE 명령  
    :::column-end:::
    :::column:::
        NTOM () 함수  
        NVL () 함수  
    :::column-end:::
:::row-end:::

## <a name="o"></a>O  

:::row:::
    :::column:::
        Occurs () 함수  
        OLDVAL () 함수  
        ON () 함수  
    :::column-end:::
    :::column:::
        ON ERROR 명령  
        ON KEY 명령  
        데이터베이스 열기 명령  
    :::column-end:::
    :::column:::
        OR 연산자  
        ORDER () 함수  
        OS () 함수  
    :::column-end:::
:::row-end:::

## <a name="p"></a>P  

:::row:::
    :::column:::
        PACK 명령  
        PADL () &#124; PADR () &#124; PADC () 함수  
        PARAMETERS 명령  
        PARAMETERS () 함수  
        결제 () 함수  
    :::column-end:::
    :::column:::
        PI () 함수  
        PRIMARY () 함수  
        PRIVATE 명령  
        프로시저 명령  
        PROGRAM () 함수  
    :::column-end:::
    :::column:::
        적절 한 () 함수  
        공용 명령  
        PV () 함수  
    :::column-end:::
:::row-end:::

## <a name="r"></a>R  

:::row:::
    :::column:::
        RAND () 함수  
        RAT () 함수  
        RATC () 함수  
        RATLINE () 함수  
        회수 명령  
        RECCOUNT () 함수  
        -NO () 함수  
        고 크기 () 함수  
    :::column-end:::
    :::column:::
        국가별 명령  
        RELATION () 함수  
        테이블 제거 명령  
        REPLACE 명령  
        배열에서 바꾸기 명령  
        복제 () 함수  
        RETRY 명령  
        반환 명령  
    :::column-end:::
    :::column:::
        RIGHT () 함수  
        RIGHTC () 함수  
        RLOCK () 함수  
        ROLLBACK 명령  
        ROUND () 함수  
        RTOD () 함수  
        RTRIM () 함수  
    :::column-end:::
:::row-end:::

## <a name="s"></a>S  

:::row:::
    :::column:::
        검색 ... ENDSCAN 명령  
        분산형 명령  
        SEC () 함수  
        SECONDS () 함수  
        SEEK 명령  
        SEEK () 함수  
        명령 선택  
        SELECT () 함수  
        SELECT-SQL 명령  
        SET () 함수  
        SET BLOCKSIZE 명령  
        SET 운반 명령  
        세기 명령 설정  
        SET COLLATE 명령  
        데이터베이스 명령 설정  
        날짜 설정 명령  
        기본 명령 설정  
        SET DELETED 명령  
        SET EXACT 명령  
        SET EXCLUSIVE 명령  
        SET FDOW 명령  
    :::column-end:::
    :::column:::
        SET FIELDS 명령  
        필터 명령 설정  
        고정 명령 설정  
        SET FULLPATH 명령  
        FWEEK 명령 설정  
        시간 설정 명령  
        인덱스 설정 명령  
        잠금 명령 설정  
        SET MULTILOCKS 명령  
        NEAR 명령 설정  
        NOCPTRANS 명령 설정  
        알림 설정 명령  
        SET NULL 명령  
        최적화 명령 설정  
        SET ORDER 명령  
        SET PATH 명령  
        SET PROCEDURE 명령  
        RELATION 명령 설정  
        관계 해제 명령 설정  
        SET REPROCESS 명령  
        SKIP 명령 설정  
    :::column-end:::
    :::column:::
        SET UDFPARMS 명령  
        SET UNIQUE 명령  
        볼륨 설정 명령  
        SETFLDSTATE () 함수  
        SIGN () 함수  
        SIN () 함수  
        SKIP 명령  
        정렬 명령  
        SPACE () 함수  
        SQRT () 함수  
        저장 명령  
        STR () 함수  
        STRCONV () 함수  
        STRTRAN () 함수  
        사물 () 함수  
        STUFFC () 함수  
        SUBSTR () 함수  
        SUBSTRC () 함수  
        SUM 명령  
        SYS (2011) 함수  
    :::column-end:::
:::row-end:::

## <a name="t"></a>T  

:::row:::
    :::column:::
        TABLEREVERT () 함수  
        TABLEUPDATE () 함수  
        TAG () 함수  
        TAGCOUNT () 함수  
        TAGNO () 함수  
        _TALLY 시스템 메모리 변수  
    :::column-end:::
    :::column:::
        TAN () 함수  
        TARGET () 함수  
        TIME () 함수  
        TOTAL 명령  
        _TRIGGERLEVEL 시스템 메모리 변수  
        TRIM () 함수  
    :::column-end:::
    :::column:::
        TTOC () 함수  
        TTOD () 함수  
        TXNLEVEL () 함수  
        TYPE () 함수  
    :::column-end:::
:::row-end:::

## <a name="u"></a>U  

:::row:::
    :::column:::
        UNIQUE () 함수  
        잠금 해제 명령  
        UPDATE 명령  
    :::column-end:::
    :::column:::
        UPDATE - SQL 명령  
        UPPER () 함수  
        명령 사용  
    :::column-end:::
    :::column:::
        USED () 함수  
    :::column-end:::
:::row-end:::

## <a name="v"></a>V  

:::row:::
    :::column:::
        VAL () 함수
    :::column-end:::
    :::column:::
        VERSION () 함수
    :::column-end:::
:::row-end:::

## <a name="w"></a>W  

WEEK () 함수

## <a name="y"></a>Y  

YEAR () 함수

## <a name="z"></a>Z  

ZAP 명령
