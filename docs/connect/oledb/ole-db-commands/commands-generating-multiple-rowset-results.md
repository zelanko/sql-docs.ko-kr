---
title: 여러 행 집합 결과 생성 하는 명령 | Microsoft Docs
description: 여러 행 집합 결과 생성 하는 명령
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- OLE DB Driver for SQL Server, commands
- OLE DB Driver for SQL Server, multiple rowsets
- commands [OLE DB]
- multiple-rowset results
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e056aefaf23fc046d8b6760b1c9ba1c7ace52848
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="commands-generating-multiple-rowset-results"></a>여러 행 집합 결과를 생성하는 명령
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB Driver for SQL Server에서 여러 행 집합을 반환할 수 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 문. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 문은 다음과 같은 조건에서 여러 행 집합 결과를 반환합니다.  
  
-   일괄 처리되는 SQL 문이 단일 명령으로 제출된 경우  
  
-   저장 프로시저가 SQL 문의 일괄 처리를 구현하는 경우  
  
## <a name="batches"></a>일괄 처리  
 OLE DB Driver for SQL Server는 SQL 문의 일괄 처리 구분 기호로 세미콜론을 인식합니다.  
  
```  
WCHAR*       wSQLString = L"SELECT * FROM Categories; "  
                          L"SELECT * FROM Products";  
```  
  
 여러 SQL 문을 하나의 일괄 처리로 보내는 것이 각 SQL 문을 별도로 실행하는 것보다 효율적입니다. 하나의 일괄 처리를 보내는 경우 클라이언트에서 서버로의 네트워크 왕복 수가 줄어듭니다.  
  
## <a name="stored-procedures"></a>저장 프로시저  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 저장 프로시저의 각 문에 대해 하나의 결과 집합을 반환하므로 대부분의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 저장 프로시저는 여러 결과 집합을 반환합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [IMultipleResults를 사용 하 여 여러 결과 집합 처리](../../oledb/ole-db-commands/using-imultipleresults-to-process-multiple-result-sets.md)  
  
## <a name="see-also"></a>관련 항목:  
 [도구](../../oledb/ole-db-commands/commands.md)  
  
  
