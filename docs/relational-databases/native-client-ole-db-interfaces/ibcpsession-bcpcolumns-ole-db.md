---
description: 'IBCPSession:: BCPColumns (Native Client OLE DB 공급자)'
title: 'IBCPSession:: BCPColumns (Native Client OLE DB 공급자) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- IBCPSession::BCPColumns (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPColumns method
ms.assetid: c338abe8-9e30-4853-a7c6-b1a6c00095e1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0e912bf8e1a7ef3d9bf620799f73ec120eca51bb
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97476084"
---
# <a name="ibcpsessionbcpcolumns-native-client-ole-db-provider"></a>IBCPSession:: BCPColumns (Native Client OLE DB 공급자)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 열에 바인딩될 필드의 개수를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT BCPColumns(   
      DBCOUNTITEM nColumns);  
```  
  
## <a name="remarks"></a>설명  
 이 메서드는 [IBCPSession::BCPColFmt](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) 를 내부적으로 호출하여 필드 데이터의 기본값을 설정합니다. 이러한 기본값은 [IBCPSession::BCPInit](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)를 통해 테이블 이름을 지정할 때 공급자가 내부적으로 검색하는 SQL Server 열 정보에서 가져옵니다.  
  
> [!NOTE]  
>  이 메서드는 유효한 파일 이름을 사용하여 **BCPInit** 를 호출한 후에만 호출할 수 있습니다.  
  
 이 메서드는 기본값과는 다른 사용자 파일 형식을 사용하려는 경우에만 호출해야 합니다. 기본 사용자 파일 형식에 대한 자세한 설명을 보려면 **BCPInit** 메서드를 참조하십시오.  
  
 사용자 정의 파일 형식을 완전하게 정의하려면 **BCPColumns** 메서드를 호출한 후에 사용자 파일의 각 열에 대해 **BCPColFmt** 메서드를 반드시 호출해야 합니다.  
  
## <a name="arguments"></a>인수  
 *nColumns*[in]  
 사용자 파일에 포함된 총 필드 수입니다. 사용자 파일의 데이터를 SQL Server 테이블에 대량 복사하면서 사용자 파일의 필드 일부만 복사하려는 경우에도 *nColumns* 인수에 사용자 파일 필드의 총 개수를 설정해야 합니다. 이 경우 건너뛴 필드를 **BCPColFmt** 를 통해 지정할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 메서드가 성공했습니다.  
  
 E_FAIL  
 공급자 관련 오류가 발생했습니다. 자세한 내용을 보려면 [ISQLServerErrorInfo](isqlservererrorinfo-geterrorinfo-ole-db.md) 인터페이스를 사용하세요.  
  
 E_UNEXPECTED  
 예기치 않은 메서드가 호출되었습니다. 예를 들어 이 메서드를 호출하기 전에 **BCPInit** 메서드를 호출하지 않았습니다. 대량 복사 작업에 이 메서드를 두 번 이상 호출한 경우에도 발생합니다.  
  
 E_OUTOFMEMORY  
 메모리 부족 오류가 발생했습니다.  
  
## <a name="see-also"></a>참고 항목  
 [IBCPSession &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [대량 복사 작업 수행](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
  
