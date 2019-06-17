---
title: ADO.NET의 사용자 정의 형식 액세스 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 893b2c69a20974bb379cc032f442e5fcb3525ec5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62919680"
---
# <a name="accessing-user-defined-types-in-adonet"></a>ADO.NET의 사용자 정의 형식 액세스
  사용자 정의 형식 (Udt)에서 지 원하는 언어 중 하나를 사용 하 여 작성 되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework CLR (공용 언어 런타임) 검증할 수 있는 코드를 생성 하는 합니다. 이러한 언어에는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 등이 있습니다. UDT를 사용하면 개체와 사용자 지정 데이터 구조를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장할 수 있습니다. 데이터는 .NET Framework 클래스 또는 구조의 공용 멤버로 노출되며 동작은 클래스 또는 구조의 메서드로 정의됩니다. UDT를 테이블의 열 정의, [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리의 변수 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수나 저장 프로시저의 인수로 사용할 수 있습니다.  
  
 ADO.NET에서 `System.Data.SqlClient` 공급자는 UDT를 다음과 같은 방식으로 노출합니다.  
  
-   `System.Data.SqlClient.SqlDataReader`를 통해 개체로 노출  
  
-   `SqlDataReader`를 통해 원시 바이트로 노출  
  
-   `System.Data.SqlClient.SqlParameter` 개체의 매개 변수로 노출  
  
## <a name="in-this-section"></a>섹션 내용  
 [UDT 데이터 검색](accessing-user-defined-types-retrieving-udt-data.md)  
 UDT 데이터를 검색하는 방법과 매개 변수를 지정하는 방법에 대해 설명합니다.  
  
 [DataAdapter로 UDT 열 업데이트](accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 `DataSets`에서 UDT로 작업하는 방법과 `DataAdapters`를 사용하여 UDT를 업데이트하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
 [CLR 사용자 정의 형식](clr-user-defined-types.md)  
  
  
