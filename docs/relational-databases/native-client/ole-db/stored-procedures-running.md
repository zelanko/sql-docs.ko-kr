---
description: 저장 프로시저-SQL Server Native Client에서 실행
title: 저장 프로시저 실행(OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [OLE DB], executing
- OLE DB, stored procedures
- SQL Server Native Client OLE DB provider, stored procedures
ms.assetid: c77d9be9-2176-4438-8c7a-04b63ebece08
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 21cca9e6dd3ce8f3ee177997d94b1cfadb15ed1c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467534"
---
# <a name="stored-procedures---running-in-sql-server-native-client"></a>저장 프로시저-SQL Server Native Client에서 실행
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  문을 실행할 때 클라이언트 애플리케이션에서 직접 문을 실행하거나 준비하는 대신 데이터 원본의 저장 프로시저를 호출하면 다음과 같은 장점이 있습니다.  
  
-   성능 향상  
  
-   네트워크 오버헤드 감소  
  
-   일관성 향상  
  
-   정확성 향상  
  
-   기능 추가  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 저장 프로시저에서 데이터를 반환 하는 데 사용 하는 세 가지 메커니즘을 지원 합니다.  
  
-   프로시저의 모든 SELECT 문은 결과 집합을 생성합니다.  
  
-   프로시저는 출력 매개 변수를 통해 데이터를 반환할 수 있습니다.  
  
-   프로시저에는 정수 반환 코드가 있을 수 있습니다.  
  
 애플리케이션은 저장 프로시저의 이러한 모든 출력을 처리할 수 있어야 합니다.  
  
 OLE DB 공급자는 결과를 처리하는 동안 각각 다른 시기에 출력 매개 변수와 반환 값을 반환합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자의 경우 소비자가 저장 프로시저에서 반환 된 결과 집합을 검색 하거나 취소할 때까지 출력 매개 변수 및 반환 코드가 제공 되지 않습니다. 반환 코드와 출력 매개 변수는 서버에서 보내는 마지막 TDS 패킷에서 반환됩니다.  
  
 공급자는 출력 매개 변수와 반환 값을 반환할 때 DBPROP_OUTPUTPARAMETERAVAILABILITY 속성을 사용하여 보고합니다. 이 속성은 DBPROPSET_DATASOURCEINFO 속성 집합에 들어 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 DBPROP_OUTPUTPARAMETERAVAILABILITY 속성을 DBPROPVAL_OA_ATROWRELEASE로 설정 하 여 반환 코드와 출력 매개 변수가 반환 되지 않고 결과 집합이 처리 되거나 해제 될 때까지 반환 되도록 지정 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [저장 프로시저](../../../relational-databases/native-client/ole-db/stored-procedures.md)  
  
  
