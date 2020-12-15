---
description: 데이터 형식 사용
title: 데이터 형식 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC data types
- ODBC data types, about ODBC data types
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC]
- SQL Server Native Client ODBC driver, data types
- data types [ODBC], about data types
ms.assetid: 4f19b0d6-94ac-4a98-a121-57d38787864c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ea1f3c6d629fa8b0a36f4b568afaf59bf73ada44
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473514"
---
# <a name="data-type-usage"></a>데이터 형식 사용
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다음과 같은 데이터 형식을 사용 합니다.  
  
|데이터 형식|제한 사항|  
|---------------|----------------|  
|날짜 리터럴|날짜 리터럴은 SQL_TYPE_TIMESTAMP 열 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** 또는 **smalldatetime** 의 데이터 형식)에 저장 된 경우 시간 값 12:00:00:00:00:00:00:00:00:00.000|  
|**money** 및 **smallmoney**|**Money** 및 **smallmoney** 데이터 형식의 정수 부분만 의미가 있습니다. 데이터 형식 변환 중에 SQL **money** 데이터의 소수 부분이 잘린 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 오류가 아닌 경고를 반환 합니다.|  
|SQL_BINARY(Null 허용)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 이전 버전의 인스턴스에 연결되어 있으면 SQL_BINARY 열에서 Null을 허용하는 경우 데이터 원본에 저장된 데이터에 0이 붙지 않습니다. 이러한 열의 데이터가 검색 되 면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 드라이버는 오른쪽에 0으로 채웁니다. 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 수행한 작업(예: 연결)에서 만들어진 데이터에는 이러한 패딩이 없습니다.<br /><br /> 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 이전 버전의 인스턴스에서 데이터가 이러한 열에 배치되면 데이터가 너무 길어 열에 맞지 않을 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오른쪽의 데이터를 자릅니다.<br /><br /> 참고: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 및 이전 버전에 대 한 연결을 지원 합니다.|  
|SQL_CHAR(잘림)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 이전 버전의 인스턴스에 연결되어 있고 데이터가 SQL_CHAR 열에 배치되면 데이터가 너무 길어 열에 맞지 않을 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 경고 없이 오른쪽의 데이터를 자릅니다.<br /><br /> 참고: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 및 이전 버전에 대 한 연결을 지원 합니다.|  
|SQL_CHAR(Null 허용)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 이전 버전의 인스턴스에 연결되어 있으면 SQL_CHAR 열에서 Null을 허용하는 경우 데이터 원본에 저장된 데이터에 공백이 붙지 않습니다. 이러한 열의 데이터가 검색 되 면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 드라이버는 오른쪽에 공백을 사용 하 여 채웁니다. 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 수행한 작업(예: 연결)에서 만들어진 데이터에는 이러한 패딩이 없습니다.<br /><br /> 참고: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 및 이전 버전에 대 한 연결을 지원 합니다.|  
|SQL_LONGVARBINARY, SQL_LONGVARCHAR, SQL_WLONGVARCHAR|인스턴스에 연결 된 경우 여러 행에 영향을 주는 SQL_LONGVARBINARY, SQL_LONGVARCHAR 또는 SQL_WLONGVARCHAR 데이터 형식 (WHERE 절 사용)의 열 업데이트가 완전히 지원 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .*x* 이상. 4.2 x 인스턴스에 연결 된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] S1000"부분 삽입/업데이트" 라는 오류가 발생 합니다. 텍스트 또는 이미지 열의 삽입/업데이트가 실패했습니다"가 반환됩니다.<br /><br /> 참고: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 및 이전 버전에 대 한 연결을 지원 합니다.|  
|문자열 함수 매개 변수|문자열 함수에 대 한 *string_exp* 매개 변수는 SQL_CHAR 또는 SQL_VARCHAR 데이터 형식 이어야 합니다. SQL_LONG_VARCHAR 데이터 형식은 문자열 함수에서 지원되지 않습니다. SQL_CHAR 및 SQL_VARCHAR 데이터 형식은 최대 8000 문자로 제한 되므로 *count* 매개 변수는 8000 보다 작거나 같아야 합니다.|  
|시간 리터럴|시간 리터럴은 SQL_TIMESTAMP 열에 저장 된 경우 (날짜 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **/시간** 또는 **smalldatetime** 의 데이터 형식) 1900 년 1 월 1 일의 날짜 값을 갖습니다.|  
|**timestamp**|**Timestamp** 열에는 NULL 값만 수동으로 삽입할 수 있습니다. 그러나 **timestamp** 열은에 의해 자동으로 업데이트 되기 때문에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NULL 값을 덮어씁니다.|  
|**tinyint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Tinyint** 데이터 형식은 부호가 없습니다. **Tinyint** 열은 기본적으로 SQL_C_UTINYINT 데이터 형식의 변수에 바인딩됩니다.|  
|별칭 데이터 형식|4.2 x 인스턴스에 연결 된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC드라이버는 열의 null 허용 여부를 명시적으로 선언 하지 않는 열 정의에 NULL을 추가 합니다. 따라서 별칭 데이터 형식의 정의에 저장된 Null 허용 여부는 무시됩니다.<br /><br /> 4.2 x 인스턴스에 연결 된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본데이터 형식이 **char** 또는 **binary** 이 고 null 허용 여부가 선언 되지 않은 별칭 데이터 형식의 열이 **varchar** 또는 **varbinary** 데이터 형식으로 만들어집니다. [Sqlcolattribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md), [Sqlcolumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)및 [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) 는 SQL_VARCHAR 또는 SQL_VARBINARY를 이러한 열의 데이터 형식으로 반환 합니다. 해당 열에서 검색한 데이터는 채워지지 않습니다.<br /><br /> 참고: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 및 이전 버전에 대 한 연결을 지원 합니다.|  
|LONG 데이터 형식|*실행 시 데이터* 매개 변수는 SQL_LONGVARBINARY 및 SQL_LONGVARCHAR 데이터 형식 모두에 대해 제한 됩니다.|  
|큰 값 형식|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT odbc 드라이버는 ODBC SQL 데이터 형식을 허용 하거나 반환 하는 api에서 **varchar (max)**, **varbinary (max)** 및 **nvarchar (max)** 형식을 각각 SQL_VARCHAR, SQL_VARBINARY 및 SQL_WVARCHAR (각각)로 노출 합니다.|  
|UDT(사용자 정의 형식)|UDT 열은 SQL_SS_UDT로 매핑됩니다. UDT의 ToString() 또는 ToXMLString() 메서드를 사용하거나 CAST/CONVERT 함수를 통해 SQL 문에서 명시적으로 UDT 열이 다른 형식에 매핑되어 있으면 결과 집합의 열 형식은 해당 열이 변환된 실제 형식을 반영합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는 UDT 열에 이진 으로만 바인딩할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 SQL_SS_UDT 및 SQL_C_BINARY 데이터 형식 간의 변환만 지원합니다.|  
|XML|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 자동으로 XML을 유니코드 텍스트로 변환합니다. XML 유형은 SQL_SS_XML로 매핑됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;결과 처리 ](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
