---
title: 데이터 형식 매핑 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 692f9cf66bdafecd85c693635b145749f4e432ff
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37408192"
---
# <a name="mapping-data-types-odbc"></a>데이터 형식 매핑(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 맵 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL 데이터 형식을 ODBC SQL 데이터 형식입니다. 아래 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL 데이터 형식과 이러한 데이터 형식이 매핑되는 ODBC SQL 데이터 형식에 대해 설명합니다. 또한 ODBC SQL 데이터 형식 및 해당 ODBC C 데이터 형식과 지원되는 변환 및 기본 변환에 대해 설명합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **타임 스탬프** 데이터 형식이 때문에 SQL_BINARY 또는 SQL_VARBINARY ODBC 데이터 형식에 매핑되 값 **타임 스탬프** 열에는 없는 **datetime** 값 하지만 **binary (8)** 또는 **varbinary(8)** 시퀀스를 나타내는 값 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 행에는 활동입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에서 바이트 수가 홀수인 SQL_C_WCHAR(유니코드) 값을 발견하면 후행 홀수 바이트가 잘립니다.  
  
## <a name="dealing-with-sqlvariant-data-type-in-odbc"></a>ODBC의 sql_variant 데이터 형식 처리  
 **sql_variant** 데이터 형식의 열 데이터 형식 중 하나를 포함할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 같은 Lob (large object)를 제외한 **텍스트**를 **ntext**, 및  **이미지**합니다. 예를 들어 열 포함할 수 있습니다 **smallint** 일부 행에 값 **float** 다른 행에 대 한 값 및 **char/nchar** 나머지의 값입니다.  
  
 합니다 **sql_variant** 데이터 형식은 비슷합니다 합니다 **Variant** Microsoft Visual Basic®의 데이터 형식입니다.  
  
### <a name="retrieving-data-from-the-server"></a>서버에서 데이터 검색  
 ODBC 없는 variant 형식의 개념이의 사용을 제한 합니다 **sql_variant** 데이터 형식에서 ODBC 드라이버를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]바인딩이 지정 하는 경우는 **sql_variant** 데이터 형식을 문서화 된 ODBC 데이터 형식 중 하나에 바인딩해야 합니다. **SQL_CA_SS_VARIANT_TYPE**, 관련 새 특성을를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버의 인스턴스 데이터 형식을 반환 합니다 **sql_variant** 사용자에 게 열입니다.  
  
 바인딩이 지정 되지 않은, 경우 합니다 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 에 있는 인스턴스의 데이터 형식을 확인 하려면 함수를 사용할 수 있습니다 합니다 **sql_variant** 열입니다.  
  
 검색할 **sql_variant** 데이터는 다음이 단계를 수행 합니다.  
  
1.  호출 **SQLFetch** 검색 된 행에 위치 합니다.  
  
2.  호출 **SQLGetData**, 형식 및 데이터 길이 0에 대 한 SQL_C_BINARY를 지정 합니다. 이렇게 하면 읽도록 드라이버에는 **sql_variant** 헤더입니다. 헤더에 있는 해당 인스턴스의 데이터 형식을 제공 합니다 **sql_variant** 열입니다. **SQLGetData** 값을 바이트 단위로 크기를 반환 합니다.  
  
3.  호출 [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) 지정 하 여 **SQL_CA_SS_VARIANT_TYPE** 특성 값으로. 이 함수는 C 데이터 형식 인스턴스를 반환 합니다 **sql_variant** 클라이언트에는 열입니다.  
  
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
  
 사용자가 사용 하 여 바인딩을 만드는 경우 [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md), 드라이버는 메타 데이터 및 데이터를 읽습니다. 그런 다음 데이터를 바인딩에 지정된 적절한 ODBC 형식으로 변환합니다.  
  
### <a name="sending-data-to-the-server"></a>데이터를 서버로 보내기  
 **SQL_SS_VARIANT**, 새 데이터 형식에 특정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 전송 된 데이터에 사용 되는 **sql_variant** 열. 매개 변수를 사용 하 여 서버에 데이터를 보낼 때 (예를 들어 INSERT INTO TableName VALUES (?,?)), [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) C 형식 및 해당를 포함 하 여 매개 변수 정보를 지정 하는 데 사용 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식입니다. 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 C 데이터 형식 중 하나로 변환 적절 한 **sql_variant** 하위 형식입니다.  
  
## <a name="see-also"></a>관련 항목  
 [결과 처리 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
