---
title: "Create 메서드 (ADOX) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Catalog::raw_Create
- _Catalog::Create
helpviewer_keywords:
- Create method [ADOX]
ms.assetid: 64f5c21c-b581-42d8-bdc7-c4f1bebaf105
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0bfad8159575c9439846ed2cf407e1b6e407418c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="create-method-adox"></a>Create 메서드 (ADOX)
새 카탈로그를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Catalog.Create ConnectString  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ConnectString*  
 A **문자열** 데이터 원본에 연결 하는 데 사용 되는 값입니다.  
  
## <a name="remarks"></a>주의  
 **만들기** 메서드가 생성 되 고 새 ADO 열립니다 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 에 지정 된 데이터 원본에 *ConnectString*합니다. 성공 하면 새 **연결** 개체에 할당 된 [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) 속성입니다.  
  
 공급자는 새 카탈로그 만들기를 지원 하지 않는 경우 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Catalog 개체(ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Create 메서드 예 (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [ActiveConnection 속성(ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)

