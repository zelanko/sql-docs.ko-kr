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
author: rothja
ms.author: jroth
ms.openlocfilehash: 15ea5cf8b565a943f4905a890cb08ba0afed202f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759269"
---
# <a name="create-method-adox"></a>Create 메서드(ADOX)
새 카탈로그를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Catalog.Create ConnectString  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ConnectString*  
 데이터 원본에 연결 하는 데 사용 되는 **문자열** 값입니다.  
  
## <a name="remarks"></a>설명  
 **Create** 메서드는 *connectstring*에 지정 된 데이터 원본에 대 한 새 ADO [연결](../../../ado/reference/ado-api/connection-object-ado.md) 을 만들고 엽니다. 성공 하면 새 **연결** 개체가 [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) 속성에 할당 됩니다.  
  
 공급자가 새 카탈로그 만들기를 지원 하지 않는 경우 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Catalog 개체(ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>참고 항목  
 [Create 메서드 예제 (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [ActiveConnection 속성(ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)
