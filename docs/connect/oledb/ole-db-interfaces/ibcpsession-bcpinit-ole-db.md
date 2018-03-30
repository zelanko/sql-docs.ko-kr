---
title: 'Ibcpsession:: Bcpinit (OLE DB) | Microsoft Docs'
description: IBCPSession::BCPInit(OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
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
- IBCPSession::BCPInit (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPInit method
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 275dd24ac49aeef761ce86c3ab0c072b23ee7fe1
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2018
---
# <a name="ibcpsessionbcpinit-ole-db"></a>IBCPSession::BCPInit(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  대량 복사 구조를 초기화하고, 일부 오류 검사를 수행하고, 데이터 및 서식 파일 이름이 올바른지 확인한 다음 파일을 엽니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT BCPInit(   
      const wchar_t *pwszTable,  
      const wchar_t *pwszDataFile,  
      const wchar_t *pwszErrorFile,  
      int eDirection);  
```  
  
## <a name="remarks"></a>주의  
 **BCPInit** 다른 대량 복사 메서드 전에 메서드를 호출 해야 합니다. **BCPInit** 워크스테이션 간의 데이터 대량 복사에 필요한 초기화를 수행 하는 메서드 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.  
  
 **BCPInit** 메서드는 데이터베이스 원본 또는 대상 테이블에 데이터 파일이 아니라의 구조를 검사 합니다. 또한 데이터베이스 테이블, 뷰 또는 SELECT 결과 집합에 있는 각 열을 기반으로 데이터 파일의 데이터 형식 값을 지정합니다. 이 지정에는 각 열의 데이터 형식, 데이터에 길이 또는 Null 표시자 및 종결자 바이트 문자열이 있는지 여부, 고정 길이 데이터 형식의 길이가 포함됩니다. **BCPInit** 메서드 이러한 값을 다음과 같이 설정 합니다.  
  
-   지정되는 데이터 형식은 데이터베이스 테이블, 뷰 또는 SELECT 결과 집합에 있는 열의 데이터 형식입니다. 데이터 형식을 열거 하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB 드라이버에서 SQL Server 헤더 파일 (msoledbsql.h)에 대해 지정 된 네이티브 데이터 형식입니다. 이 값은 BCP_TYPE_XXX 패턴을 사용합니다. 데이터는 해당 컴퓨터 형식으로 표현됩니다. 즉, integer 데이터 형식의 열에서 가져온 데이터는 데이터 파일을 만든 컴퓨터에 따라 Big Endian 또는 Little Endian인 4바이트 시퀀스로 표현됩니다.  
  
-   데이터베이스 데이터 형식의 길이가 고정된 경우 데이터 파일 데이터의 길이도 고정됩니다. 데이터를 처리 하는 대량 복사 메서드 (예를 들어 [ibcpsession:: Bcpexec](../../oledb/ole-db-interfaces/ibcpsession-bcpexec-ole-db.md))와 동일 하 게 데이터베이스 테이블, 뷰 또는 SELECT 열에 지정 된 데이터의 길이 데이터 파일에 있는 데이터의 길이 예상 하는 데이터 행을 구문 분석 목록입니다. 예를 들어 `char(13)`로 정의된 데이터베이스 열의 데이터에서 파일의 각 데이터 행은 13자로 표현되어야 합니다. 데이터베이스 열이 Null 값을 허용하는 경우에는 고정 길이 데이터 앞에 Null 표시자를 붙일 수 있습니다.  
  
-   데이터를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 복사하는 경우 데이터 파일에 데이터베이스 테이블의 각 열에 대한 데이터가 있어야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 데이터를 복사하는 경우 데이터베이스 테이블, 뷰 또는 SELECT 결과 집합에 있는 모든 열의 데이터가 데이터 파일로 복사됩니다.  
  
-   데이터를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 복사하는 경우 데이터 파일에 있는 열의 서수 위치가 데이터베이스 테이블에 있는 열의 서수 위치와 같아야 합니다. 데이터를 복사 하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], **BCPExec** 메서드는 데이터베이스 테이블의 열 서 수 위치에 따라 데이터를 배치 합니다.  
  
-   데이터베이스 데이터 형식의 길이가 가변적(예: `varbinary(22)`)이거나 데이터베이스 열이 Null 값을 포함할 수 있는 경우 데이터 파일의 데이터 앞에 길이/Null 표시자가 옵니다. 표시자의 길이는 데이터 형식 및 대량 복사 버전에 따라 다릅니다. [ibcpsession:: Bcpcontrol](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md) 이전 대량 복사 데이터 파일 및 이후 버전의를 실행 하는 서버 간의 호환성을 제공 하는 메서드 옵션 BCP_OPTION_FILEFMT [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 시기를 지정 하 여 표시기의 너비는 데이터는 예상 보다입니다.  
  
> [!NOTE]  
>  데이터 파일에 대해 지정 된 데이터 형식 값을 변경 하려면 사용 된 [ibcpsession:: Bcpcolumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) 및 [ibcpsession:: Bcpcolfmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) 메서드.  
  
 대량 복사를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스 옵션을 설정 하 여 인덱스를 포함 하지 않는 테이블에 대 한 최적화 될 **에 선택 / bulkcopy**합니다.  
  
## <a name="arguments"></a>인수  
 *pwszTable*[in]  
 복사의 원본 또는 대상이 될 데이터베이스 테이블의 이름입니다. 이 이름은 데이터베이스 이름 또는 소유자 이름을 포함할 수 있습니다. 예를 들면 "pubs.username.titles", "pubs..titles", "username.titles"와 같습니다.  
  
 eDirection 인수가 BCP_DIRECTION_OUT으로 설정된 경우 pwszTable 인수는 데이터베이스 뷰의 이름일 수 있습니다.  
  
 EDirection 인수가 BCP_DIRECTION_OUT로 설정 된 SELECT 문을 사용 하 여 지정 된 경우는 **BCPControl** 먼저 메서드는 **BCPExec** 메서드가 호출 되는 *pwszTable*인수를 NULL로 설정 해야 합니다.  
  
 *pwszDataFile*[in]  
 복사의 원본 또는 대상이 될 사용자 파일의 이름입니다.  
  
 *pwszErrorFile*[in]  
 진행 메시지, 오류 메시지 및 어떤 이유로든 사용자 파일에서 테이블로 복사하지 못한 모든 행의 복사본으로 채워질 오류 파일의 이름입니다. 경우는 *pwszErrorFile* 인수는 NULL로 설정 되어, 없음 오류 파일을 사용 합니다.  
  
 *eDirection*[in]  
 복사 작업의 방향(BCP_DIRECTION_IN 또는 BCP_DIRECTION _OUT)입니다. BCP_DIRECTION _IN은 사용자 파일에서 데이터베이스 테이블로의 복사본을 나타내고, BCP_DIRECTION _OUT은 데이터베이스 테이블에서 사용자 파일로의 복사본을 나타냅니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 메서드가 성공했습니다.  
  
 E_FAIL  
 공급자 관련 오류가 발생 했습니다. '에 대 한 자세한 정보를 사용 하 여는 [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 인터페이스입니다.  
  
 E_OUTOFMEMORY  
 메모리 부족 오류가 발생했습니다.  
  
 E_INVALIDARG  
 하나 이상의 인수가 잘못 지정되었습니다. 예를 들어 잘못된 파일 이름이 제공되었습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [대량 복사 작업 수행](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
