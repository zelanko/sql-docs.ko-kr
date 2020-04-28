---
title: Append 메서드 (ADOX 프로시저) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedures::Append
- Procedures::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 38e3492c-c1e1-42e3-a71a-befdc90204db
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dd64ba8119db1ecf2d2b621cd202c9f700b53475
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67967287"
---
# <a name="append-method-adox-procedures"></a>Append 메서드(ADOX 프로시저)
[프로시저](../../../ado/reference/adox-api/procedures-collection-adox.md) 컬렉션에 새 [프로시저](../../../ado/reference/adox-api/procedure-object-adox.md) 개체를 추가 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>매개 변수  
 *이름*  
 만들고 추가 하는 프로시저의 이름을 지정 하는 **문자열** 값입니다.  
  
 *명령*  
 만들고 추가 하는 프로시저를 나타내는 ADO [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다.  
  
## <a name="remarks"></a>설명  
 **명령** 개체에 지정 된 이름과 특성을 사용 하 여 데이터 소스에 새 프로시저를 만듭니다.  
  
 사용자가 지정 하는 명령 텍스트가 프로시저가 아닌 뷰를 나타내는 경우이 동작은 사용 중인 공급자에 따라 달라 집니다. 공급자가 명령 유지를 지원 하지 않으면 **추가** 작업이 실패 합니다.  
  
> [!NOTE]
>  Microsoft Jet 용 OLE DB 공급자를 사용 하는 경우 Procedure collection **Append** 메서드를 사용 **하 여** *명령* 매개 변수의 **프로시저가** 아닌 **뷰** 를 지정할 수 있습니다. **뷰가** 데이터 원본에 추가 되 고 **프로시저** 컬렉션에 추가 됩니다. **추가**후에 **프로시저** 및 **뷰** 컬렉션을 새로 고치면 **뷰가** **프로시저** 컬렉션에 더 이상 표시 되지 않고 **Views** 컬렉션에 표시 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Procedures 컬렉션(ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
  
## <a name="see-also"></a>참고 항목  
 [프로시저 Append 메서드 예제 (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Append 메서드 (ADOX Columns)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 메서드 (ADOX Groups)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 메서드 (ADOX 인덱스)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 메서드 (ADOX 키)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 메서드 (ADOX Tables)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 메서드 (ADOX 사용자)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 메서드(ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
