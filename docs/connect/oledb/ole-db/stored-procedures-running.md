---
title: 저장된 프로시저 (OLE DB)를 실행 | Microsoft Docs
description: 저장 프로시저 실행(OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [OLE DB], executing
- OLE DB, stored procedures
- OLE DB Driver for SQL Server, stored procedures
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 68f2298552a0dc6f313b54e357cecc2a6e7a855c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="stored-procedures---running"></a>저장된 프로시저-실행
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  문을 실행할 때 클라이언트 응용 프로그램에서 직접 문을 실행하거나 준비하는 대신 데이터 원본의 저장 프로시저를 호출하면 다음과 같은 장점이 있습니다.  
  
-   성능 향상  
  
-   네트워크 오버헤드 감소  
  
-   일관성 향상  
  
-   정확성 향상  
  
-   기능 추가  
  
 OLE DB Driver for SQL Server 세 가지 메커니즘을 지원 하 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터를 반환 하려면 저장된 프로시저를 사용 합니다.  
  
-   프로시저의 모든 SELECT 문은 결과 집합을 생성합니다.  
  
-   프로시저는 출력 매개 변수를 통해 데이터를 반환할 수 있습니다.  
  
-   프로시저에는 정수 반환 코드가 있을 수 있습니다.  
  
 응용 프로그램은 저장 프로시저의 이러한 모든 출력을 처리할 수 있어야 합니다.  
  
 OLE DB 공급자는 결과를 처리하는 동안 각각 다른 시기에 출력 매개 변수와 반환 값을 반환합니다. OLE DB Driver for SQL Server를 발생 시 출력 매개 변수 및 반환 코드 제공 하지 않는 될 때까지 소비자가 검색 또는 저장된 프로시저에서 반환 된 결과 집합을 취소 한 후 합니다. 반환 코드와 출력 매개 변수는 서버에서 보내는 마지막 TDS 패킷에서 반환됩니다.  
  
 공급자는 출력 매개 변수와 반환 값을 반환할 때 DBPROP_OUTPUTPARAMETERAVAILABILITY 속성을 사용하여 보고합니다. 이 속성은 DBPROPSET_DATASOURCEINFO 속성 집합에 들어 있습니다.  
  
 OLE DB Driver for SQL Server는 반환 코드 및 출력 매개 변수는 반환 되지 않습니다는 결과 집합 처리 또는 해제 될 때까지 나타내려면 DBPROPVAL_OA_ATROWRELEASE를 DBPROP_OUTPUTPARAMETERAVAILABILITY 속성을 설정 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [저장된 프로시저](../../oledb/ole-db/stored-procedures.md)  
  
  
