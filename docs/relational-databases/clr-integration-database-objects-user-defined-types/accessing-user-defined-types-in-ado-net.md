---
title: "ADO.NET에서 사용자 정의 형식 액세스 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 267f7513c3cc7342106b04232c137ffdd1621cf9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="accessing-user-defined-types-in-adonet"></a>ADO.NET의 사용자 정의 형식 액세스
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]사용자 정의 형식 (Udt)에서 지 원하는 언어 중 하나를 사용 하 여 기록 되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 공용 언어 런타임 (CLR) 확인할 수 있는 코드를 생성 하는 합니다. 이러한 언어에는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 등이 있습니다. UDT를 사용하면 개체와 사용자 지정 데이터 구조를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장할 수 있습니다. 데이터는 .NET Framework 클래스 또는 구조의 공용 멤버로 노출되며 동작은 클래스 또는 구조의 메서드로 정의됩니다. UDT의 변수는 테이블의 열 정의로 사용할 수 있습니다는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리 또는의 인수로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수 또는 저장된 프로시저입니다.  
  
 Ado.net에서 **System.Data.SqlClient** 공급자는 다음과 같은 방법으로 Udt를 노출 합니다.  
  
-   통해는 **System.Data.SqlClient.SqlDataReader** 개체입니다.  
  
-   통해는 **SqlDataReader** 원시 바이트로 합니다.  
  
-   매개 변수로 **System.Data.SqlClient.SqlParameter** 개체입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [UDT 데이터 검색](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-retrieving-udt-data.md)  
 UDT 데이터를 검색하는 방법과 매개 변수를 지정하는 방법에 대해 설명합니다.  
  
 [Dataadapter로 UDT 열 업데이트](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 Udt로 작업 하는 방법을 설명 **데이터 집합** 사용 하 여 UDT 데이터를 업데이트 하는 방법 및 **Dataadapter**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
