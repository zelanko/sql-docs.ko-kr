---
title: 'IBCPSession:: BCPControl (Native Client OLE DB 공급자) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- IBCPSession::BCPControl (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPControl method
ms.assetid: d58f3fe1-45e3-4e46-8e9c-000971829d99
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 42f50ec668d61d9244f6f2ba413095fb1642a964
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942637"
---
# <a name="ibcpsessionbcpcontrol-native-client-ole-db-provider"></a>IBCPSession:: BCPControl (Native Client OLE DB 공급자)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  대량 복사 작업에 대한 옵션을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  

HRESULT BCPControl(   
      int eOption,  
      void *iValue);  
```  
  
## <a name="remarks"></a>설명  
 **BCPControl** 메서드는 대량 복사를 취소하기 전에 허용되는 오류 수, 데이터 파일에서 복사할 첫 번째 행과 마지막 행의 번호 및 일괄 처리 크기를 비롯하여 대량 복사 작업에 대한 여러 가지 제어 매개 변수를 설정합니다.  
  
 또한 이 메서드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터를 대량 복사할 때 사용할 SELECT 문을 지정하는 데도 사용됩니다. **eOption** 인수를 BCP_OPTION_HINTS로 설정하고 **iValue** 인수를 SELECT 문이 포함된 와이드 문자열에 대한 포인터를 포함하도록 설정할 수 있습니다.  
  
 *eOption*에 가능한 값:  
  
|옵션|설명|  
|------------|-----------------|  
|BCP_OPTION_ABORT|이미 진행 중인 대량 복사 작업을 중지합니다. 다른 스레드에서 값이 BCP_OPTION_ABORT인 *eOption* 인수와 함께 **BCPControl** 메서드를 호출하여 실행 중인 대량 복사 작업을 중지할 수 있습니다. *iValue* 인수는 무시됩니다.|  
|BCP_OPTION_BATCH|일괄 처리당 행 수입니다. 기본값은 0으로, 데이터를 추출할 때 테이블에 있는 모든 행 수를 나타내거나 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 복사할 때 사용자 데이터 파일에 있는 모든 행 수를 나타냅니다. 1보다 작은 값을 지정하면 BCP_OPTION_BATCH는 기본값으로 다시 설정됩니다.|  
|BCP_OPTION_DELAYREADFMT|부울 값이 true로 설정된 경우 [IBCPSession::BCPReadFmt](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md)에서 실행 시 읽습니다. 부울 값이 false(기본값)로 설정된 경우, IBCPSession::BCPReadFmt에서 즉시 형식 파일을 읽습니다. **BCP_OPTION_DELAYREADFMT**가 true이고 IBCPSession::BCPColumns 또는 IBCPSession::BCPColFmt를 호출하는 경우 시퀀스 오류가 발생합니다.<br /><br /> `IBCPSession::BCPControl(BCPDELAYREADFMT, (void *)TRUE)` 및 IBCPSession::BCPWriteFmt를 호출한 후 `IBCPSession::BCPControl(BCPDELAYREADFMT, (void *)FALSE))`을 호출하는 경우에도 시퀀스 오류가 발생합니다.<br /><br /> 자세한 내용은 [메타데이터 검색](../../relational-databases/native-client/features/metadata-discovery.md)을 참조하세요.|  
|BCP_OPTION_FILECP|*iValue* 인수는 데이터 파일의 코드 페이지 번호를 포함합니다. 1252나 850과 같은 코드 페이지 번호를 지정하거나 다음 값 중 하나를 지정할 수 있습니다.<br /><br /> BCP_FILECP_ACP: 파일의 데이터가 클라이언트의 Microsoft Windows® 코드 페이지에 있습니다.<br /><br /> BCP_FILECP_OEMCP: 파일의 데이터가 클라이언트의 OEM 코드 페이지에 있습니다(기본값).<br /><br /> BCP_FILECP_RAW: 파일의 데이터가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 코드 페이지에 있습니다.|  
|BCP_OPTION_FILEFMT|데이터 파일 형식의 버전 번호입니다. 이 값은 80([!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]), 90([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]), 100([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 또는 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]), 110([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) 또는 120([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)])이 될 수 있습니다. 기본값은 120입니다. 이 옵션은 이전 버전 서버에서 지원하는 형식으로 데이터를 가져오고 내보내는 데 유용합니다.  예를 들어 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 서버의 텍스트 열에서 얻은 데이터를 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 서버의 **varchar(max)** 열로 가져오려면 80을 지정해야 합니다. 마찬가지로 **varchar(max)** 열에서 데이터를 내보낼 때 80을 지정하면 해당 데이터가 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 형식으로 텍스트 열이 저장되는 것과 같이 저장되어 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 서버의 텍스트 열로 가져올 수 있습니다.|  
|BCP_OPTION_FIRST|복사할 파일이나 테이블의 첫 번째 데이터 행입니다. 기본값은 1입니다. 1보다 작은 값을 지정하면 이 옵션은 기본값으로 다시 설정됩니다.|  
|BCP_OPTION_FIRSTEX|BCP out 작업의 경우 데이터 파일에 복사할 데이터베이스 테이블의 첫 번째 행을 지정합니다.<br /><br /> BCP in 작업의 경우 데이터베이스 테이블에 복사할 데이터 파일의 첫 번째 행을 지정합니다.<br /><br /> *iValue* 매개 변수는 값을 포함하는 부호 있는 64비트 정수 주소여야 합니다. BCPFIRSTEX에 전달할 수 있는 최대값은 2^63-1입니다.|  
|BCP_OPTION_FMTXML|생성되는 서식 파일이 XML 형식이 되도록 지정하는 데 사용됩니다. 이 옵션은 기본적으로 해제되어 있으며 서식 파일은 텍스트 파일로 저장됩니다. XML 서식 파일은 더 높은 유연성을 제공하지만 몇 가지 제약 조건이 있습니다. 예를 들어 이전 서식 파일에서는 가능했던 작업인 필드의 접두사와 종결자를 동시에 지정할 수 없습니다.<br /><br /> 참고: XML 서식 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구를 Native Client와 함께 설치한 경우에만 지원 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|BCP_OPTION_HINTS|*iValue* 인수는 와이드 문자열 포인터를 포함합니다. 주소가 지정된 문자열에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대량 복사 처리 힌트나 결과 집합을 반환하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 지정합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 둘 이상의 결과 집합을 반환하도록 지정된 경우 첫 번째 결과 집합 다음에 오는 결과 집합은 모두 무시됩니다.|  
|BCP_OPTION_KEEPIDENTITY|*iValue* 인수가 TRUE로 설정된 경우 이 옵션은 대량 복사 메서드에서 IDENTITY 제약 조건을 사용하여 정의된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열에 제공된 데이터 값을 삽입하도록 지정합니다. 입력 파일은 ID 열에 해당하는 값을 제공해야 합니다. 설정되지 않은 경우 삽입된 행에 대해 새 ID 값이 생성됩니다. 파일에서 ID 열에 대한 데이터는 모두 무시됩니다.|  
|BCP_OPTION_KEEPNULLS|파일의 빈 데이터 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에서 NULL 값으로 변환할지 여부를 지정합니다. *iValue* 인수가 TRUE로 설정된 경우 빈 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에서 NULL로 변환됩니다. 기본적으로 빈 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에서 열의 기본값(있는 경우)으로 변환됩니다.|  
|BCP_OPTION_LAST|복사할 마지막 행입니다. 기본값은 모든 행을 복사하는 것입니다. 1보다 작은 값을 지정하면 이 옵션은 기본값으로 다시 설정됩니다.|  
|BCP_OPTION_LASTEX|BCP out 작업의 경우 데이터 파일에 복사할 데이터베이스 테이블의 마지막 행을 지정합니다.<br /><br /> BCP in 작업의 경우 데이터베이스 테이블에 복사할 데이터 파일의 마지막 행을 지정합니다.<br /><br /> *iValue* 매개 변수는 값을 포함하는 부호 있는 64비트 정수 주소여야 합니다. BCPLASTEX에 전달할 수 있는 최대값은 2^63-1입니다.|  
|BCP_OPTION_MAXERRS|대량 복사 작업이 실패하기 전에 허용되는 오류 개수입니다. 기본값은 10입니다. 1보다 작은 값을 지정하면 이 옵션은 기본값으로 다시 설정됩니다. 대량 복사에는 최대 65,535개의 오류가 허용됩니다. 이 옵션을 65,535보다 큰 값으로 설정하려고 하는 경우 이 옵션은 65,535로 설정됩니다.|  
|BCP_OPTION_ROWCOUNT|현재(또는 마지막) BCP 작업에 의해 영향을 받는 행의 수를 반환합니다.|  
|BCP_OPTION_TEXTFILE|데이터 파일이 이진 파일이 아닌 텍스트 파일입니다. BCP는 데이터 파일의 첫 번째 2바이트에서 유니코드 바이트 표식을 확인하여 텍스트 파일이 유니코드인지 여부를 검사합니다.|  
|BCP_OPTION_UNICODEFILE|TRUE로 설정된 경우 이 옵션은 입력 파일이 유니코드 파일 형식이 되도록 지정합니다.|  
  
## <a name="arguments"></a>인수  
 *eOption*[in]  
 위의 주의 섹션에 나열된 옵션 중 하나를 설정합니다.  
  
 *iValue*[in]  
 지정한 *eOption*의 값입니다. *iValue* 인수는 64비트 값으로 추가로 확장할 수 있도록 void 포인터로 캐스팅되는 정수 값입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 메서드가 성공했습니다.  
  
 E_FAIL  
 공급자별 오류가 발생 했습니다. 자세한 내용은 [ISQLServerErrorInfo](https://docs.microsoft.com/sql/connect/oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db?view=sql-server-ver15) 인터페이스를 사용 합니다.  
  
 E_UNEXPECTED  
 예기치 않은 메서드가 호출되었습니다. 예를 들어 이 함수를 호출하기 전에 [IBCPSession::BCPInit](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) 메서드를 호출하지 않았습니다.  
  
 E_OUTOFMEMORY  
 메모리 부족 오류가 발생했습니다.  
  
## <a name="see-also"></a>참고 항목  
 [IBCPSession &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [대량 복사 작업 수행](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
  
  
