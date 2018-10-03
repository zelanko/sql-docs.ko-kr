---
title: ADO.NET으로 SQL Server In-process 전용 확장 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- data access [CLR integration]
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- database objects [CLR integration], in-process extensions
- in-process data access providers [CLR integration]
- extensions [CLR integration]
ms.assetid: 781b812e-eb14-472a-85fa-aa4cdb929bee
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9c5e98bebb99192c7245db3e2c255a36af751c0c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47683162"
---
# <a name="sql-server-in-process-specific-extensions-to-adonet"></a>ADO.NET에 대한 SQL Server In-Process 전용 확장
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  ADO.NET과 관련하여 In-Process에 사용하기 위해 특별히 고안된 네 가지 주요 기능 확장이 있습니다. 다음 항목에서는 이러한 확장에 대해 자세히 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [SqlContext 개체](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
 이 클래스는 관리 코드를 In-Process로 실행하는 SQL Server 루틴 호출자의 컨텍스트를 추상화하여 다른 확장에 대한 액세스를 제공합니다.  
  
 [SqlPipe 개체](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)  
 이 클래스에는 테이블 형식 결과 및 메시지를 클라이언트로 보내는 루틴이 포함되어 있습니다.  
  
 [SqlTriggerContext 개체](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)  
 이 클래스는 트리거가 실행되는 컨텍스트에 대한 정보를 제공합니다.  
  
 [SqlDataRecord 개체](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqldatarecord-object.md)  
 SqlDataRecord 클래스는 단일 데이터 행과 이와 관련된 메타데이터를 나타내며, 저장 프로시저는 이를 사용하여 사용자 지정 결과 집합을 클라이언트에 반환할 수 있습니다.  
  
  
