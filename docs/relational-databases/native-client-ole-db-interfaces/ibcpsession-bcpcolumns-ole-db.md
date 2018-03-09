---
title: 'Ibcpsession:: Bcpcolumns (OLE DB) | Microsoft Docs'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-interfaces
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- IBCPSession::BCPColumns (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPColumns method
ms.assetid: c338abe8-9e30-4853-a7c6-b1a6c00095e1
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4e80461dc1b77a648b87f79415849d492980e16b
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="ibcpsessionbcpcolumns-ole-db"></a>IBCPSession::BCPColumns(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 열에 바인딩될 필드의 개수를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT BCPColumns(   
      DBCOUNTITEM nColumns);  
```  
  
## <a name="remarks"></a>주의  
 내부적으로 호출 [ibcpsession:: Bcpcolfmt](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) 필드 데이터에 대 한 기본 값을 설정 합니다. 이 값은 기본값을 통해 테이블 이름을 지정할 때 공급자가 내부적으로 검색 하는 SQL Server 열 정보에서 가져오는 [ibcpsession:: Bcpinit](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)합니다.  
  
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
 공급자 관련 오류가 발생 했습니다. 자세한 내용은 사용 하 여는 [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 인터페이스입니다.  
  
 E_UNEXPECTED  
 예기치 않은 메서드가 호출되었습니다. 예를 들어 이 메서드를 호출하기 전에 **BCPInit** 메서드를 호출하지 않았습니다. 대량 복사 작업에 이 메서드를 두 번 이상 호출한 경우에도 발생합니다.  
  
 E_OUTOFMEMORY  
 메모리 부족 오류가 발생했습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [IBCPSession &#40; OLE db&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [대량 복사 작업 수행](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
  
  
