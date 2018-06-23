---
title: bcp_setcolfmt | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- bcp_setcolfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_setcolfmt function
ms.assetid: afb47987-39e7-4079-ad66-e0abf4d4c72b
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 87c86d900f8923bfbed16fc890298d49be036909
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089936"
---
# <a name="bcpsetcolfmt"></a>bcp_setcolfmt
  **bcp_setcolfmt** 함수를 대체는 [bcp_colfmt](bcp-colfmt.md)합니다. 열 데이터 정렬을 지정 하는 **bcp_setcolfmt** 함수를 사용 해야 합니다. [bcp_setbulkmode](bcp-setbulkmode.md) 는 둘 이상의 열 형식을 지정 하는 데 사용할 수 있습니다.  
  
 이 함수를 사용하면 대량 복사 작업에서 열 형식을 융통성 있게 지정할 수 있습니다. 이 함수는 개별 열의 형식 특성을 설정하는 데 사용합니다. 호출할 때마다 **bcp_setcolfmt** 한 열 형식 특성을 설정 합니다.  
  
 **bcp_setcolfmt** 함수 사용자 파일의 데이터 원본 또는 대상 형식을 지정 합니다. 원본 형식으로 사용 될 경우 **bcp_setcolfmt** 테이블에 대량 복사에서 데이터의 데이터 원본으로 사용 되는 기존 데이터 파일의 형식을 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 지정 된 열 형식을 사용 하 여 데이터 파일을 만들 대상 형식으로 사용 하는 경우 **bcp_setcolfmt**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_setcolfmt (  
HDBC   
hdbc  
,  
INT   
field  
,  
INT   
property  
,  
void*   
pValue  
,  
INT   
cbValue  
);  
  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
 *field*  
 속성을 설정할 서수 열 번호입니다.  
  
 *property*  
 속성 상수 중 하나입니다. 다음 표에는 속성 상수가 정의되어 있습니다.  
  
|속성|값|Description|  
|--------------|-----------|-----------------|  
|BCP_FMT_TYPE|BYTE|사용자 파일에 있는 이 열의 데이터 형식입니다. 데이터베이스 테이블에 있는 해당 열의 데이터 형식과 다를 경우 대량 복사에서 가능한 경우 데이터를 변환합니다.<br /><br /> BCP_FMT_TYPE 매개 변수는 ODBC C 데이터 형식 열거자가 아닌 sqlncli.h의 SQL Server 데이터 형식 토큰에 의해 열거됩니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 SQLCHARACTER 형식을 사용하여 ODBC 형식의 SQL_C_CHAR라는 문자열을 지정할 수 있습니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에 대한 기본 데이터 표현을 지정하려면 이 매개 변수를 0으로 설정합니다.<br /><br /> SQL Server에서 파일로의 대량 복사에서 BCP_FMT_TYPE이 SQLDECIMAL 또는 SQLNUMERIC인 경우<br /><br /> -원본 열이 없으면 **10 진수** 또는 **숫자**, 기본 전체 자릿수 및 소수 자릿수가 사용 됩니다.<br />-원본 열이 있으면 **10 진수** 또는 **숫자**, 전체 자릿수와 소수 자릿수가 원본 열이 사용 됩니다.|  
|BCP_FMT_INDICATOR_LEN|INT|표시기(접두사)의 길이(바이트)입니다.<br /><br /> 열 데이터의 길이 또는 null 표시기의 길이(바이트)입니다. 올바른 표시기 길이 값은 0(표시기를 사용하지 않을 경우), 1, 2 또는 4입니다.<br /><br /> 기본 대량 복사 표시기를 사용하도록 지정하려면 이 매개 변수를 SQL_VARLEN_DATA로 설정합니다.<br /><br /> 표시기는 메모리에서는 임의의 데이터 바로 앞에 나타나고 데이터 파일에서는 표시기가 적용되는 데이터 바로 앞에 나타납니다.<br /><br /> 표시기와 최대 열 길이를 사용하거나 표시기와 종결자 시퀀스를 사용하는 등 두 가지 이상의 방법을 사용하여 데이터 파일 열 길이를 지정하는 경우 대량 복사에는 복사되는 데이터 크기가 가장 작은 방법이 선택됩니다.<br /><br /> 사용자 개입을 통해 데이터 형식이 조정되지 않는 대량 복사로 생성된 데이터 파일에는 열 데이터의 길이가 변경될 수 있거나 열이 NULL 값을 허용할 수 있는 경우 표시기가 포함됩니다.|  
|BCP_FMT_DATA_LEN|DBINT|데이터의 길이(바이트), 즉 열 길이입니다.<br /><br /> 길이 표시기나 종결자의 길이를 제외한 사용자 파일에 있는 이 열 데이터의 최대 길이(바이트)입니다.<br /><br /> BCP_FMT_DATA_LEN을 SQL_NULL_DATA로 설정하면 데이터 파일 열의 모든 값이 NULL이거나 NULL로 설정됨을 나타냅니다.<br /><br /> BCP_FMT_DATA_LEN을 SQL_VARLEN_DATA로 설정하면 시스템에서 각 열의 데이터 길이를 확인함을 나타냅니다. 일부 열의 경우 이 설정은 길이 또는 null 표시기가 생성되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 복사되는 복사본의 데이터 앞에 추가됨을 의미하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 복사되는 데이터에 표시기가 필요함을 나타냅니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문자 및 이진 데이터 형식에 대해서는 BCP_FMT_DATA_LEN이 SQL_VARLEN_DATA, SQL_NULL_DATA, 0 또는 양수 값일 수 있습니다. BCP_FMT_DATA_LEN이 SQL_VARLEN_DATA이면 시스템에서 길이 표시기(있는 경우)나 종결자 시퀀스를 사용하여 데이터 길이를 확인합니다. 길이 표시기와 종결자 시퀀스를 모두 지정하는 경우 대량 복사에는 복사되는 데이터 크기가 가장 작은 방법이 사용됩니다. BCP_FMT_DATA_LEN이 SQL_VARLEN_DATA인 경우 데이터 형식이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문자 또는 이진 형식이며 길이 표시기나 종결자 시퀀스를 모두 지정하지 않으면 시스템에서 오류 메시지를 반환합니다.<br /><br /> BCP_FMT_DATA_LEN이 0이나 양수 값이면 시스템에서 BCP_FMT_DATA_LEN을 최대 데이터 길이로 사용합니다. 그러나 양수 BCP_FMT_DATA_LEN과 함께 길이 표시기 또는 종결자 시퀀스도 지정하는 경우 시스템에서는 복사되는 데이터가 적은 방법을 사용하여 데이터 길이를 확인합니다.<br /><br /> BCP_FMT_DATA_LEN 값은 데이터의 바이트 수를 나타냅니다. 문자 데이터가 유니코드 와이드 문자로 표현되는 경우 양수 BCP_FMT_DATA_LEN 매개 변수 값은 문자 수에 각 문자의 크기(바이트)를 곱한 값을 나타냅니다.|  
|BCP_FMT_TERMINATOR|LPCBYTE|이 열에 사용할 종결자 시퀀스(ANSI 또는 유니코드)에 대한 포인터입니다. 이 매개 변수는 주로 문자 데이터 형식에 유용한데 그 이유는 다른 모든 형식은 길이가 고정되어 있거나 이진 데이터의 경우 현재 바이트 수를 정확하게 기록하기 위해 길이 표시기가 필요하기 때문입니다.<br /><br /> 추출한 데이터가 종결되지 않도록 하거나 사용자 파일의 데이터가 종결되지 않았음을 나타내려면 이 매개 변수를 NULL로 설정하십시오.<br /><br /> 종결자와 길이 표시기를 사용하거나 종결자와 최대 열 길이를 사용하는 등 두 가지 이상의 방법을 사용하여 사용자 파일 열 길이를 지정하는 경우 대량 복사에는 복사되는 데이터 크기가 가장 작은 방법이 선택됩니다.<br /><br /> 대량 복사 API는 필요한 경우 유니코드에서 MBCS로의 문자 변환을 수행합니다. 종결자 바이트 문자열 및 바이트 문자열 길이가 모두 올바르게 설정되도록 주의해야 합니다.|  
|BCP_FMT_SERVER_COL|INT|데이터베이스에서 열의 서수 위치입니다.|  
|BCP_FMT_COLLATION|LPCSTR|데이터 정렬 이름입니다.|  
  
 *pValue*  
 에 연결할 값에 대 한 포인터는 *속성*합니다. 이 인수를 사용하여 열 형식 속성을 개별적으로 설정할 수 있습니다.  
  
 *cbvalue*  
 속성 버퍼의 길이(바이트)입니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>Remarks  
 이 함수를 대체는 **bcp_colfmt** 함수입니다. 모든 기능 **bcp_colfmt** 에 제공 된 **bcp_setcolfmt** 함수입니다. 또한 열 데이터 정렬에 대한 지원도 제공합니다. 다음 열 형식 특성을 아래에 지정된 순서대로 설정하는 것이 좋습니다.  
  
 BCP_FMT_SERVER_COL  
  
 BCP_FMT_DATA_LEN  
  
 BCP_FMT_TYPE  
  
 **bcp_setcolfmt** 함수를 사용 하면 대량 복사에 사용할 사용자 파일 형식을 지정할 수 있습니다. 대량 복사의 경우 형식에는 다음과 같은 부분이 포함됩니다.  
  
-   사용자 파일 열에서 데이터베이스 열로의 매핑  
  
-   각 사용자 파일 열의 데이터 형식  
  
-   각 열에 대한 표시기(옵션)의 길이  
  
-   사용자 파일 열당 최대 데이터 길이  
  
-   각 열에 대한 종결 바이트 시퀀스(옵션)  
  
-   선택 사항인 종결 바이트 시퀀스의 길이  
  
 호출할 때마다 **bcp_setcolfmt** 사용자 파일의 한 열에 대 한 형식을 지정 합니다. 예를 들어 다섯 개의 열 사용자 데이터 파일의 세 열에 대 한 기본 설정을 변경 하려면 먼저 호출 [bcp_columns](bcp-columns.md)**(5)**, 한 다음 호출 **bcp_setcolfmt** 5 번 세 번의 호출에서 사용자 지정 형식을 설정 합니다. 나머지 두 호출에 대 한 BCP_FMT_TYPE을 0으로 설정 하 고 BCP_FMT_INDICATOR_LENGTH, BCP_FMT_DATA_LEN을 설정 하 고 *cbValue* 를 0, SQL_VARLEN_DATA 및 0 각각. 이 프로시저는 다섯 개의 열을 모두 복사하는데 이 중 세 개는 사용자 지정된 형식으로, 두 개는 기본 형식으로 복사합니다.  
  
 **bcp_columns** 함수를 호출 하기 전에 호출 해야 **bcp_setcolfmt**합니다.  
  
 호출 해야 **bcp_setcolfmt** 사용자 파일에 있는 각 열의 각 속성에 대해 한 번씩입니다.  
  
 사용자 파일의 모든 데이터를 SQL Server 테이블로 복사할 필요는 없습니다. 열을 건너뛰려면 BCP_FMT_SERVER_COL 매개 변수를 0으로 설정하여 해당 열의 데이터 형식을 지정합니다. 열을 건너뛰려면 열 형식을 지정해야 합니다.  
  
 [bcp_writefmt](bcp-writefmt.md) 함수 형식 지정에 사용할 수 있습니다.  
  
## <a name="bcpsetcolfmt-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 bcp_setcolfmt 지원  
 날짜/시간 형식에 대 한 BCP_FMT_TYPE 속성으로 사용 되는 형식으로는에 지정 된 [향상 된 날짜 및 시간 형식에 대 한 대량 복사 변경 사항 &#40;OLE DB 및 ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)합니다.  
  
 자세한 내용은 참조 [날짜 및 시간 기능 향상 &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 함수](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  