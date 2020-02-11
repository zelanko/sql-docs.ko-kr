---
title: 원시 오류 번호 | Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b1bc1f9383ab615a24b0506b86cf0ec5e37b6c74
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73783401"
---
# <a name="native-error-numbers"></a>원시 오류 번호
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  에서 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]하는 데이터 원본에서 발생 하는 오류의 경우 NATIVE Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 드라이버는에 의해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 된 원시 오류 번호를 반환 합니다. 드라이버에서 검색 된 오류의 경우 native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 드라이버는 원시 오류 번호 0을 반환 합니다. 네이티브 오류 번호 목록에 대 한 자세한 내용은의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **master** 데이터베이스에서 **sysmessages** 시스템 테이블의 error 열을 참조 하십시오.  
  
 상태 오류 코드에 대 한 자세한 내용은 [SQLSTATE &#40;ODBC 오류 코드&#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md)를 참조 하세요. Net-Library에서 반환된 오류의 경우 원시 오류 번호는 기본 네트워크 소프트웨어에서 가져온 것입니다.  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 메시지 처리](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
