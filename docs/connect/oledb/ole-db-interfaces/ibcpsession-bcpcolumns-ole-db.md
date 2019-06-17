---
title: 'Ibcpsession:: Bcpcolumns (OLE DB) | Microsoft Docs'
description: IBCPSession::BCPColumns(OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.technology: connectivity
ms.topic: reference
apiname:
- IBCPSession::BCPColumns (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPColumns method
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 0be5ef8671e327601314061902b804decc9ecc7a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66790947"
---
# <a name="ibcpsessionbcpcolumns-ole-db"></a>IBCPSession::BCPColumns(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블의 열에 바인딩될 필드의 개수를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT BCPColumns(   
      DBCOUNTITEM nColumns);  
```  
  
## <a name="remarks"></a>Remarks  
 이 메서드는 [IBCPSession::BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) 를 내부적으로 호출하여 필드 데이터의 기본값을 설정합니다. 이러한 기본값은 [IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)를 통해 테이블 이름을 지정할 때 공급자가 내부적으로 검색하는 SQL Server 열 정보에서 가져옵니다.  
  
> [!NOTE]  
>  이 메서드는 유효한 파일 이름을 사용하여 **BCPInit** 를 호출한 후에만 호출할 수 있습니다.  
  
 이 메서드는 기본값과는 다른 사용자 파일 형식을 사용하려는 경우에만 호출해야 합니다. 기본 사용자 파일 형식에 대한 자세한 설명을 보려면 **BCPInit** 메서드를 참조하십시오.  
  
 사용자 정의 파일 형식을 완전하게 정의하려면 **BCPColumns** 메서드를 호출한 후에 사용자 파일의 각 열에 대해 **BCPColFmt** 메서드를 반드시 호출해야 합니다.  
  
## <a name="arguments"></a>인수  
 *nColumns*[in]  
 사용자 파일에 포함된 총 필드 수입니다. 사용자 파일의 데이터를 SQL Server 테이블에 대량 복사하면서 사용자 파일의 필드 일부만 복사하려는 경우에도 *nColumns* 인수에 사용자 파일 필드의 총 개수를 설정해야 합니다. 이 경우 건너뛴 필드를 **BCPColFmt**를 통해 지정할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 메서드가 성공했습니다.  
  
 E_FAIL  
 공급자 관련 오류가 발생했습니다. 자세한 내용을 보려면 [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 인터페이스를 사용하십시오.  
  
 E_UNEXPECTED  
 예기치 않은 메서드가 호출되었습니다. 예를 들어 이 메서드를 호출하기 전에 **BCPInit** 메서드를 호출하지 않았습니다. 대량 복사 작업에 이 메서드를 두 번 이상 호출한 경우에도 발생합니다.  
  
 E_OUTOFMEMORY  
 메모리 부족 오류가 발생했습니다.  
  
## <a name="see-also"></a>참고 항목  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [대량 복사 작업 수행](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
