---
title: 데이터 입력 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e2c894b0f686385e9090b6e0a60496ede71e5c08
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184479"
---
# <a name="data-type-usage"></a>데이터 형식 사용
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다음 데이터 형식 사용을 적용 합니다.  
  
|데이터 형식|제한 사항|  
|---------------|----------------|  
|날짜 리터럴|SQL_TYPE_TIMESTAMP 열에 저장 하는 경우 날짜 리터럴의 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 유형의 **datetime** 또는 **smalldatetime**), 오전 12:00:00.000의 시간 값|  
|**money** 및 **smallmoney**|정수 부분만 **money** 및 **smallmoney** 데이터 유형은 중요 합니다. 경우 SQL의 소수 부분이 **money** 데이터 형식 변환 하는 동안 데이터는 잘리지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 오류가 아니라 경고를 반환 합니다.|  
|SQL_BINARY(Null 허용)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 이전 버전의 인스턴스에 연결되어 있으면 SQL_BINARY 열에서 Null을 허용하는 경우 데이터 원본에 저장된 데이터에 0이 붙지 않습니다. 이러한 열에서 데이터를 검색할 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 오른쪽에 0으로 채웁니다. 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 수행한 작업(예: 연결)에서 만들어진 데이터에는 이러한 패딩이 없습니다.<br /><br /> 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 이전 버전의 인스턴스에서 데이터가 이러한 열에 배치되면 데이터가 너무 길어 열에 맞지 않을 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오른쪽의 데이터를 자릅니다. **참고:** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결할 Native Client ODBC 드라이버에서는 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 및 이전 버전입니다.|  
|SQL_CHAR(잘림)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 이전 버전의 인스턴스에 연결되어 있고 데이터가 SQL_CHAR 열에 배치되면 데이터가 너무 길어 열에 맞지 않을 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 경고 없이 오른쪽의 데이터를 자릅니다. **참고:** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결할 Native Client ODBC 드라이버에서는 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 및 이전 버전입니다.|  
|SQL_CHAR(Null 허용)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 이전 버전의 인스턴스에 연결되어 있으면 SQL_CHAR 열에서 Null을 허용하는 경우 데이터 원본에 저장된 데이터에 공백이 붙지 않습니다. 이러한 열에서 데이터를 검색할 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 오른쪽에 공백으로 채웁니다. 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 수행한 작업(예: 연결)에서 만들어진 데이터에는 이러한 패딩이 없습니다. **참고:** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결할 Native Client ODBC 드라이버에서는 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 및 이전 버전입니다.|  
|SQL_LONGVARBINARY, SQL_LONGVARCHAR, SQL_WLONGVARCHAR|SQL_LONGVARBINARY, SQL_LONGVARCHAR 또는 SQL_WLONGVARCHAR 데이터 형식 (WHERE 절 사용) 여러 행에 영향을 주는 열 업데이트 완벽 하 게 지원의 인스턴스로 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6. *x* 이상. 인스턴스에 연결 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4.2*x*, S1000 오류, "부분 삽입/업데이트 합니다. 텍스트 또는 이미지 열의 삽입/업데이트가 실패했습니다"가 반환됩니다. **참고:** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결할 Native Client ODBC 드라이버에서는 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 및 이전 버전입니다.|  
|문자열 함수 매개 변수|*string_exp* SQL_CHAR 또는 SQL_VARCHAR 함수는 데이터의 여야 합니다. 문자열에 매개 변수를 입력 합니다. SQL_LONG_VARCHAR 데이터 형식은 문자열 함수에서 지원되지 않습니다. *count* 매개 변수 SQL_CHAR 및 SQL_VARCHAR 데이터 형식의 최대 길이는 8, 000 자 제한 되기 때문 8000 보다 작거나 같아야 합니다.|  
|시간 리터럴|SQL_TIMESTAMP 열에 저장 된 경우 시간 리터럴의 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 유형의 **datetime** 또는 **smalldatetime**), 1900 년 1 월 1 일의 날짜 값이 있어야 합니다.|  
|**timestamp**|에 NULL 값만 수동으로 삽입할 수는 **타임 스탬프** 열입니다. 그러나 때문에 **타임 스탬프**열은 자동으로 업데이트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], NULL 값을 덮어씁니다.|  
|**tinyint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **tinyint** 부호 없는 데이터 형식입니다. A **tinyint** 열은 기본적으로 SQL_C_UTINYINT 데이터 형식의 변수에 바인딩됩니다.|  
|별칭 데이터 형식|인스턴스에 연결 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4.2*x*, ODBC 드라이버는 열의 null 허용 여부를 명시적으로 선언 하지 않는 열 정의에 NULL을 추가 합니다. 따라서 별칭 데이터 형식의 정의에 저장된 Null 허용 여부는 무시됩니다.<br /><br /> 인스턴스에 연결 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4.2*x*, 기본 데이터에 있는 별칭 데이터 형식과 열 유형의 **char** 또는 **이진** 및 된 없는 null 허용 여부는 선언 된 데이터 형식으로 생성 **varchar** 또는 **varbinary**합니다. [SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md), [SQLColumns](../native-client-odbc-api/sqlcolumns.md), 및 [SQLDescribeCol](../native-client-odbc-api/sqldescribecol.md) SQL_VARCHAR 또는 이러한 열에 대 한 입력 데이터와 SQL_VARBINARY를 반환 합니다. 해당 열에서 검색한 데이터는 채워지지 않습니다. **참고:** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결할 Native Client ODBC 드라이버에서는 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 및 이전 버전입니다.|  
|LONG 데이터 형식|*실행 시 데이터* 매개 변수는 SQL_LONGVARBINARY 및 SQL_LONGVARCHAR 데이터 형식 모두에 대 한 제한 됩니다.|  
|큰 값 형식|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 노출 **varchar (max)**, **varbinary (max)**, 및 **nvarchar (max)** 형식을 SQL_VARCHAR, SQL_VARBINARY 및 SQL_로 WVARCHAR (각각) Api를 사용 하거나 ODBC SQL 데이터 형식을 반환 합니다.|  
|UDT(사용자 정의 형식)|UDT 열은 SQL_SS_UDT로 매핑됩니다. UDT의 ToString() 또는 ToXMLString() 메서드를 사용하거나 CAST/CONVERT 함수를 통해 SQL 문에서 명시적으로 UDT 열이 다른 형식에 매핑되어 있으면 결과 집합의 열 형식은 해당 열이 변환된 실제 형식을 반영합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 이진 형식으로 UDT 열에만 바인딩할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 SQL_SS_UDT 및 SQL_C_BINARY 데이터 형식 간의 변환만 지원합니다.|  
|XML|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 자동으로 XML을 유니코드 텍스트로 변환합니다. XML 유형은 SQL_SS_XML로 매핑됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [결과 처리 &#40;ODBC&#41;](processing-results-odbc.md)  
  
  