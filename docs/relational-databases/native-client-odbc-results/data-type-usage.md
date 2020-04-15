---
title: 데이터 유형 사용 | 마이크로 소프트 문서
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0384857c53e898af9fca89bb2ee2351f0b65f986
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297860"
---
# <a name="data-type-usage"></a>데이터 형식 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 드라이버를 적용하고 다음과 같은 데이터 형식 사용을 적용합니다.  
  
|데이터 형식|제한 사항|  
|---------------|----------------|  
|날짜 리터럴|SQL_TYPE_TIMESTAMP[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **열(날짜 시간** 또는 작은 날짜 **시간의**데이터 형식)에 저장된 날짜 리터럴은 시간 값12:00:00.000 A.M.입니다.|  
|**돈과** **소액**|**돈과** 작은 돈의 정수 **부분만돈** 데이터 형식이 중요합니다. 데이터 형식 변환 중에 SQL **MONEY** 데이터의 소수 부분이 잘린 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경우 네이티브 클라이언트 ODBC 드라이버는 오류가 아닌 경고를 반환합니다.|  
|SQL_BINARY(Null 허용)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 이전 버전의 인스턴스에 연결되어 있으면 SQL_BINARY 열에서 Null을 허용하는 경우 데이터 원본에 저장된 데이터에 0이 붙지 않습니다. 이러한 열의 데이터를 검색하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버가 오른쪽에 0으로 패드를 지정합니다. 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 수행한 작업(예: 연결)에서 만들어진 데이터에는 이러한 패딩이 없습니다.<br /><br /> 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 이전 버전의 인스턴스에서 데이터가 이러한 열에 배치되면 데이터가 너무 길어 열에 맞지 않을 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오른쪽의 데이터를 자릅니다.<br /><br /> 참고: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 이전 연결을 지원합니다.|  
|SQL_CHAR(잘림)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 이전 버전의 인스턴스에 연결되어 있고 데이터가 SQL_CHAR 열에 배치되면 데이터가 너무 길어 열에 맞지 않을 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 경고 없이 오른쪽의 데이터를 자릅니다.<br /><br /> 참고: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 이전 연결을 지원합니다.|  
|SQL_CHAR(Null 허용)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 이전 버전의 인스턴스에 연결되어 있으면 SQL_CHAR 열에서 Null을 허용하는 경우 데이터 원본에 저장된 데이터에 공백이 붙지 않습니다. 이러한 열의 데이터를 검색하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버가 오른쪽에 공백으로 패드를 지정합니다. 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 수행한 작업(예: 연결)에서 만들어진 데이터에는 이러한 패딩이 없습니다.<br /><br /> 참고: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 이전 연결을 지원합니다.|  
|SQL_LONGVARBINARY, SQL_LONGVARCHAR, SQL_WLONGVARCHAR|여러 행에 영향을 주는 SQL_LONGVARBINARY, SQL_LONGVARCHAR 또는 SQL_WLONGVARCHAR 데이터 형식(WHERE 절 사용)이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열의 업데이트는 6의 인스턴스에 연결될 때 완전히 지원됩니다. *x* 및 이후. 4.2*x* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , S1000 오류의 인스턴스에 연결 하면 " 부분 삽입/업데이트. 텍스트 또는 이미지 열의 삽입/업데이트가 실패했습니다"가 반환됩니다.<br /><br /> 참고: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 이전 연결을 지원합니다.|  
|문자열 함수 매개 변수|문자열 함수에 대한 *string_exp* 매개 변수는 데이터 형식 SQL_CHAR SQL_VARCHAR 있어야 합니다. SQL_LONG_VARCHAR 데이터 형식은 문자열 함수에서 지원되지 않습니다. SQL_CHAR 및 SQL_VARCHAR 데이터 형식의 최대 길이가 8,000자로 제한되므로 *count* 매개 변수는 8,000보다 작거나 같아야 합니다.|  
|시간 리터럴|시간 리터럴은 SQL_TIMESTAMP[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열(날짜 **시간** 또는 작은 **날짜 시간의**데이터 형식)에 저장될 때 1900년 1월 1일의 날짜 값을 가갖다.|  
|**타임 스탬프**|NULL 값만 **타임스탬프** 열에 수동으로 삽입할 수 있습니다. 그러나 **타임스탬프**열은 에 의해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]자동으로 업데이트되므로 NULL 값이 덮어씁니까?|  
|**tinyint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **tinyint** 데이터 형식은 서명되지 않았습니다. **tinyint** 열은 기본적으로 SQL_C_UTINYINT 데이터 형식의 변수에 바인딩됩니다.|  
|별칭 데이터 형식|4.2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *x의*인스턴스에 연결하면 ODBC 드라이버는 열의 null 가능성을 명시적으로 선언하지 않는 열 정의에 NULL을 추가합니다. 따라서 별칭 데이터 형식의 정의에 저장된 Null 허용 여부는 무시됩니다.<br /><br /> 4.2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *x의*인스턴스에 연결하면 **기본** 데이터 형식이 char 또는 **이진이** 있고 nullnull이 선언되지 않은 별칭 데이터 형식이 있는 열이 데이터 형식 **varchar** 또는 **varbinary로**만들어집니다. [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md), [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)및 [SQLDescribeCol은](../../relational-databases/native-client-odbc-api/sqldescribecol.md) 이러한 열의 데이터 형식으로 SQL_VARCHAR 또는 SQL_VARBINARY 반환합니다. 해당 열에서 검색한 데이터는 채워지지 않습니다.<br /><br /> 참고: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 이전 연결을 지원합니다.|  
|LONG 데이터 형식|*실행 시 데이터* 매개 변수는 SQL_LONGVARBINARY 및 SQL_LONGVARCHAR 데이터 형식 모두에 대해 제한됩니다.|  
|큰 값 형식|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 ODBC SQL 데이터 형식을 수락하거나 반환하는 API에서 **varchar(최대)** 및 **varbinary(최대)** 및 **nvarchar(최대)** 형식을 SQL_VARCHAR, SQL_VARBINARY 및 SQL_WVARCHAR(각각)으로 노출합니다.|  
|UDT(사용자 정의 형식)|UDT 열은 SQL_SS_UDT로 매핑됩니다. UDT의 ToString() 또는 ToXMLString() 메서드를 사용하거나 CAST/CONVERT 함수를 통해 SQL 문에서 명시적으로 UDT 열이 다른 형식에 매핑되어 있으면 결과 집합의 열 형식은 해당 열이 변환된 실제 형식을 반영합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 UDT 열에만 이진으로 바인딩할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 SQL_SS_UDT 및 SQL_C_BINARY 데이터 형식 간의 변환만 지원합니다.|  
|XML|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 자동으로 XML을 유니코드 텍스트로 변환합니다. XML 유형은 SQL_SS_XML로 매핑됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;처리 결과](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
