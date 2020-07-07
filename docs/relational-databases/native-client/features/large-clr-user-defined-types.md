---
title: 큰 CLR 사용자 정의 형식 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- large CLR user-defined types
ms.assetid: b65eb61d-ccf6-49c0-98e7-9a4ef4b2f790
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c927a2227b5efaa05db070861b84816a23df6f4b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009077"
---
# <a name="large-clr-user-defined-types"></a>큰 CLR 사용자 정의 형식
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  SQL Server 2005에서는 CLR(공용 언어 런타임)에서의 UDT(사용자 정의 형식) 크기가 8,000바이트로 제한되었습니다. [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 이상 버전에서는 이 제한이 더 이상 적용되지 않습니다. 이제 CLR UDT가 LOB(Large Object) 형식과 비슷하게 처리됩니다. 즉, 8,000바이트보다 작거나 같은 UDT는 SQL Server 2005에서와 동일하게 처리되나 이보다 큰 UDT도 지원되며 이 경우 크기가 "제한 없음"으로 보고됩니다.  
  
 자세한 내용은 [ODBC&#41;&#40;](../../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md) [&#41;OLE DB &#40;크고](../../../relational-databases/native-client/ole-db/large-clr-user-defined-types-ole-db.md) clr 사용자 정의 형식을 참조 하세요.  
  
## <a name="use-cases"></a>사용 사례  
 ODBC의 경우 UDT 값을 실행 시 데이터 매개 변수로 조각으로 나누어 보낼 수 있는 기능이 큰 UDT에 대한 지원에 포함되었습니다. SQLPutData를 사용 하 여이 작업을 수행 합니다.  
  
 OLE DB의 경우 ISequentialStream 바인딩을 통해 UDT 값을 서버로 스트리밍하거나 서버에서 스트리밍하는 기능이 큰 UDT에 대한 지원에 포함되었습니다.  
  
 8,000바이트보다 작거나 같은 UDT는 SQL Server 2005에서와 동일하게 처리됩니다. OLE DB의 경우 작은 UDT는 ISequentialStream 바인딩을 사용하여 이전처럼 스트리밍할 수 있습니다.  
  
 네이티브 코드가 CLR UDT의 내용을 이해해야 하지만 관리되는 개체를 인스턴스화할 필요는 없는 경우가 있습니다. 이 경우 사용자 지정 직렬화를 사용하여 서버의 UDT 값을 클라이언트의 잘 알려진 형식으로 변환할 수 있습니다.  
  
 데이터 액세스 코드가 이미 있는 애플리케이션의 경우 네이티브 API를 통해 UDT를 검색한 후 이를 혼합 모드 애플리케이션에서 C++ CLI interop을 사용하여 인스턴스화하는 방법으로 클라이언트에서 CLR UDT 동작을 이용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client 기능](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
