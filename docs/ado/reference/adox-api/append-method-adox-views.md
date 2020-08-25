---
description: Append 메서드(ADOX 보기)
title: Append 메서드 (ADOX Views) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Views::raw_Append
- Views::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6070fd58-3237-4c77-a966-5b39ce5d57e4
author: rothja
ms.author: jroth
ms.openlocfilehash: 74432aa3bb610b1cd5688e1f52c7d7ea81166f75
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771362"
---
# <a name="append-method-adox-views"></a>Append 메서드(ADOX 보기)
새 [뷰](./view-object-adox.md) 개체를 만들어 [Views](./views-collection-adox.md) 컬렉션에 추가 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Views.Append Name, Command  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Name*  
 만들 뷰의 이름을 지정 하는 **문자열** 값입니다.  
  
 *명령*  
 만들 뷰를 나타내는 ADO [명령](../ado-api/command-object-ado.md) 개체입니다.  
  
## <a name="remarks"></a>설명  
 **명령** 개체에 지정 된 이름과 특성을 사용 하 여 데이터 소스에 새 뷰를 만듭니다.  
  
 사용자가 지정 하는 명령 텍스트가 뷰가 아닌 프로시저를 나타내는 경우 동작은 공급자에 따라 달라 집니다. 공급자가 명령 유지를 지원 하지 않으면 **추가** 작업이 실패 합니다.  
  
> [!NOTE]
>  Microsoft Jet 용 OLE DB 공급자를 사용 하는 경우 **Views** collection **Append** 메서드를 사용 하 여 *명령* 매개 변수의 **뷰가** 아닌 **프로시저** 를 지정할 수 있습니다. **프로시저가** 데이터 원본에 추가 되 고 **Views** 컬렉션에 추가 됩니다. **추가**후 **프로시저 및** **뷰** 컬렉션이 새로 고쳐질 경우 **프로시저** 는 더 이상 **Views** 컬렉션에 없으며 **프로시저** 컬렉션에 표시 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Views 컬렉션(ADOX)](./views-collection-adox.md)  
  
## <a name="see-also"></a>참고 항목  
 [Views Append 메서드 예제 (VB)](./views-append-method-example-vb.md)   
 [Append 메서드 (ADOX Columns)](./append-method-adox-columns.md)   
 [Append 메서드 (ADOX Groups)](./append-method-adox-groups.md)   
 [Append 메서드 (ADOX 인덱스)](./append-method-adox-indexes.md)   
 [Append 메서드 (ADOX 키)](./append-method-adox-keys.md)   
 [Append 메서드 (ADOX 프로시저)](./append-method-adox-procedures.md)   
 [Append 메서드 (ADOX Tables)](./append-method-adox-tables.md)   
 [Append 메서드(ADOX 사용자)](./append-method-adox-users.md)