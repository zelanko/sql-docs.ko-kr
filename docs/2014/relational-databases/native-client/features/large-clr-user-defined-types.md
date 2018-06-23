---
title: 큰 CLR 사용자 정의 형식 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- large CLR user-defined types
ms.assetid: b65eb61d-ccf6-49c0-98e7-9a4ef4b2f790
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a85d6672a7346b3962dca8d3826306defaa76099
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089302"
---
# <a name="large-clr-user-defined-types"></a>큰 CLR 사용자 정의 형식
  SQL Server 2005에서는 CLR(공용 언어 런타임)에서의 UDT(사용자 정의 형식) 크기가 8,000바이트로 제한되었습니다. [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 이상 버전에서는 이 제한이 더 이상 적용되지 않습니다. 이제 CLR UDT가 LOB(Large Object) 형식과 비슷하게 처리됩니다. 즉, 8,000바이트보다 작거나 같은 UDT는 SQL Server 2005에서와 동일하게 처리되나 이보다 큰 UDT도 지원되며 이 경우 크기가 "제한 없음"으로 보고됩니다.  
  
 자세한 내용은 참조 [Large CLR User-Defined 형식 &#40;OLE DB&#41; ](../ole-db/large-clr-user-defined-types-ole-db.md) 및 [Large CLR User-Defined 형식 &#40;ODBC&#41;](../odbc/large-clr-user-defined-types-odbc.md)합니다.  
  
## <a name="use-cases"></a>사용 사례  
 ODBC의 경우 UDT 값을 실행 시 데이터 매개 변수로 조각으로 나누어 보낼 수 있는 기능이 큰 UDT에 대한 지원에 포함되었습니다. 이 SQLPutData를 사용 하 여 수행 됩니다.  
  
 큰 Udt에 대 한 OLE DB 지원에 대 한 ISequentialStream 바인딩을 사용 하 여 스트림 UDT 값을 서버에서 하는 기능이 포함 됩니다.  
  
 8,000바이트보다 작거나 같은 UDT는 SQL Server 2005에서와 동일하게 처리됩니다. OLE DB에 대 한 ISequentialStream 바인딩을 사용 하 여 작은 Udt를 계속 스트리밍할 수 있습니다.  
  
 네이티브 코드가 CLR UDT의 내용을 이해해야 하지만 관리되는 개체를 인스턴스화할 필요는 없는 경우가 있습니다. 이 경우 사용자 지정 직렬화를 사용하여 서버의 UDT 값을 클라이언트의 잘 알려진 형식으로 변환할 수 있습니다.  
  
 데이터 액세스 코드가 이미 있는 응용 프로그램의 경우 네이티브 API를 통해 UDT를 검색한 후 이를 혼합 모드 응용 프로그램에서 C++ CLI interop을 사용하여 인스턴스화하는 방법으로 클라이언트에서 CLR UDT 동작을 이용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client 기능](sql-server-native-client-features.md)  
  
  