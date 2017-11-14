---
title: "Append 메서드 (ADOX 보기) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Views::raw_Append
- Views::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6070fd58-3237-4c77-a966-5b39ce5d57e4
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 535f25f475f6357d467e2f7ac19a96ed6eea1605
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="append-method-adox-views"></a>Append 메서드 (ADOX 뷰)
새 [보기](../../../ado/reference/adox-api/view-object-adox.md) 개체 및 필터를 추가 하는 [뷰](../../../ado/reference/adox-api/views-collection-adox.md) 컬렉션입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Views.Append Name, Command  
```  
  
#### <a name="parameters"></a>매개 변수  
 *이름*  
 A **문자열** 만들 뷰 이름을 지정 하는 값입니다.  
  
 *Command*  
 ADO [명령](../../../ado/reference/ado-api/command-object-ado.md) 만들 뷰를 나타내는 개체입니다.  
  
## <a name="remarks"></a>주의  
 이름 및 특성에 지정 된 데이터 소스에서 새 뷰를 만듭니다는 **명령** 개체입니다.  
  
 사용자 지정 하는 명령 텍스트를 뷰가 아닌 프로시저를 나타내는 경우 동작 공급자에 따라 달라 집니다. **추가** 공급자 명령 유지를 지원 하지 않는 경우 실패 합니다.  
  
> [!NOTE]
>  Microsoft Jet 용 OLE DB Provider를 사용 하는 경우는 **뷰** 컬렉션 **Append** 메서드를 사용 하면 지정할 수는 **프로시저** 아닌 **보기**  에 *명령* 매개 변수입니다. **프로시저** 데이터 소스에 추가 되 고에 추가 되는 **뷰** 컬렉션입니다. 후의 **Append**경우는 **프로시저** 및 **뷰** 컬렉션을 새로 고칠는 **프로시저** 는 에더이상됩니다**뷰** 컬렉션에 표시 됩니다는 **프로시저** 컬렉션입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Views 컬렉션(ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)  
  
## <a name="see-also"></a>관련 항목:  
 [뷰 추가 (VB) 메서드 예제](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Append 메서드 (ADOX 열)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 메서드 (ADOX 그룹)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 메서드 (ADOX 인덱스)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 메서드 (ADOX 키)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 메서드 (ADOX 프로시저)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 메서드 (ADOX 테이블)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 메서드(ADOX 사용자)](../../../ado/reference/adox-api/append-method-adox-users.md)

