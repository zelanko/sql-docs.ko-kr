---
title: bcp_colfmt | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- bcp_colfmt
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_colfmt function
ms.assetid: 5c3b6299-80c7-4e84-8e69-4ff33009548e
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: de5e429a0b2038064bfde3cf4835d4f8edd4beff
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="bcpcolfmt"></a>bcp_colfmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  사용자 파일에 있는 데이터의 원본 또는 대상 형식을 지정합니다. 원본 형식으로 사용 될 경우 **bcp_colfmt** 대량 복사에서 데이터 원본으로 사용 되는 기존 데이터 파일의 형식을 지정 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다. 대상 형식으로 사용될 경우에는 데이터 파일이 **bcp_colfmt**에 지정된 열 형식을 사용하여 만들어집니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_colfmt (  
        HDBC hdbc,  
        INT idxUserDataCol,  
        BYTE eUserDataType,  
        INT cbIndicator,  
        DBINT cbUserData,  
        LPCBYTE pUserDataTerm,  
        INT cbUserDataTerm,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
 *idxUserDataCol*  
 형식이 지정되는 사용자 데이터 파일의 서수 열 번호입니다. 첫 번째 열은 1입니다.  
  
 *eUserDataType*  
 사용자 파일에 있는 이 열의 데이터 형식입니다. 데이터베이스 테이블에 있는 해당 열의 데이터 형식(*idxServerColumn*)과 다르면 가능한 경우 대량 복사에서 데이터를 변환합니다.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SQLXML 및 SQLUDT 데이터 형식 토큰에 대 한 지원 도입는 *eUserDataType* 매개 변수입니다.  
  
 *eUserDataType* 매개 변수 열거 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 ODBC C 데이터 형식 열거자가 아닌, 데이터 형식 토큰 sqlncli.h에 있습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 관련된 SQLCHARACTER 형식을 사용하여 ODBC 유형 SQL_C_CHAR라는 문자열을 지정할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에 대한 기본 데이터 표현을 지정하려면 이 매개 변수를 0으로 설정합니다.  
  
 대량 복사에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 파일로 때 *eUserDataType* 이 SQLDECIMAL 또는 SQLNUMERIC:  
  
-   원본 열이 **decimal** 또는 **numeric**이 아니면 기본 전체 자릿수 및 소수 자릿수가 사용됩니다.  
  
-   원본 열이 **decimal** 또는 **numeric**이면 원본 열의 전체 자릿수 및 소수 자릿수가 사용됩니다.  
  
 *cbIndicator*  
 열 데이터의 길이 또는 Null 표시기의 길이(바이트)입니다. 올바른 표시기 길이 값은 0(표시기를 사용하지 않을 경우), 1, 2, 4 또는 8입니다.  
  
 기본 대량 복사 표시기를 사용하도록 지정하려면 이 매개 변수를 SQL_VARLEN_DATA로 설정합니다.  
  
 표시기는 메모리에서는 임의의 데이터 바로 앞에 나타나고 데이터 파일에서는 표시기가 적용되는 데이터 바로 앞에 나타납니다.  
  
 표시기와 최대 열 길이를 사용하거나 표시기와 종결자 시퀀스를 사용하는 등 두 가지 이상의 방법을 사용하여 데이터 파일 열 길이를 지정하는 경우 대량 복사에는 복사되는 데이터 크기가 가장 작은 방법이 선택됩니다.  
  
 사용자 개입을 통해 데이터 형식이 조정되지 않는 대량 복사로 생성된 데이터 파일에는 열 데이터의 길이가 변경될 수 있거나 열이 NULL 값을 허용할 수 있는 경우 표시기가 포함됩니다.  
  
 *cbUserData*  
 길이 표시기나 종결자의 길이를 제외한 사용자 파일에 있는 이 열 데이터의 최대 길이(바이트)입니다.  
  
 *cbUserData* 를 SQL_NULL_DATA로 설정하면 데이터 파일 열의 모든 값이 NULL이거나 NULL로 설정해야 함을 나타냅니다.  
  
 *cbUserData* 를 SQL_VARLEN_DATA로 설정하면 시스템에서 각 열의 데이터 길이를 확인함을 나타냅니다. 일부 열의 경우 이 설정은 길이 또는 null 표시기가 생성되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 복사되는 복사본의 데이터 앞에 추가됨을 의미하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 복사되는 데이터에 표시기가 필요함을 나타냅니다.  
  
 에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문자 및 이진 데이터 형식의 *cbUserData* SQL_VARLEN_DATA, SQL_NULL_DATA, 0 또는 양수 값일 수 있습니다. *cbUserData* 가 SQL_VARLEN_DATA이면 시스템에서 길이 표시기(있는 경우)나 종결자 시퀀스를 사용하여 데이터 길이를 확인합니다. 길이 표시기와 종결자 시퀀스를 모두 지정하는 경우 대량 복사에는 복사되는 데이터 크기가 가장 작은 방법이 사용됩니다. 경우 *cbUserData* 가 SQL_VARLEN_DATA 이면 데이터 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문자 또는 이진 형식 및 길이 표시기 나 종결자 시퀀스 모두 지정 되 면 시스템 오류 메시지를 반환 합니다.  
  
 *cbUserData* 가 0이거나 양수 값이면 시스템은 *cbUserData* 를 최대 데이터 길이로 사용합니다. 그러나 *cbUserData*가 양수이고 길이 표시자 또는 종결자 시퀀스도 제공되는 경우 시스템은 복사할 데이터가 적은 방법을 사용하여 데이터 길이를 확인합니다.  
  
 *cbUserData* 값은 데이터의 바이트 수를 나타냅니다. 문자 데이터가 유니코드 와이드 문자로 표현되는 경우 양수 *cbUserData* 매개 변수 값은 문자 수와 각 문자의 바이트 크기를 곱한 값을 나타냅니다.  
  
 *pUserDataTerm*  
 이 열에 사용할 종결자 시퀀스입니다. 이 매개 변수는 주로 문자 데이터 형식에 유용한데 그 이유는 다른 모든 형식은 길이가 고정되어 있거나 이진 데이터의 경우 현재 바이트 수를 정확하게 기록하기 위해 길이 표시기가 필요하기 때문입니다.  
  
 추출한 데이터가 종결되지 않도록 하거나 사용자 파일의 데이터가 종결되지 않았음을 나타내려면 이 매개 변수를 NULL로 설정하십시오.  
  
 종결자와 길이 표시기를 사용하거나 종결자와 최대 열 길이를 사용하는 등 두 가지 이상의 방법을 사용하여 사용자 파일 열 길이를 지정하는 경우 대량 복사에는 복사되는 데이터 크기가 가장 작은 방법이 선택됩니다.  
  
 대량 복사 API는 필요한 경우 유니코드에서 MBCS로의 문자 변환을 수행합니다. 종결자 바이트 문자열 및 바이트 문자열 길이가 모두 올바르게 설정되도록 주의해야 합니다.  
  
 *cbUserDataTerm*  
 이 열에 사용할 종결자 시퀀스의 길이(바이트)입니다. 종결자가 없거나 데이터에 필요하지 않은 경우 이 값을 0으로 설정합니다.  
  
 *idxServerCol*  
 데이터베이스 테이블에서 열의 서수 위치입니다. 첫 번째 열 번호는 1입니다. 열의 서 수 위치를 보고 [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)합니다.  
  
 이 값이 0이면 대량 복사에서 데이터 파일의 열을 무시합니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>주의  
 **bcp_colfmt** 함수를 사용하여 대량 복사에 사용할 사용자 파일 형식을 지정할 수 있습니다. 대량 복사의 경우 형식에는 다음과 같은 부분이 포함됩니다.  
  
-   사용자 파일 열에서 데이터베이스 열로의 매핑  
  
-   각 사용자 파일 열의 데이터 형식  
  
-   각 열에 대한 표시기(옵션)의 길이  
  
-   사용자 파일 열당 최대 데이터 길이  
  
-   각 열에 대한 종결 바이트 시퀀스(옵션)  
  
-   선택 사항인 종결 바이트 시퀀스의 길이  
  
 **bcp_colfmt** 에 대한 각 호출에서는 사용자 파일의 한 열에 대한 서식을 지정합니다. 예를 들어 다섯 개의 열 사용자 데이터 파일의 세 열에 대 한 기본 설정을 변경 하려면 먼저 호출 [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)**(5)**, 한 다음 호출 **bcp_colfmt** 다섯 번 사용자 지정 형식을 설정 하는 것 중 3 개를 호출 합니다. 나머지 두 번의 호출에서는 *eUserDataType* 을 0으로 설정하고 *cbIndicator*, *cbUserData*및 *cbUserDataTerm* 을 각각 0, SQL_VARLEN_DATA 및 0으로 설정합니다. 이 프로시저는 다섯 개의 열을 모두 복사하는데 이 중 세 개는 사용자 지정된 형식으로, 두 개는 기본 형식으로 복사합니다.  
  
 *cbIndicator*의 경우 이제 큰 값 형식을 나타내는 값 8이 유효합니다. 해당 열이 새로운 최대 유형인 필드에 접두사가 지정되어 있으면 필드 값을 8로만 설정할 수 있습니다. 자세한 내용은 참조 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)합니다.  
  
 **bcp_colfmt** 를 호출하기 전에 **bcp_columns**함수를 호출해야 합니다.  
  
 사용자 파일에 있는 각 열에 대해 **bcp_colfmt** 를 한 번씩 호출해야 합니다.  
  
 사용자 파일의 열에 대해 **bcp_colfmt** 를 두 번 이상 호출하면 오류가 발생합니다.  
  
 사용자 파일의 모든 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블로 복사할 필요가 없습니다. 열을 건너뛰려면 *idxServerCol* 매개 변수를 0으로 설정하여 해당 열의 데이터 형식을 지정합니다. 열을 건너뛰려면 열 형식을 지정해야 합니다.  
  
 [bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md) 함수 형식 지정에 사용할 수 있습니다.  
  
## <a name="bcpcolfmt-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 bcp_colfmt 지원  
 와 사용 되는 형식에 대 한 내용은 *eUserDataType* 날짜/시간 형식에 대 한 매개 변수 참조 [향상 된 날짜 및 시간 형식에 대 한 대량 복사 변경 사항 &#40;OLE DB 및 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)합니다.  
  
 자세한 내용은 참조 [날짜 및 시간 기능 향상 & #40; ODBC & #41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [대량 복사 함수](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
