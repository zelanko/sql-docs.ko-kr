---
title: SQLFreeHandle | Microsoft 문서
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFreeHandle function
ms.assetid: d374e5c8-ed35-43bf-8dd6-c37e38d9b5f1
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: fe6e241e1596fd81cfc4cc284088a1ceacc6cfd7
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39559083"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  수동 커밋 모드에서 트랜잭션이 열려 있을 때 문 핸들에 대해 **SQLFreeHandle** 을 호출하면 보류 중인 변경 내용이 데이터베이스에 롤백됩니다. 문 핸들에 대해 **SQLFreeHandle** 을 호출하면 항상 열려 있는 모든 커서가 닫히고 보류 중인 결과가 삭제되어 문 핸들에 연결된 모든 리소스가 해제됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLFreeHandle 함수](http://go.microsoft.com/fwlink/?LinkId=59345)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
