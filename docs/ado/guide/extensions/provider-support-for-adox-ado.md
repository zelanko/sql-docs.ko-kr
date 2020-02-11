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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923213"
---
# <a name="provider-support-for-adox-ado"></a>ADOX에 대한 공급자 지원(ADO)
OLE DB 데이터 공급자에 따라 ADOX의 특정 기능을 지원 하지 않습니다. ADOX는 [Microsoft Jet 용 OLE DB 공급자](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)에서 완벽 하 게 지원 됩니다. [Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), [ODBC 용 microsoft OLE DB 공급자](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)또는 [Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) 에서 지원 되지 않는 기능은 다음 표에 나와 있습니다. ADOX는 다른 Microsoft OLE DB 공급자에서 지원 되지 않습니다.  
  
## <a name="microsoft-ole-db-provider-for-sql-server"></a>SQL Server용 Microsoft OLE DB Provider  
  
|개체 또는 컬렉션|사용 제한|  
|--------------------------|-----------------------|  
|**Tables** 컬렉션|속성은 개체를 만들기 전에 읽기/쓰기이 고, 기존 개체를 참조 하는 경우에는 읽기 전용입니다.|  
|**Views** 컬렉션|**뷰** 는 지원 되지 않습니다.|  
|**프로시저** 컬렉션|**Append** 및 **Delete** 메서드는 지원 되지 않습니다.|  
|**프로시저** 개체|**Command** 속성은 지원 되지 않습니다.|  
|**Keys** 컬렉션|**Append** 및 **Delete** 메서드는 지원 되지 않습니다.|  
|**사용자** 컬렉션|**사용자** 가 지원 되지 않습니다.|  
|**Groups** 컬렉션|**그룹이** 지원 되지 않습니다.|  
  
## <a name="microsoft-ole-db-provider-for-odbc"></a>ODBC용 Microsoft OLE DB 공급자  
  
|개체 또는 컬렉션|사용 제한|  
|--------------------------|-----------------------|  
|**Catalog** 개체|**Create** 메서드는 지원 되지 않습니다.|  
|**Tables** 컬렉션|**Append** 및 **Delete** 메서드는 지원 되지 않습니다. 속성은 개체를 만들기 전에 읽기/쓰기이 고, 기존 개체를 참조 하는 경우에는 읽기 전용입니다.|  
|**프로시저** 컬렉션|**Append** 및 **Delete** 메서드는 지원 되지 않습니다.|  
|**프로시저** 개체|**Command** 속성은 지원 되지 않습니다.|  
|**Indexes** 컬렉션|**Append** 및 **Delete** 메서드는 지원 되지 않습니다.|  
|**Keys** 컬렉션|**Append** 및 **Delete** 메서드는 지원 되지 않습니다.|  
|**사용자** 컬렉션|**사용자** 가 지원 되지 않습니다.|  
|**Groups** 컬렉션|**그룹이** 지원 되지 않습니다.|  
  
## <a name="microsoft-ole-db-provider-for-oracle"></a>Oracle용 Microsoft OLE DB Provider  
  
|개체 또는 컬렉션|사용 제한|  
|--------------------------|-----------------------|  
|**Catalog** 개체|**Create** 메서드는 지원 되지 않습니다.|  
|**Tables** 컬렉션|**Append** 및 **Delete** 메서드는 지원 되지 않습니다. 속성은 개체를 만들기 전에 읽기/쓰기이 고, 기존 개체를 참조 하는 경우에는 읽기 전용입니다.|  
|**Views** 컬렉션|**Append** 및 **Delete** 메서드는 지원 되지 않습니다.|  
|개체 **보기**|**Command** 속성은 지원 되지 않습니다.|  
|**프로시저** 개체|**Append** 및 **Delete** 메서드는 지원 되지 않습니다.|  
|**프로시저** 개체|**Command** 속성은 지원 되지 않습니다.|  
|**Indexes** 컬렉션|**Append** 및 **Delete** 메서드는 지원 되지 않습니다.|  
|**Keys** 컬렉션|**Append** 및 **Delete** 메서드는 지원 되지 않습니다.|  
|**사용자** 컬렉션|**사용자** 가 지원 되지 않습니다.|  
|**Groups** 컬렉션|**그룹이** 지원 되지 않습니다.|
