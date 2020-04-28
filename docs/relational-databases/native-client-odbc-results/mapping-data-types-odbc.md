---
title: 데이터 형식 매핑 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- mapping data types [ODBC]
- result sets [ODBC], data types
- ODBC data types, mapping
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC], mapping
- sql_variant data type
- SQL Server Native Client ODBC driver, data types
ms.assetid: 4ba0924d-9fca-4c48-aced-0a8d817b3dde
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 92426c854758d07a9d62ec57510d202b870dd9f2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304635"
---
# <a name="mapping-data-types-odbc"></a>데이터 형식 매핑(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client odbc 드라이버는 sql [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 odbc sql 데이터 형식에 매핑합니다. 아래 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL 데이터 형식과 이러한 데이터 형식이 매핑되는 ODBC SQL 데이터 형식에 대해 설명합니다. 또한 ODBC SQL 데이터 형식 및 해당 ODBC C 데이터 형식과 지원되는 변환 및 기본 변환에 대해 설명합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Timestamp 데이터 형식은** **timestamp** 열의 값이 **datetime** 값이 아니라 행의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업 순서를 나타내는 **BINARY (8)** 또는 **VARBINARY (8)** 값 이기 때문에 SQL_BINARY 또는 SQL_VARBINARY ODBC 데이터 형식에 매핑됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에서 바이트 수가 홀수인 SQL_C_WCHAR(유니코드) 값을 발견하면 후행 홀수 바이트가 잘립니다.  
  
## <a name="dealing-with-sql_variant-data-type-in-odbc"></a>ODBC의 sql_variant 데이터 형식 처리  
 **Sql_variant** 데이터 형식 열에는 **text**, **Ntext**및 **image**와 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lob (large objects)를 제외한의 데이터 형식이 포함 될 수 있습니다. 예를 들어 열에는 일부 행에 대해 **smallint** 값, 다른 행의 경우 **float** 값, 나머지에는 **char/nchar** 값이 포함 될 수 있습니다.  
  
 **Sql_variant** 데이터 형식은 Microsoft Visual Basic®의 **variant** 데이터 형식과 비슷합니다.  
  
### <a name="retrieving-data-from-the-server"></a>서버에서 데이터 검색  
 ODBC에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는의 odbc 드라이버를 사용 하 여 **sql_variant** 데이터 형식의 사용을 제한 하는 variant 형식의 개념이 없습니다. 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]바인딩이 지정 된 경우 **sql_variant** 데이터 형식이 문서화 된 ODBC 데이터 형식 중 하나에 바인딩되어야 합니다. Native Client ODBC 드라이버와 관련 된 새 특성인 SQL_CA_SS_VARIANT_TYPE는 **sql_variant** 열에 있는 인스턴스의 데이터 형식을 사용자에 게 반환 합니다. **SQL_CA_SS_VARIANT_TYPE** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 바인딩이 지정 되지 않은 경우 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 함수를 사용 하 여 **sql_variant** 열에서 인스턴스의 데이터 형식을 확인할 수 있습니다.  
  
 **Sql_variant** 데이터를 검색 하려면 다음 단계를 수행 합니다.  
  
1.  **Sqlfetch** 를 호출 하 여 검색 된 행에 배치 합니다.  
  
2.  **SQLGetData**를 호출 하 여 형식에 대 한 SQL_C_BINARY를 지정 하 고 데이터 길이에 대해 0을 지정 합니다. 이렇게 하면 드라이버가 **sql_variant** 헤더를 강제로 읽습니다. 헤더는 **sql_variant** 열에 해당 인스턴스의 데이터 형식을 제공 합니다. **SQLGetData** 는 값의 크기 (바이트)를 반환 합니다.  
  
3.  특성 값으로 **SQL_CA_SS_VARIANT_TYPE** 를 지정 하 여 [sqlcolattribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) 를 호출 합니다. 이 함수는 **sql_variant** 열에 있는 인스턴스의 C 데이터 형식을 클라이언트에 반환 합니다.  
  
 위의 단계를 보여 주는 코드 세그먼트는 다음과 같습니다.  
  
```  
while ((retcode = SQLFetch (hstmt))==SQL_SUCCESS)  
{  
    if (retcode != SQL_SUCCESS && retcode != SQL_SUCCESS_WITH_INFO)  
    {  
        SQLError (NULL, NULL, hstmt, NULL,   
                    &lNativeError,szError,MAX_DATA,&sReturned);  
        printf_s ("%s\n",szError);  
        goto Exit;  
    }  
    retcode = SQLGetData (hstmt, 1, SQL_C_BINARY,   
                                pBuff,0,&Indicator);//Figure out the length  
    if (retcode != SQL_SUCCESS_WITH_INFO && retcode != SQL_SUCCESS)  
    {  
        SQLError (NULL, NULL, hstmt, NULL, &lNativeError,   
                    szError,MAX_DATA,&sReturned);  
        printf_s ("%s\n",szError);  
        goto Exit;  
    }  
    printf_s ("Byte length : %d ",Indicator); //Print out the byte length  
  
    int iValue = 0;  
    retcode = SQLColAttribute (hstmt, 1, SQL_CA_SS_VARIANT_TYPE, NULL,   
                                        NULL,NULL,&iValue);  //Figure out the type  
    printf_s ("Sub type = %d ",iValue);//Print the type, the return is C_type of the column]  
  
// Set up a new binding or do the SQLGetData on that column with   
// the appropriate type  
}  
```  
  
 사용자가 [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)를 사용 하 여 바인딩을 만드는 경우 드라이버는 메타 데이터 및 데이터를 읽습니다. 그런 다음 데이터를 바인딩에 지정된 적절한 ODBC 형식으로 변환합니다.  
  
### <a name="sending-data-to-the-server"></a>데이터를 서버로 보내기  
 Native Client ODBC 드라이버와 관련 된 새 데이터 유형인 SQL_SS_VARIANT는 **sql_variant** 열로 전송 되는 데이터에 사용 됩니다. **SQL_SS_VARIANT** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 매개 변수를 사용 하 여 서버에 데이터를 전송 하는 경우 (예: INSERT INTO TableName VALUES (?,?)) [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) 는 C 형식 및 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식을 포함 하는 매개 변수 정보를 지정 하는 데 사용 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 드라이버는 C 데이터 형식을 적절 한 **sql_variant** 하위 형식 중 하나로 변환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;결과 처리](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
