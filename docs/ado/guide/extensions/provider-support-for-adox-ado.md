---
title: "ADOX (ADO)에 대 한 공급자 지원 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADOX provider support [ADO]
ms.assetid: 64234ce5-dc46-4c8a-a316-61956b6b9abb
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b15df02c70e2dcdc2efb2ba468b76219a233d65a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="provider-support-for-adox-ado"></a>ADOX (ADO)에 대 한 공급자 지원
ADOX의 특정 기능은 OLE DB 데이터 공급자에 따라 지원 되지 않습니다. ADOX는 완전히 지원 되는 [OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)합니다. 지원 되지 않는 기능으로는 [Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), [Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md), 또는 [Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) 됩니다 다음 표에 나와 있습니다. ADOX 다른 Microsoft OLE DB 공급자가 지원 되지 않습니다.  
  
## <a name="microsoft-ole-db-provider-for-sql-server"></a>Microsoft OLE DB Provider for SQL Server  
  
|개체 또는 컬렉션|제한 사항|  
|--------------------------|-----------------------|  
|**테이블** 컬렉션|속성은 기존 개체를 참조할 때 개체가 만들어지기 전에 읽기/쓰기가 가능 하지만 읽기 전용입니다.|  
|**뷰** 컬렉션|**뷰** 지원 되지 않습니다.|  
|**프로시저** 컬렉션|**Append** 및 **삭제** 메서드가 지원 되지 않습니다.|  
|**프로시저** 개체|**명령** 속성이 지원 되지 않습니다.|  
|**키** 컬렉션|**Append** 및 **삭제** 메서드가 지원 되지 않습니다.|  
|**사용자가** 컬렉션|**사용자가** 지원 되지 않습니다.|  
|**그룹** 컬렉션|**그룹** 지원 되지 않습니다.|  
  
## <a name="microsoft-ole-db-provider-for-odbc"></a>ODBC용 Microsoft OLE DB 공급자  
  
|개체 또는 컬렉션|제한 사항|  
|--------------------------|-----------------------|  
|**카탈로그** 개체|**만들기** 메서드가 지원 되지 않습니다.|  
|**테이블** 컬렉션|**Append** 및 **삭제** 메서드가 지원 되지 않습니다. 속성은 기존 개체를 참조할 때 개체가 만들어지기 전에 읽기/쓰기가 가능 하지만 읽기 전용입니다.|  
|**프로시저** 컬렉션|**Append** 및 **삭제** 메서드가 지원 되지 않습니다.|  
|**프로시저** 개체|**명령** 속성이 지원 되지 않습니다.|  
|**인덱스** 컬렉션|**Append** 및 **삭제** 메서드가 지원 되지 않습니다.|  
|**키** 컬렉션|**Append** 및 **삭제** 메서드가 지원 되지 않습니다.|  
|**사용자가** 컬렉션|**사용자가** 지원 되지 않습니다.|  
|**그룹** 컬렉션|**그룹** 지원 되지 않습니다.|  
  
## <a name="microsoft-ole-db-provider-for-oracle"></a>Oracle용 Microsoft OLE DB 공급자  
  
|개체 또는 컬렉션|제한 사항|  
|--------------------------|-----------------------|  
|**카탈로그** 개체|**만들기** 메서드가 지원 되지 않습니다.|  
|**테이블** 컬렉션|**Append** 및 **삭제** 메서드가 지원 되지 않습니다. 속성은 기존 개체를 참조할 때 개체가 만들어지기 전에 읽기/쓰기가 가능 하지만 읽기 전용입니다.|  
|**뷰** 컬렉션|**Append** 및 **삭제** 메서드가 지원 되지 않습니다.|  
|**보기** 개체|**명령** 속성이 지원 되지 않습니다.|  
|**프로시저** 개체|**Append** 및 **삭제** 메서드가 지원 되지 않습니다.|  
|**프로시저** 개체|**명령** 속성이 지원 되지 않습니다.|  
|**인덱스** 컬렉션|**Append** 및 **삭제** 메서드가 지원 되지 않습니다.|  
|**키** 컬렉션|**Append** 및 **삭제** 메서드가 지원 되지 않습니다.|  
|**사용자가** 컬렉션|**사용자가** 지원 되지 않습니다.|  
|**그룹** 컬렉션|**그룹** 지원 되지 않습니다.|
