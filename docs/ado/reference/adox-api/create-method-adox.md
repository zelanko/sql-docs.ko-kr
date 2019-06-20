---
title: Create 메서드 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::raw_Create
- _Catalog::Create
helpviewer_keywords:
- Create method [ADOX]
ms.assetid: 64f5c21c-b581-42d8-bdc7-c4f1bebaf105
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: bbdd7f6b663fb1c6c2ee12b7a6e4c843eb16d42d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66703359"
---
# <a name="create-method-adox"></a>Create 메서드(ADOX)
새 카탈로그를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Catalog.Create ConnectString  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ConnectString*  
 A **문자열** 데이터 원본에 연결 하는 데 사용 되는 값입니다.  
  
## <a name="remarks"></a>Remarks  
 **Create** 메서드를 만들고 새 ADO 열립니다 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 에 지정 된 데이터 원본에 *ConnectString*합니다. 성공 하면 새 **연결** 개체에 할당 된 [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) 속성입니다.  
  
 공급자는 새 카탈로그 만들기를 지원 하지 않는 경우 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Catalog 개체(ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>관련 항목  
 [Create 메서드 예제 (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [ActiveConnection 속성(ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)
