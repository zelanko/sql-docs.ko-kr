---
title: 'Ibcpsession:: Bcpinit (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IBCPSession::BCPInit (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPInit method
ms.assetid: 583096d7-da34-49be-87fd-31210aac81aa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fc9983cea171eb78f4b3b4f2b9c5cb9f31ecb2d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63033598"
---
# <a name="ibcpsessionbcpinit-ole-db"></a>IBCPSession::BCPInit(OLE DB)
  대량 복사 구조를 초기화하고, 일부 오류 검사를 수행하고, 데이터 및 서식 파일 이름이 올바른지 확인한 다음 파일을 엽니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT BCPInit(   
const wchar_t *pwszTable,  
const wchar_t *pwszDataFile,  
const wchar_t *pwszErrorFile,  
inteDirection);  
```  
  
## <a name="remarks"></a>Remarks  
 **BCPInit** 메서드는 다른 대량 복사 메서드를 호출하기 전에 호출해야 합니다. **BCPInit** 메서드는 워크스테이션과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 간의 데이터 대량 복사에 필요한 초기화를 수행합니다.  
  
 **BCPInit** 메서드는 데이터 파일이 아니라 데이터베이스 원본 또는 대상 테이블의 구조를 검사합니다. 또한 데이터베이스 테이블, 뷰 또는 SELECT 결과 집합에 있는 각 열을 기반으로 데이터 파일의 데이터 형식 값을 지정합니다. 이 지정에는 각 열의 데이터 형식, 데이터에 길이 또는 Null 표시자 및 종결자 바이트 문자열이 있는지 여부, 고정 길이 데이터 형식의 길이가 포함됩니다. **BCPInit** 메서드는 이러한 값을 다음과 같이 설정합니다.  
  
-   지정되는 데이터 형식은 데이터베이스 테이블, 뷰 또는 SELECT 결과 집합에 있는 열의 데이터 형식입니다. 데이터 형식을 열거 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 데이터 형식에 지정 된 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 헤더 파일 (sqlncli.h). 이 값은 BCP_TYPE_XXX 패턴을 사용합니다. 데이터는 해당 컴퓨터 형식으로 표현됩니다. 즉, integer 데이터 형식의 열에서 가져온 데이터는 데이터 파일을 만든 컴퓨터에 따라 Big Endian 또는 Little Endian인 4바이트 시퀀스로 표현됩니다.  
  
-   데이터베이스 데이터 형식의 길이가 고정된 경우 데이터 파일 데이터의 길이도 고정됩니다. 데이터를 처리하는 대량 복사 메서드(예: [IBCPSession::BCPExec](ibcpsession-bcpexec-ole-db.md))는 데이터 파일에 있는 데이터의 길이가 데이터베이스 테이블, 뷰 또는 SELECT 열 목록에 지정된 데이터의 길이와 동일할 것이라 예상하고 데이터 행을 구문 분석합니다. 예를 들어 `char(13)`로 정의된 데이터베이스 열의 데이터에서 파일의 각 데이터 행은 13자로 표현되어야 합니다. 데이터베이스 열이 Null 값을 허용하는 경우에는 고정 길이 데이터 앞에 Null 표시자를 붙일 수 있습니다.  
  
-   데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 복사하는 경우 데이터 파일에 데이터베이스 테이블의 각 열에 대한 데이터가 있어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터를 복사하는 경우 데이터베이스 테이블, 뷰 또는 SELECT 결과 집합에 있는 모든 열의 데이터가 데이터 파일로 복사됩니다.  
  
-   데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 복사하는 경우 데이터 파일에 있는 열의 서수 위치가 데이터베이스 테이블에 있는 열의 서수 위치와 같아야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터를 복사하는 경우 **BCPExec** 메서드는 데이터베이스 테이블에 있는 열의 서수 위치를 기반으로 데이터를 배치합니다.  
  
-   데이터베이스 데이터 형식의 길이가 가변적(예: `varbinary(22)`)이거나 데이터베이스 열이 Null 값을 포함할 수 있는 경우 데이터 파일의 데이터 앞에 길이/Null 표시자가 옵니다. 표시자의 길이는 데이터 형식 및 대량 복사 버전에 따라 다릅니다. [IBCPSession::BCPControl](ibcpsession-bcpcontrol-ole-db.md) 메서드 옵션 BCP_OPTION_FILEFMT는 데이터에 있는 표시자의 너비가 예상보다 짧은 경우를 표시하여 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하는 서버와 이전 대량 복사 데이터 파일 간의 호환성을 제공합니다.  
  
> [!NOTE]  
>  데이터 파일에 대해 지정된 데이터 형식 값을 변경하려면 [IBCPSession::BCPColumns](ibcpsession-bcpcolumns-ole-db.md) 및 [IBCPSession::BCPColFmt](ibcpsession-bcpcolfmt-ole-db.md) 메서드를 사용합니다.  
  
 데이터베이스 옵션 **select into/bulkcopy**를 설정하면 인덱스가 없는 테이블에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로의 대량 복사를 최적화할 수 있습니다.  
  
## <a name="arguments"></a>인수  
 *pwszTable*[in]  
 복사의 원본 또는 대상이 될 데이터베이스 테이블의 이름입니다. 이 이름은 데이터베이스 이름 또는 소유자 이름을 포함할 수 있습니다. 예를 들면 "pubs.username.titles", "pubs..titles", "username.titles"와 같습니다.  
  
 eDirection 인수가 BCP_DIRECTION_OUT으로 설정된 경우 pwszTable 인수는 데이터베이스 뷰의 이름일 수 있습니다.  
  
 eDirection 인수를 BCP_DIRECTION_OUT으로 설정하고 **BCPControl** 메서드가 호출되기 전에 **BCPExec** 메서드를 사용하여 SELECT 문을 지정한 경우 *pwszTable* 인수를 NULL로 설정해야 합니다.  
  
 *pwszDataFile*[in]  
 복사의 원본 또는 대상이 될 사용자 파일의 이름입니다.  
  
 *pwszErrorFile*[in]  
 진행 메시지, 오류 메시지 및 어떤 이유로든 사용자 파일에서 테이블로 복사하지 못한 모든 행의 복사본으로 채워질 오류 파일의 이름입니다. 경우는 *pwszErrorFile* 인수를 NULL로 설정, 없음 오류 파일이 사용 됩니다.  
  
 *eDirection*[in]  
 복사 작업의 방향(BCP_DIRECTION_IN 또는 BCP_DIRECTION _OUT)입니다. BCP_DIRECTION _IN은 사용자 파일에서 데이터베이스 테이블로의 복사본을 나타내고, BCP_DIRECTION _OUT은 데이터베이스 테이블에서 사용자 파일로의 복사본을 나타냅니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 메서드가 성공했습니다.  
  
 E_FAIL  
 공급자 관련 오류가 발생했습니다. 자세한 내용을 보려면 [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) 인터페이스를 사용하세요.  
  
 E_OUTOFMEMORY  
 메모리 부족 오류가 발생했습니다.  
  
 E_INVALIDARG  
 하나 이상의 인수가 잘못 지정되었습니다. 예를 들어 잘못된 파일 이름이 제공되었습니다.  
  
## <a name="see-also"></a>관련 항목  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [대량 복사 작업 수행](../native-client/features/performing-bulk-copy-operations.md)  
  
  
