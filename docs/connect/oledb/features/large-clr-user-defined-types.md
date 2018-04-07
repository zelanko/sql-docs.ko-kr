---
title: 큰 CLR 사용자 정의 형식 | Microsoft Docs
description: OLE DB Driver for SQL Server에서에서 큰 CLR 사용자 정의 형식
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- large CLR user-defined types
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b15b2992cb82da368a7aa0786a37e23b6c100cf9
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="large-clr-user-defined-types"></a>큰 CLR 사용자 정의 형식
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server 2005에서는 CLR(공용 언어 런타임)에서의 UDT(사용자 정의 형식) 크기가 8,000바이트로 제한되었습니다. [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 이상 버전에서는 이 제한이 더 이상 적용되지 않습니다. 이제 CLR UDT가 LOB(Large Object) 형식과 비슷하게 처리됩니다. 즉, 8,000바이트보다 작거나 같은 UDT는 SQL Server 2005에서와 동일하게 처리되나 이보다 큰 UDT도 지원되며 이 경우 크기가 "제한 없음"으로 보고됩니다.  
  
 자세한 내용은 참조 [Large CLR User-Defined 형식 &#40;OLE DB&#41;](../../oledb/ole-db/large-clr-user-defined-types-ole-db.md)합니다.  
  
## <a name="use-cases"></a>사용 사례   
  
 큰 Udt에 대 한 OLE DB 지원에 대 한 ISequentialStream 바인딩을 사용 하 여 스트림 UDT 값을 서버에서 하는 기능이 포함 됩니다.  
  
 8,000바이트보다 작거나 같은 UDT는 SQL Server 2005에서와 동일하게 처리됩니다. OLE DB에 대 한 ISequentialStream 바인딩을 사용 하 여 작은 Udt를 계속 스트리밍할 수 있습니다.  
  
 네이티브 코드가 CLR UDT의 내용을 이해해야 하지만 관리되는 개체를 인스턴스화할 필요는 없는 경우가 있습니다. 이 경우 사용자 지정 직렬화를 사용하여 서버의 UDT 값을 클라이언트의 잘 알려진 형식으로 변환할 수 있습니다.  
  
 데이터 액세스 코드가 이미 있는 응용 프로그램의 경우 네이티브 API를 통해 UDT를 검색한 후 이를 혼합 모드 응용 프로그램에서 C++ CLI interop을 사용하여 인스턴스화하는 방법으로 클라이언트에서 CLR UDT 동작을 이용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)    
  
  
