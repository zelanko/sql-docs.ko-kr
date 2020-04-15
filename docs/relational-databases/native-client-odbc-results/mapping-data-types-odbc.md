---
title: 매핑 데이터 유형(ODBC) | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304635"
---
# <a name="mapping-data-types-odbc"></a>데이터 형식 매핑(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 드라이버는 SQL 데이터 형식을 ODBC SQL 데이터 형식에 매핑합니다. 아래 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL 데이터 형식과 이러한 데이터 형식이 매핑되는 ODBC SQL 데이터 형식에 대해 설명합니다. 또한 ODBC SQL 데이터 형식 및 해당 ODBC C 데이터 형식과 지원되는 변환 및 기본 변환에 대해 설명합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **타임스탬프** 데이터 형식은 **타임스탬프** 열의 값이 **날짜 시간** 값이 아니라 행의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 활동 순서를 나타내는 **이진(8)** 또는 **varbinary(8)** 값이기 때문에 odBC 데이터 형식에 SQL_BINARY 또는 SQL_VARBINARY 매핑됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에서 바이트 수가 홀수인 SQL_C_WCHAR(유니코드) 값을 발견하면 후행 홀수 바이트가 잘립니다.  
  
## <a name="dealing-with-sql_variant-data-type-in-odbc"></a>ODBC의 sql_variant 데이터 형식 처리  
 **sql_variant** 데이터 형식 열에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **텍스트,** **ntext**및 **이미지와**같은 큰 개체(LOB)를 제외한 모든 데이터 형식이 포함될 수 있습니다. 예를 들어 열에는 일부 행에 대한 **작은 값,** 다른 행의 **float** 값 및 나머지의 **char/nchar** 값이 포함될 수 있습니다.  
  
 **sql_variant** 데이터 형식은 Microsoft Visual Basic® **변형** 데이터 형식과 유사합니다.  
  
### <a name="retrieving-data-from-the-server"></a>서버에서 데이터 검색  
 ODBC에는 변형 형식의 개념이 없기 때문에 에서 **sql_variant** ODBC 드라이버가 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sql_variant 데이터 형식의 사용을 제한합니다. 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]바인딩을 지정하면 **sql_variant** 데이터 형식이 문서화된 ODBC 데이터 형식 중 하나에 바인딩되어야 합니다. **네이티브**클라이언트 ODBC 드라이버와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관련된 새 특성인 SQL_CA_SS_VARIANT_TYPE **sql_variant** 열에 있는 인스턴스의 데이터 형식을 사용자에게 반환합니다.  
  
 바인딩을 지정하지 않으면 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 함수를 사용하여 **sql_variant** 열에서 인스턴스의 데이터 형식을 확인할 수 있습니다.  
  
 데이터를 **sql_variant** 검색하려면 다음 단계를 따르십시오.  
  
1.  검색된 행에 위치하려면 **SQLFetch를** 호출합니다.  
  
2.  **SQLGetData를**호출하여 형식에 대한 SQL_C_BINARY 및 데이터 길이에 대해 0을 지정합니다. 이렇게 하면 드라이버가 **sql_variant** 헤더를 읽게 됩니다. 헤더는 **sql_variant** 열에서 해당 인스턴스의 데이터 형식을 제공합니다. **SQLGetData** 값의 크기(바이트)를 반환합니다.  
  
3.  **SQL_CA_SS_VARIANT_TYPE** 특성 값으로 지정하여 [SQLColAttribute를](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) 호출합니다. 이 함수는 **sql_variant** 열에 있는 인스턴스의 C 데이터 형식을 클라이언트에 반환합니다.  
  
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
  
 사용자가 [SQLBindCol을](../../relational-databases/native-client-odbc-api/sqlbindcol.md)사용하여 바인딩을 만드는 경우 드라이버는 메타데이터와 데이터를 읽습니다. 그런 다음 데이터를 바인딩에 지정된 적절한 ODBC 형식으로 변환합니다.  
  
### <a name="sending-data-to-the-server"></a>데이터를 서버로 보내기  
 네이티브 클라이언트 ODBC 드라이버와 관련된 새 데이터 형식인 SQL_SS_VARIANT **sql_variant** 열로 전송되는 데이터에 사용됩니다. **SQL_SS_VARIANT** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 매개 변수를 사용하여 서버에 데이터를 보낼 때(예: 테이블이름 값(?,? 삽입))) [SQLBindParameter는](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) C 유형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 해당 형식을 포함한 매개 변수 정보를 지정하는 데 사용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 C 데이터 형식을 적절한 **sql_variant** 하위 유형 중 하나로 변환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;처리 결과](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
