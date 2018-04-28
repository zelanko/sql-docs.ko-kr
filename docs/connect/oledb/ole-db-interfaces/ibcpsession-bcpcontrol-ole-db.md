---
title: 'Ibcpsession:: Bcpcontrol (OLE DB) | Microsoft Docs'
description: IBCPSession::BCPControl(OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IBCPSession::BCPControl (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPControl method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: beb59a71630220278442dcff1c1b3e96a1c69338
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="ibcpsessionbcpcontrol-ole-db"></a>IBCPSession::BCPControl(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  대량 복사 작업에 대한 옵션을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT BCPControl(   
      int eOption,  
      void *iValue);  
```  
  
## <a name="remarks"></a>주의  
 **BCPControl** 메서드 수의 일괄 처리 크기 및 데이터 파일에서 복사할 첫 번째 및 마지막 행에는 대량 복사를 취소 하기 전에 허용 되는 오류 수를 포함 하 여 대량 복사 작업에 대 한 다양 한 제어 매개 변수를 설정 합니다.  
  
 또한 이 메서드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 데이터를 대량 복사할 때 사용할 SELECT 문을 지정하는 데도 사용됩니다. 설정할 수 있습니다는 **eOption** 인수를 bcp_option_hints로 설정 하 고 **iValue** 인수 SELECT 문이 포함 된 와이드 문자열에 대 한 포인터입니다.  
  
 가능한 값에 대 한 *eOption* 됩니다.  
  
|옵션|Description|  
|------------|-----------------|  
|BCP_OPTION_ABORT|이미 진행 중인 대량 복사 작업을 중지합니다. 호출할 수 있습니다는 **BCPControl** 메서드는 *eOption* 실행 대량 복사 작업을 중지 하려면 다른 스레드에서 BCP_OPTION_ABORT의 인수입니다. *iValue* 인수는 무시 됩니다.|  
|BCP_OPTION_BATCH|일괄 처리당 행 수입니다. 기본값은 0으로, 데이터를 추출할 때 테이블에 있는 모든 행 수를 나타내거나 데이터를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 복사할 때 사용자 데이터 파일에 있는 모든 행 수를 나타냅니다. 1보다 작은 값을 지정하면 BCP_OPTION_BATCH는 기본값으로 다시 설정됩니다.|  
|BCP_OPTION_DELAYREADFMT|부울, 경우에는 true로 설정 하면 [ibcpsession:: Bcpreadfmt](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md) 에서 실행 시 읽습니다. False (기본값) 이면 ibcpsession:: Bcpreadfmt 즉시 되는 경우에 서식 파일을 읽습니다. 시퀀스 오류가 발생 합니다 **BCP_OPTION_DELAYREADFMT** 가 true 호출 ibcpsession:: Bcpcolumns 또는 ibcpsession:: Bcpcolfmt 합니다.<br /><br /> 호출 하는 경우에 시퀀스 오류가 발생 합니다 `IBCPSession::BCPControl(BCPDELAYREADFMT, (void *)FALSE))` 호출한 후 `IBCPSession::BCPControl(BCPDELAYREADFMT, (void *)TRUE)` 및 ibcpsession:: Bcpwritefmt 합니다.<br /><br /> 자세한 내용은 [Metadata Discovery](../../oledb/features/metadata-discovery.md)를 참조하십시오.|  
|BCP_OPTION_FILECP|*iValue* 인수 데이터 파일에 대 한 코드 페이지 번호를 포함 합니다. 1252나 850과 같은 코드 페이지 번호를 지정하거나 다음 값 중 하나를 지정할 수 있습니다.<br /><br /> BCP_FILECP_ACP: 파일의 데이터가 클라이언트의 Microsoft Windows® 코드 페이지에 있습니다.<br /><br /> BCP_FILECP_OEMCP: 파일의 데이터가 클라이언트의 OEM 코드 페이지에 있습니다(기본값).<br /><br /> BCP_FILECP_RAW: 파일의 데이터가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 코드 페이지에 있습니다.|  
|BCP_OPTION_FILEFMT|데이터 파일 형식의 버전 번호입니다. 이 값은 80([!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)]), 90([!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]), 100([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 또는 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]), 110([!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]) 또는 120([!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)])이 될 수 있습니다. 120 기본값입니다. 이 옵션은 이전 버전 서버에서 지원하는 형식으로 데이터를 가져오고 내보내는 데 유용합니다.  예를 들어 데이터를 가져오려면 텍스트 열에서 얻은 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 으로 서버는 **varchar (max)** 열에는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상의 서버 80을 지정 해야 합니다. 마찬가지로, 데이터를 내보낼 때 80을 지정 하는 경우는 **varchar (max)** 열에 저장 됩니다 텍스트 열에 저장 되는 것 처럼는 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 서식을 지정 하 고 텍스트 열으로 가져올 수는 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 서버입니다.|  
|BCP_OPTION_FIRST|복사할 파일이나 테이블의 첫 번째 데이터 행입니다. 기본값은 1입니다. 1보다 작은 값을 지정하면 이 옵션은 기본값으로 다시 설정됩니다.|  
|BCP_OPTION_FIRSTEX|BCP out 작업의 경우 데이터 파일에 복사할 데이터베이스 테이블의 첫 번째 행을 지정합니다.<br /><br /> BCP in 작업의 경우 데이터베이스 테이블에 복사할 데이터 파일의 첫 번째 행을 지정합니다.<br /><br /> *iValue* 매개 변수가 예상 값을 포함 하는 부호 있는 64 비트 정수 주소 여야 합니다. BCPFIRSTEX에 전달할 수 있는 최대값은 2^63-1입니다.|  
|BCP_OPTION_FMTXML|생성되는 서식 파일이 XML 형식이 되도록 지정하는 데 사용됩니다. 이 옵션은 기본적으로 해제되어 있으며 서식 파일은 텍스트 파일로 저장됩니다. XML 서식 파일은 더 높은 유연성을 제공하지만 몇 가지 제약 조건이 있습니다. 예를 들어 이전 서식 파일에서는 가능했던 작업인 필드의 접두사와 종결자를 동시에 지정할 수 없습니다.<br /><br /> 참고: XML 서식 파일은만 실행할 수 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 도구는 SQL Server 용 OLE DB 드라이버와 함께 설치 됩니다.|  
|BCP_OPTION_HINTS|*iValue* 인수는 와이드 문자 문자열 포인터를 포함 합니다. 주소가 지정된 문자열에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 대량 복사 처리 힌트나 결과 집합을 반환하는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 지정합니다. [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문이 둘 이상의 결과 집합을 반환하도록 지정된 경우 첫 번째 결과 집합 다음에 오는 결과 집합은 모두 무시됩니다.|  
|BCP_OPTION_KEEPIDENTITY|경우는 *iValue* 인수는 TRUE로 설정 된 경우이 옵션 지정 하는 대량 복사 방법에 대 한 제공 된 데이터 값을 삽입 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 열 identity 제약 조건을 사용 하 여 정의 합니다. 입력 파일은 ID 열에 해당하는 값을 제공해야 합니다. 설정되지 않은 경우 삽입된 행에 대해 새 ID 값이 생성됩니다. 파일에서 ID 열에 대한 데이터는 모두 무시됩니다.|  
|BCP_OPTION_KEEPNULLS|파일의 빈 데이터 값을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블에서 NULL 값으로 변환할지 여부를 지정합니다. 경우는 *iValue* 인수는 TRUE로 설정 되어 빈 값은 변환에서 NULL로는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블입니다. 기본적으로 빈 값은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블에서 열의 기본값(있는 경우)으로 변환됩니다.|  
|BCP_OPTION_LAST|복사할 마지막 행입니다. 기본값은 모든 행을 복사하는 것입니다. 1보다 작은 값을 지정하면 이 옵션은 기본값으로 다시 설정됩니다.|  
|BCP_OPTION_LASTEX|BCP out 작업의 경우 데이터 파일에 복사할 데이터베이스 테이블의 마지막 행을 지정합니다.<br /><br /> BCP in 작업의 경우 데이터베이스 테이블에 복사할 데이터 파일의 마지막 행을 지정합니다.<br /><br /> *iValue* 매개 변수가 예상 값을 포함 하는 부호 있는 64 비트 정수 주소 여야 합니다. BCPLASTEX에 전달할 수 있는 최대값은 2^63-1입니다.|  
|BCP_OPTION_MAXERRS|대량 복사 작업이 실패하기 전에 허용되는 오류 개수입니다. 기본값은 10입니다. 1보다 작은 값을 지정하면 이 옵션은 기본값으로 다시 설정됩니다. 대량 복사에는 최대 65,535개의 오류가 허용됩니다. 이 옵션을 65,535보다 큰 값으로 설정하려고 하는 경우 이 옵션은 65,535로 설정됩니다.|  
|BCP_OPTION_ROWCOUNT|현재(또는 마지막) BCP 작업에 의해 영향을 받는 행의 수를 반환합니다.|  
|BCP_OPTION_TEXTFILE|데이터 파일이 이진 파일이 아닌 텍스트 파일입니다. BCP는 데이터 파일의 첫 번째 2바이트에서 유니코드 바이트 표식을 확인하여 텍스트 파일이 유니코드인지 여부를 검사합니다.|  
|BCP_OPTION_UNICODEFILE|TRUE로 설정된 경우 이 옵션은 입력 파일이 유니코드 파일 형식이 되도록 지정합니다.|  
  
## <a name="arguments"></a>인수  
 *eOption*[in]  
 위의 주의 섹션에 나열된 옵션 중 하나를 설정합니다.  
  
 *iValue*[in]  
 지정 된 값 *eOption*합니다. *iValue* 인수는 64 비트 값으로 추가로 확장할 수 있도록 void 포인터로 캐스팅 하는 정수 값입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 메서드가 성공했습니다.  
  
 E_FAIL  
 공급자 관련 오류가 발생 했습니다. 자세한 내용은 사용 하 여는 [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 인터페이스입니다.  
  
 E_UNEXPECTED  
 예기치 않은 메서드가 호출되었습니다. 예를 들어는 [ibcpsession:: Bcpinit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) 이 함수를 호출 하기 전에 메서드를 호출 하지 않았습니다.  
  
 E_OUTOFMEMORY  
 메모리 부족 오류가 발생했습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [대량 복사 작업 수행](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
