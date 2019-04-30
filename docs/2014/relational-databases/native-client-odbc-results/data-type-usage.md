---
title: 데이터 형식 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 170cbfffde1b28d60617f0e0166ca9f8e31f5fb6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200188"
---
# <a name="data-type-usage"></a>데이터 형식 사용
  합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다음 데이터 형식 사용을 적용 합니다.  
  
|데이터 형식|제한 사항|  
|---------------|----------------|  
|날짜 리터럴|SQL_TYPE_TIMESTAMP 열에 저장 하는 경우 날짜 리터럴의 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식의 **datetime** 하거나 **smalldatetime**), 오전 12:00:00.000의 시간 값|  
|**money** 고 **smallmoney**|정수 부분만 합니다 **money** 및 **smallmoney** 데이터 유형은 중요 합니다. 하는 경우 SQL의 소수 부분이 **money** 데이터 형식 변환 하는 동안 데이터가 잘립니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 오류가 아니라 경고를 반환 합니다.|  
|SQL_BINARY(Null 허용)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 이전 버전의 인스턴스에 연결되어 있으면 SQL_BINARY 열에서 Null을 허용하는 경우 데이터 원본에 저장된 데이터에 0이 붙지 않습니다. 이러한 열에서 데이터를 검색할 때의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 오른쪽에 0으로 채웁니다. 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 수행한 작업(예: 연결)에서 만들어진 데이터에는 이러한 패딩이 없습니다.<br /><br /> 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 이전 버전의 인스턴스에서 데이터가 이러한 열에 배치되면 데이터가 너무 길어 열에 맞지 않을 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오른쪽의 데이터를 자릅니다. **참고:**  합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 연결에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 및 이전 버전입니다.|  
|SQL_CHAR(잘림)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 이전 버전의 인스턴스에 연결되어 있고 데이터가 SQL_CHAR 열에 배치되면 데이터가 너무 길어 열에 맞지 않을 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 경고 없이 오른쪽의 데이터를 자릅니다. **참고:**  합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 연결에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 및 이전 버전입니다.|  
|SQL_CHAR(Null 허용)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 이전 버전의 인스턴스에 연결되어 있으면 SQL_CHAR 열에서 Null을 허용하는 경우 데이터 원본에 저장된 데이터에 공백이 붙지 않습니다. 이러한 열에서 데이터를 검색할 때의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 오른쪽에 공백으로 채웁니다. 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 수행한 작업(예: 연결)에서 만들어진 데이터에는 이러한 패딩이 없습니다. **참고:**  합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 연결에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 및 이전 버전입니다.|  
|SQL_LONGVARBINARY, SQL_LONGVARCHAR, SQL_WLONGVARCHAR|인스턴스에 연결할 때 SQL_LONGVARBINARY, SQL_LONGVARCHAR 또는 SQL_WLONGVARCHAR 데이터 형식의 열 (WHERE 절 사용) 여러 행에 영향을 주는 업데이트 완전히 지원 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6. *x* 이상. 인스턴스에 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4.2*x*는 S1000 오류, "부분 삽입/업데이트 합니다. 텍스트 또는 이미지 열의 삽입/업데이트가 실패했습니다"가 반환됩니다. **참고:**  합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 연결에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 및 이전 버전입니다.|  
|문자열 함수 매개 변수|*string_exp* SQL_CHAR 또는 SQL_VARCHAR 데이터의 함수 여야 하는 문자열 매개 변수를 입력 합니다. SQL_LONG_VARCHAR 데이터 형식은 문자열 함수에서 지원되지 않습니다. 합니다 *개수* 매개 변수는 SQL_CHAR 및 SQL_VARCHAR 데이터 형식의 최대 길이가 8,000 자 제한 되기 때문 8,000 보다 작거나 이어야 합니다.|  
|시간 리터럴|SQL_TIMESTAMP 열에 저장 하는 경우 시간 리터럴의 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식의 **datetime** 하거나 **smalldatetime**), 1900 년 1 월 1 일의 날짜 값입니다.|  
|**timestamp**|NULL 값만 수동으로 삽입할 수는 **타임 스탬프** 열입니다. 그러나 때문 **타임 스탬프**열에서 자동으로 업데이트 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], NULL 값을 덮어씁니다.|  
|**tinyint**|합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **tinyint** 부호 없는 데이터 형식입니다. A **tinyint** 열은 기본적으로 SQL_C_UTINYINT 데이터 형식의 변수에 바인딩됩니다.|  
|별칭 데이터 형식|인스턴스에 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4.2*x*, ODBC 드라이버는 열의 null 허용 여부가 명시적으로 선언 하지 않는 열 정의에 NULL을 추가 합니다. 따라서 별칭 데이터 형식의 정의에 저장된 Null 허용 여부는 무시됩니다.<br /><br /> 인스턴스에 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4.2*x*, 기본 데이터가 있는 별칭 데이터 형식이 있는 열 형식의 **char** 하거나 **이진** 및 없는 null 허용 여부는 선언 된 데이터 형식으로 만들어집니다 **varchar** 하거나 **varbinary**합니다. [SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md), [SQLColumns](../native-client-odbc-api/sqlcolumns.md), 및 [SQLDescribeCol](../native-client-odbc-api/sqldescribecol.md) SQL_VARCHAR 또는 이러한 열에 대 한 입력 데이터와 SQL_VARBINARY를 반환 합니다. 해당 열에서 검색한 데이터는 채워지지 않습니다. **참고:**  합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 연결에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 및 이전 버전입니다.|  
|LONG 데이터 형식|*실행 시 데이터* 매개 변수는 SQL_LONGVARBINARY 및 SQL_LONGVARCHAR 데이터 형식에 대 한 제한 됩니다.|  
|큰 값 형식|합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 노출 **varchar (max)** 를 **varbinary (max)**, 및 **nvarchar (max)** SQL_VARCHAR, SQL_VARBINARY 및 SQL_ 형식 받아들이거나 ODBC SQL 데이터 형식을 반환 하는 각각의 Api WVARCHAR입니다.|  
|UDT(사용자 정의 형식)|UDT 열은 SQL_SS_UDT로 매핑됩니다. UDT의 ToString() 또는 ToXMLString() 메서드를 사용하거나 CAST/CONVERT 함수를 통해 SQL 문에서 명시적으로 UDT 열이 다른 형식에 매핑되어 있으면 결과 집합의 열 형식은 해당 열이 변환된 실제 형식을 반영합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 이진 형식으로 UDT 열에만 바인딩할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 SQL_SS_UDT 및 SQL_C_BINARY 데이터 형식 간의 변환만 지원합니다.|  
|XML|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 자동으로 XML을 유니코드 텍스트로 변환합니다. XML 유형은 SQL_SS_XML로 매핑됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [결과 처리 &#40;ODBC&#41;](processing-results-odbc.md)  
  
  
