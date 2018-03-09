---
title: "Append 메서드 (ADOX 프로시저) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
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
- Procedures::Append
- Procedures::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 38e3492c-c1e1-42e3-a71a-befdc90204db
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cdf43784501659e3fd4da883ddeac33439a30719
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="append-method-adox-procedures"></a>Append 메서드 (ADOX 프로시저)
새로 추가 [프로시저](../../../ado/reference/adox-api/procedure-object-adox.md) 개체는 [프로시저](../../../ado/reference/adox-api/procedures-collection-adox.md) 컬렉션입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>매개 변수  
 *이름*  
 A **문자열** 을 만든 추가 프로시저의 이름을 지정 하는 값입니다.  
  
 *Command*  
 ADO [명령](../../../ado/reference/ado-api/command-object-ado.md) 를 만들고 추가 하는 절차를 나타내는 개체입니다.  
  
## <a name="remarks"></a>주의  
 이름 및 특성에 지정 된 데이터 소스에 새 프로시저를 만듭니다는 **명령** 개체입니다.  
  
 사용자 지정 하는 명령 텍스트는 프로시저를 사용 하지 않고 뷰를 나타내는 경우 동작은 사용 중인 공급자에 따라 달라 집니다. **추가** 공급자 명령 유지를 지원 하지 않는 경우 실패 합니다.  
  
> [!NOTE]
>  Microsoft Jet 용 OLE DB Provider를 사용 하는 경우는 **프로시저** 컬렉션 **Append** 메서드를 사용 하면 지정할 수는 **보기** 아닌  **프로시저** 에 *명령* 매개 변수입니다. **보기** 데이터 소스에 추가 되 고에 추가 되는 **프로시저** 컬렉션입니다. 후의 **Append**경우는 **프로시저** 및 **뷰** 컬렉션을 새로 고칠는 **보기** 는 에더이상됩니다**프로시저** 컬렉션에 표시 됩니다는 **뷰** 컬렉션입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Procedures 컬렉션(ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
  
## <a name="see-also"></a>관련 항목:  
 [메서드 예제 (VB)를 추가 하는 절차](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Append 메서드 (ADOX 열)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 메서드 (ADOX 그룹)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 메서드 (ADOX 인덱스)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 메서드 (ADOX 키)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 메서드 (ADOX 테이블)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 메서드 (ADOX 사용자)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 메서드(ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
