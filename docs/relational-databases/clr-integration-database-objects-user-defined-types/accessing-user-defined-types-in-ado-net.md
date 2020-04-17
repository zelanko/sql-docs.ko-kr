---
title: ADO.NET 사용자 정의 형식 액세스 | 마이크로 소프트 문서
description: .NET Framework CLR 언어로 작성된 UDT를 사용하면 SQL Server 데이터베이스에서 개체 및 사용자 지정 데이터 구조를 저장할 수 있습니다. ADO.NET 공급자가 UDT를 노출합니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
author: rothja
ms.author: jroth
ms.openlocfilehash: d14205a6fb506f5d4fddaac1ab601ff1ee9205b8
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488261"
---
# <a name="accessing-user-defined-types-in-adonet"></a>ADO.NET의 사용자 정의 형식 액세스
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  사용자 정의 형식(UDT)은 확인 가능한 코드를 생성하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 공통 언어 런타임(CLR)에서 지원하는 언어를 사용하여 작성됩니다. 이러한 언어에는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 등이 있습니다. UDT를 사용하면 개체와 사용자 지정 데이터 구조를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장할 수 있습니다. 데이터는 .NET Framework 클래스 또는 구조의 공용 멤버로 노출되며 동작은 클래스 또는 구조의 메서드로 정의됩니다. UDT를 테이블의 열 정의, [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리의 변수 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수나 저장 프로시저의 인수로 사용할 수 있습니다.  
  
 ADO.NET **System.Data.SqlClient** 공급자는 다음과 같은 방법으로 UDT를 노출합니다.  
  
-   **System.Data.SqlClient.SqlDataReader를** 개체로 합니다.  
  
-   **SqlDataReader를** 통해 원시 바이트로.  
  
-   **System.Data.SqlClient.SqlParameter** 개체의 매개 변수입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [UDT 데이터 검색](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-retrieving-udt-data.md)  
 UDT 데이터를 검색하는 방법과 매개 변수를 지정하는 방법에 대해 설명합니다.  
  
 [DataAdapter로 UDT 열 업데이트](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 **DataSets에서** UDT를 사용하는 방법과 **DataAdapters를**사용하여 UDT 데이터를 업데이트하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
