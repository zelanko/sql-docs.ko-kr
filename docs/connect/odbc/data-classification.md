---
description: Microsoft ODBC Driver for SQL Server와 데이터 분류 사용
title: Microsoft ODBC Driver for SQL Server와 데이터 분류 사용 | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
author: v-makouz
ms.author: v-makouz
manager: kenvh
ms.openlocfilehash: a4c7664c35d4c98ebcf8f8ae4a57d2948a83624c
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081522"
---
# <a name="data-classification"></a>데이터 분류
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>개요
SQL Server와 Azure SQL Server는 중요 데이터 관리를 위해 데이터 보호 정책에 따라 클라이언트 애플리케이션에서 다양한 유형의 중요 데이터(예: 건강, 재무 등)를 처리할 수 있도록 하는 민감도 메타데이터를 데이터베이스 열에 제공하는 기능을 도입했습니다.

열에 분류를 할당하는 방법에 대한 자세한 내용은 [SQL 데이터 검색 및 분류](../../relational-databases/security/sql-data-discovery-and-classification.md)를 참조하세요.

Microsoft ODBC Driver 17.2는 SQL_CA_SS_DATA_CLASSIFICATION 필드 식별자를 사용하는 SQLGetDescField를 통해 이 메타데이터를 검색할 수 있도록 합니다.

## <a name="format"></a>형식
SQLGetDescField의 구문은 다음과 같습니다.

```  
SQLRETURN SQLGetDescField(  
     SQLHDESC        DescriptorHandle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     FieldIdentifier,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```
*DescriptorHandle*  
 [Input] IRD(구현 행 설명자) 핸들입니다. SQL_ATTR_IMP_ROW_DESC 문 특성의 SQLGetStmtAttr를 호출하여 검색할 수 있습니다.
  
 *RecNumber*  
 [Input] 0
  
 *FieldIdentifier*  
 [입력] SQL_CA_SS_DATA_CLASSIFICATION
  
 *ValuePtr*  
 [Output] 출력 버퍼
  
 *BufferLength*  
 [Input] 출력 버퍼의 길이(바이트)

 *StringLengthPtr* [Output] *ValuePtr*에 반환할 수 있는 총 바이트 수를 반환할 버퍼에 대한 포인터입니다.
 
> [!NOTE]
> 버퍼의 크기를 알 수 없다면 *ValuePtr*이 있는 SQLGetDescField를 NULL로 호출하고 *StringLengthPtr*의 값을 검사하여 확인할 수 있습니다.
 
데이터 분류 정보를 사용할 수 없는 경우 *잘못된 설명자 필드* 오류가 반환됩니다.

SQLGetDescField에 대한 호출이 성공적으로 완료되면 *ValuePtr*이 가리키는 버퍼에 다음 데이터가 포함됩니다.

 `nn nn [n sensitivitylabels] tt tt [t informationtypes] cc cc [c columnsensitivitys]`

> [!NOTE]
> `nn nn`, `tt tt`, `cc cc`는 가장 낮은 주소에서 최하위 바이트로 저장된 멀티바이트 정수입니다.

*`sensitivitylabel`* 및 *`informationtype`* 은 모두 다음 형식을 취합니다.

 `nn [n bytes name] ii [i bytes id]`

*`columnsensitivity`* 는 다음 형식을 취합니다.

 `nn nn [n sensitivityprops]`

각 열의 경우에는 *(c)* , *n* 4-byte *`sensitivityprops`* 가 있습니다.

 `ss ss tt tt`

s - *`sensitivitylabels`* 배열의 인덱스, 레이블 지정이 되지 않을 경우 `FF FF`

t - *`informationtypes`* 배열의 인덱스, 레이블 지정이 되지 않을 경우 `FF FF`


<br><br>
데이터 형식은 다음과 같은 의사 구조체로 표현될 수 있습니다.

```
struct IDnamePair {
 BYTE nameLen;
 USHORT name[nameLen];
 BYTE idLen;
 USHORT id[idLen];
};

struct SensitivityProp {
 USHORT labelIdx;
 USHORT infoTypeIdx;
};

USHORT nLabels;
struct IDnamePair labels[nLabels];
USHORT nInfoTypes;
struct IDnamePair infotypes[nInfoTypes];
USHORT nColumns;
struct {
 USHORT nProps;
 struct SensitivityProp[nProps];
} columnClassification[nColumns];
```


## <a name="code-sample"></a>코드 샘플
데이터 분류 메타데이터를 읽는 방법을 시연하는 테스트 애플리케이션입니다. Windows에서는 `cl /MD dataclassification.c /I (directory of msodbcsql.h) /link odbc32.lib`를 사용하여 컴파일하고 연결 문자열과 함께 실행할 수 있으며, 분류된 열을 반환하는 SQL 쿼리를 매개 변수로 사용할 수 있습니다.

```
#ifdef _WIN32
#include <windows.h>
#endif
#include <sql.h>
#include <sqlext.h>
#include <msodbcsql.h>
#include <stdio.h>
SQLHANDLE env, dbc, stmt;
void checkRC_exit(SQLRETURN rc, SQLHANDLE hand, SQLSMALLINT htype, int retcode, char *action)
{
    if ((rc == SQL_ERROR || rc == SQL_SUCCESS_WITH_INFO) && hand)
    {
        char msg[1024], state[6];
        int i = 0;
        SQLRETURN rc2;
        SQLINTEGER err;
        SQLSMALLINT lenout;
        while ((rc2 = SQLGetDiagRec(htype, hand, ++i, state, &err, msg, sizeof(msg), &lenout)) == SQL_SUCCESS ||
            rc2 == SQL_SUCCESS_WITH_INFO)
            printf("%d (%d)[%s]%s\n", i, err, state, msg);
    }
    if (rc == SQL_ERROR && retcode)
    {
        printf("Error occurred%s%s\n", action ? " upon " : "", action ? action : "");
        exit(retcode);
    }
}
void printLabelInfo(char *type, char **pptr)
{
    char *ptr = *pptr;
    unsigned short nlabels;
    printf("----- %s(%u) -----\n", type, nlabels = *(unsigned short*)ptr);
    ptr += sizeof(unsigned short);
    while (nlabels--)
    {
        int namelen, idlen;
        char *nameptr, *idptr;
        namelen = *ptr++;
        nameptr = ptr;
        ptr += namelen * 2;
        idlen = *ptr++;
        idptr = ptr;
        ptr += idlen * 2;
        wprintf(L"Name: \"%.*s\" Id: \"%.*s\"\n", namelen, nameptr, idlen, idptr);
    }
    *pptr = ptr;
}
int main(int argc, char **argv)
{
    unsigned char *dcbuf;
    unsigned int dclen = 0;
    SQLRETURN rc;
    SQLHANDLE ird;
    if (argc < 3)
    {
        fprintf(stderr, "usage: dataclassification connstr query\n");
        return 1;
    }
    checkRC_exit(SQLAllocHandle(SQL_HANDLE_ENV, 0, &env), 0, 0,
        2, "allocate environment");
    checkRC_exit(SQLSetEnvAttr(env, SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, 0), env, SQL_HANDLE_ENV,
        3, "set ODBC version");
    checkRC_exit(SQLAllocHandle(SQL_HANDLE_DBC, env, &dbc), env, SQL_HANDLE_ENV,
        4, "allocate connection");
    checkRC_exit(SQLDriverConnect(dbc, 0, argv[1], SQL_NTS, 0, 0, 0, SQL_DRIVER_NOPROMPT), dbc, SQL_HANDLE_DBC,
        5, "connect to server");
    checkRC_exit(SQLAllocHandle(SQL_HANDLE_STMT, dbc, &stmt), dbc, SQL_HANDLE_DBC,
        6, "allocate statement");
    checkRC_exit(SQLExecDirect(stmt, argv[2], SQL_NTS), stmt, SQL_HANDLE_STMT,
        7, "execute query");
    checkRC_exit(SQLGetStmtAttr(stmt, SQL_ATTR_IMP_ROW_DESC, (SQLPOINTER)&ird, SQL_IS_POINTER, 0), stmt, SQL_HANDLE_STMT,
        8, "get IRD handle");
    rc = SQLGetDescFieldW(ird, 0, SQL_CA_SS_DATA_CLASSIFICATION, dcbuf, 0, &dclen);
    if (rc != SQL_SUCCESS && rc != SQL_SUCCESS_WITH_INFO)
    {
        checkRC_exit(rc, ird, SQL_HANDLE_DESC, 0, 0);
        printf("Error reading SQL_CA_SS_DATA_CLASSIFICATION IRD field. Ensure that the driver and\n"
            "server both support the Data Classification feature, and that the query returns columns\n"
            "with classification information.\n");
    }
    else
    {
        SQLINTEGER dclenout;
        unsigned char *dcptr;
        unsigned short ncols;
        printf("Data Classification information (%u bytes):\n", dclen);
        if (!(dcbuf = malloc(dclen)))
        {
            printf("Memory Allocation Error");
            return 9;
        }
        checkRC_exit(SQLGetDescFieldW(ird, 0, SQL_CA_SS_DATA_CLASSIFICATION, dcbuf, dclen, &dclenout),
            ird, SQL_HANDLE_DESC, 10, "reading SQL_CA_SS_DATA_CLASSIFICATION");
        dcptr = dcbuf;
        printLabelInfo("Labels", &dcptr);
        printLabelInfo("Information Types", &dcptr);
        printf("----- Column Sensitivities(%u) -----\n", ncols = *(unsigned short*)dcptr);
        dcptr += sizeof(unsigned short);
        while (ncols--)
        {
            unsigned short nprops = *(unsigned short*)dcptr;
            dcptr += sizeof(unsigned short);
            while (nprops--)
            {
                unsigned short labelidx, typeidx;
                labelidx = *(unsigned short*)dcptr; dcptr += sizeof(unsigned short);
                typeidx = *(unsigned short*)dcptr; dcptr += sizeof(unsigned short);
                printf(labelidx == 0xFFFF ? "(none) " : "%u ", labelidx);
                printf(typeidx == 0xFFFF ? "(none)\n" : "%u\n", typeidx);
            }
            printf("-----\n");
        }
        if (dcptr != dcbuf + dclen)
        {
            printf("Error: unexpected parse of DATACLASSIFICATION data\n");
            return 11;
        }
        free(dcbuf);
    }
    return 0;
}
```

## <a name="supported-version"></a><a name="bkmk-version"></a>지원되는 버전
Microsoft ODBC Driver 17.2는 `FieldIdentifier`가 `SQL_CA_SS_DATA_CLASSIFICATION`(1237)으로 설정된 경우 `SQLGetDescField`를 통해 데이터 분류 정보를 검색할 수 있습니다. 

Microsoft ODBC Driver 17.4.1.1부터는 `SQL_CA_SS_DATA_CLASSIFICATION_VERSION`(1238) 필드 식별자를 사용하여 `SQLGetDescField`를 통해 서버에서 지원하는 데이터 분류 버전을 검색할 수 있습니다. 17.4.1.1에서는 지원되는 데이터 분류 버전이 "2"로 설정됩니다.

 

17.4.2.1부터는 "1"로 설정되고 드라이버가 SQL Server에 지원 대상으로 보고하는 버전인 기본적 데이터 분류 버전이 도입되었습니다. 새 연결 특성 `SQL_COPT_SS_DATACLASSIFICATION_VERSION`(1400)은 지원되는 버전의 데이터 분류를 애플리케이션에서 "1"부터 지원되는 최대 수까지 변경하도록 허용합니다.  

예제: 

버전을 설정하려면 SQLConnect 또는 SQLDriverConnect 호출 바로 전에 이 호출이 실행되어야 합니다.
```
ret = SQLSetConnectAttr(dbc, SQL_COPT_SS_DATACLASSIFICATION_VERSION, (SQLPOINTER)2, SQL_IS_INTEGER);
```

현재 지원되는 데이터 분류 버전의 값은 SQLGetConnectAttr 호출을 통해 검색할 수 있습니다. 
```
ret = SQLGetConnectAttr(dbc, SQL_COPT_SS_DATACLASSIFICATION_VERSION, (SQLPOINTER)&dataClassVersion, SQL_IS_INTEGER, 0);
```