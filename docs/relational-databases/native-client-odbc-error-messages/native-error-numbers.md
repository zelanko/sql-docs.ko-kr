---
title: 원시 오류 번호 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, native error numbers
- SQL Server Native Client ODBC driver, errors
- native error numbers [SQL Server Native Client]
- messages [ODBC], native error numbers
- errors [ODBC], native error numbers
ms.assetid: 77cbc826-f47f-4803-8e7a-223d6df069b1
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c1a66e011ee5716f92d8b0257ed8424c86244139
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47659161"
---
# <a name="native-error-numbers"></a>원시 오류 번호
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  데이터 원본에서 발생 하는 오류에 대 한 (반환한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에서 반환 된 원시 오류 번호를 반환 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 드라이버에 의해 발견 된 오류에 대 한는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 원시 오류 번호 0 반환 합니다. 원시 오류 번호 목록에 대 한 자세한 내용은 오류 열을 참조 합니다 **sysmessages** 시스템 테이블에는 **마스터** 데이터베이스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]입니다.  
  
 상태 오류 코드에 대 한 자세한 내용은 [SQLSTATE &#40;ODBC 오류 코드&#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md)합니다. Net-Library에서 반환된 오류의 경우 원시 오류 번호는 기본 네트워크 소프트웨어에서 가져온 것입니다.  
  
## <a name="see-also"></a>관련 항목  
 [오류 및 메시지 처리](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
