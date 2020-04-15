---
title: 네이티브 오류 번호 | 마이크로 소프트 문서
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0b5572ee784f47b0444e1d825de1b6dd53db8066
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291611"
---
# <a name="native-error-numbers"></a>원시 오류 번호
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  데이터 원본에서 발생하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]오류(반환됨)의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경우 네이티브 클라이언트 ODBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 반환되는 기본 오류 번호를 반환합니다. 드라이버에서 검색된 오류의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경우 네이티브 클라이언트 ODBC 드라이버는 기본 오류 번호 0을 반환합니다. 기본 오류 번호 목록에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 **마스터** 데이터베이스에서 **sysmessages** 시스템 테이블의 오류 열을 참조하십시오.  
  
 상태 오류 코드에 대한 자세한 내용은 [SQLSTATE &#40;ODBC 오류 코드&#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md)를 참조하십시오. Net-Library에서 반환된 오류의 경우 원시 오류 번호는 기본 네트워크 소프트웨어에서 가져온 것입니다.  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 메시지 처리](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
