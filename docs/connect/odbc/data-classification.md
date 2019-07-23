---
title: Microsoft ODBC Driver for SQL Server에서 데이터 분류 사용 | Microsoft Docs
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
ms.openlocfilehash: 75688cc1e5155c83501204f1634d320b9ae7d8be
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264000"
---
# <a name="data-classification"></a>데이터 분류
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>개요
중요 한 데이터를 관리 하기 위해 SQL Server 및 Azure SQL Server는 클라이언트 응용 프로그램에서 다양 한 유형의 중요 한 데이터 (예: 상태, 금융 등)를 처리할 수 있도록 하는 민감도 메타 데이터를 데이터베이스 열에 제공 하는 기능을 도입 했습니다. )를 사용 합니다.

열에 분류를 할당 하는 방법에 대 한 자세한 내용은 [SQL 데이터 검색 및 분류](https://docs.microsoft.com/sql/relational-databases/security/sql-data-discovery-and-classification?view=sql-server-2017)를 참조 하세요.

Microsoft ODBC Driver 17.2에서는 SQL_CA_SS_DATA_CLASSIFICATION 필드 식별자를 사용 하 여 SQLGetDescField를 통해이 메타 데이터를 검색할 수 있습니다.

## <a name="format"></a>형식
SQLGetDescField에는 다음 구문이 있습니다.

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
 입력 IRD (구현 행 설명자) 핸들입니다. SQL_ATTR_IMP_ROW_DESC 문 특성을 사용 하 여 SQLGetStmtAttr를 호출 하 여 검색할 수 있습니다.
  
 *RecNumber*  
 [Input] 0
  
 *FieldIdentifier*  
 [입력] SQL_CA_SS_DATA_CLASSIFICATION
  
 *ValuePtr*  
 출력 출력 버퍼
  
 *BufferLength*  
 입력 출력 버퍼의 길이 (바이트)

 *StringLengthPtr* 출력 *Valueptr*에서 반환 하는 데 사용할 수 있는 총 바이트 수를 반환할 버퍼에 대 한 포인터입니다.
 
> [!NOTE]
> 버퍼의 크기를 알 수 없는 경우 SQLGetDescField를 *NULL로 호출* 하 고 *StringLengthPtr*의 값을 검사 하 여이를 확인할 수 있습니다.
 
데이터 분류 정보를 사용할 수 없는 경우 *잘못 된 설명자 필드* 오류가 반환 됩니다.

SQLGetDescField에 대 한 호출이 성공적으로 완료 되 면,이에 따라 결정 되는 버퍼에는 다음 데이터가 *포함 됩니다.*

 `nn nn [n sensitivitylabels] tt tt [t informationtypes] cc cc [c columnsensitivitys]`

> [!NOTE]
> `nn nn`, `tt tt` 및`cc cc` 는 가장 낮은 주소에서 가장 덜 중요 한 바이트로 저장 된 멀티 바이트 정수입니다.

*`sensitivitylabel`* 및 *`informationtype`* 는 모두 형식입니다.

 `nn [n bytes name] ii [i bytes id]`

*`columnsensitivity`* 양식

 `nn nn [n sensitivityprops]`

각 열 *(c)* 에 대해 *n* 4 바이트가 *`sensitivityprops`* 제공 됩니다.

 `ss ss tt tt`

s- *`sensitivitylabels`* 배열에 대 한 인덱스 `FF FF` 입니다 (레이블이 지정 되지 않은 경우).

레이블이 지정 되지 않은 경우 *`informationtypes`* 배열에 `FF FF` t 인덱스를 지정 합니다.


<br><br>
데이터 형식은 다음과 같은 의사 구조체로 표현 될 수 있습니다.

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
데이터 분류 메타 데이터를 읽는 방법을 보여 주는 테스트 응용 프로그램입니다. Windows에서는를 사용 하 여 `cl /MD dataclassification.c /I (directory of msodbcsql.h) /link odbc32.lib` 컴파일하고 연결 문자열과 함께 실행할 수 있으며, 분류 된 열을 반환 하는 SQL 쿼리를 매개 변수로 사용할 수 있습니다.

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

