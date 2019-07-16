---
title: ADOX (ADO)에 대 한 공급자 지원 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADOX provider support [ADO]
ms.assetid: 64234ce5-dc46-4c8a-a316-61956b6b9abb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b07f4563d54254310c08c8c132d0729b8ccdc6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923213"
---
# <a name="provider-support-for-adox-ado"></a>ADOX에 대한 공급자 지원(ADO)
ADOX의 특정 기능은 OLE DB 데이터 공급자에 따라 지원 되지 않습니다. ADOX에서 완전히 지원 되는 [OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)합니다. 지원 되지 않는 기능을 [Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)의 [Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md), 또는 [Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) 됩니다 다음 테이블에 나열 합니다. ADOX 다른 Microsoft OLE DB 공급자가 지원 되지 않습니다.  
  
## <a name="microsoft-ole-db-provider-for-sql-server"></a>Microsoft OLE DB Provider for SQL Server  
  
|개체 또는 컬렉션|사용 제한|  
|--------------------------|-----------------------|  
|**테이블** 컬렉션|속성은 기존 개체를 참조할 때 개체를 생성 하기 전에 읽기/쓰기가 가능 하지만 읽기 전용입니다.|  
|**뷰** 컬렉션|**뷰** 지원 되지 않습니다.|  
|**프로시저** 컬렉션|**Append** 하 고 **삭제** 메서드가 지원 되지 않습니다.|  
|**프로시저** 개체|합니다 **명령** 속성이 지원 되지 않습니다.|  
|**키** 컬렉션|**Append** 하 고 **삭제** 메서드가 지원 되지 않습니다.|  
|**사용자가** 컬렉션|**사용자가** 지원 되지 않습니다.|  
|**그룹** 컬렉션|**그룹** 지원 되지 않습니다.|  
  
## <a name="microsoft-ole-db-provider-for-odbc"></a>ODBC용 Microsoft OLE DB 공급자  
  
|개체 또는 컬렉션|사용 제한|  
|--------------------------|-----------------------|  
|**카탈로그** 개체|합니다 **만들기** 메서드가 지원 되지 않습니다.|  
|**테이블** 컬렉션|**Append** 하 고 **삭제** 메서드가 지원 되지 않습니다. 속성은 기존 개체를 참조할 때 개체를 생성 하기 전에 읽기/쓰기가 가능 하지만 읽기 전용입니다.|  
|**프로시저** 컬렉션|**Append** 하 고 **삭제** 메서드가 지원 되지 않습니다.|  
|**프로시저** 개체|합니다 **명령** 속성이 지원 되지 않습니다.|  
|**인덱스** 컬렉션|**Append** 하 고 **삭제** 메서드가 지원 되지 않습니다.|  
|**키** 컬렉션|**Append** 하 고 **삭제** 메서드가 지원 되지 않습니다.|  
|**사용자가** 컬렉션|**사용자가** 지원 되지 않습니다.|  
|**그룹** 컬렉션|**그룹** 지원 되지 않습니다.|  
  
## <a name="microsoft-ole-db-provider-for-oracle"></a>Oracle용 Microsoft OLE DB 공급자  
  
|개체 또는 컬렉션|사용 제한|  
|--------------------------|-----------------------|  
|**카탈로그** 개체|합니다 **만들기** 메서드가 지원 되지 않습니다.|  
|**테이블** 컬렉션|**Append** 하 고 **삭제** 메서드가 지원 되지 않습니다. 속성은 기존 개체를 참조할 때 개체를 생성 하기 전에 읽기/쓰기가 가능 하지만 읽기 전용입니다.|  
|**뷰** 컬렉션|**Append** 하 고 **삭제** 메서드가 지원 되지 않습니다.|  
|**보기** 개체|합니다 **명령** 속성이 지원 되지 않습니다.|  
|**프로시저** 개체|**Append** 하 고 **삭제** 메서드가 지원 되지 않습니다.|  
|**프로시저** 개체|합니다 **명령** 속성이 지원 되지 않습니다.|  
|**인덱스** 컬렉션|**Append** 하 고 **삭제** 메서드가 지원 되지 않습니다.|  
|**키** 컬렉션|**Append** 하 고 **삭제** 메서드가 지원 되지 않습니다.|  
|**사용자가** 컬렉션|**사용자가** 지원 되지 않습니다.|  
|**그룹** 컬렉션|**그룹** 지원 되지 않습니다.|
