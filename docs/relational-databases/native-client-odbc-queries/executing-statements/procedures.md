---
title: 프로시저 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC]
- stored procedures [ODBC], about ODBC stored procedures
- ODBC applications, statements
- statements [ODBC], stored procedures
- ODBC applications, stored procedures
ms.assetid: c64d5f3a-376b-48ef-84f3-b6148ac8600a
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 66db10c8ac64fee4e6e9ccbc405ab5b804adb32a
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779518"
---
# <a name="procedures"></a>절차
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  저장 프로시저란 하나 이상의 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 포함하는 미리 컴파일된 실행 개체입니다. 저장 프로시저는 입/출력 매개 변수를 가질 수 있으며 정수 반환 코드를 반환할 수도 있습니다. 애플리케이션에서는 카탈로그 함수를 사용하여 사용 가능한 저장 프로시저를 열거할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 대상으로 하는 ODBC 애플리케이션은 직접 실행 방식으로만 저장 프로시저를 호출해야 합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 임시 저장 프로시저를 만들어 [Sqlprepare 함수](https://go.microsoft.com/fwlink/?LinkId=59360) 를 구현 합니다 .이 프로시저는 **sqlprepare**에서 호출 됩니다. 대상 저장 프로시저만 호출 하 고 대상 저장 프로시저를 직접 실행 하는 임시 저장 프로시저를 만들도록 **Sqlprepare** 를 추가 하는 오버 헤드를 추가 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 인스턴스에 연결된 경우에도 호출을 준비하려면 추가 네트워크 왕복이 필요하고 저장 프로시저 실행 계획만 호출하는 실행 계획을 작성해야 합니다.  
  
 ODBC 애플리케이션에서는 저장 프로시저를 실행할 때 ODBC CALL 구문을 사용해야 합니다. ODBC CALL 구문을 사용하면 드라이버는 원격 프로시저 호출 메커니즘을 사용하여 프로시저를 호출하도록 최적화됩니다. 이 방법은 서버에 [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE 문을 보내는 데 사용되는 메커니즘에 비해 훨씬 효과적입니다.  
  
 자세한 내용은 [저장 프로시저 실행](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)을 참조 하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [문 &#40;실행 ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
