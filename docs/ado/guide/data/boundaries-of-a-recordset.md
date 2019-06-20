---
title: 레코드 집합의 경계 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- EOF property [ADO], boundaries of a Recordset
- Recordset object [ADO], boundaries of a Recordset
- BOF property [ADO], boundaries of a Recordset
ms.assetid: c0dd4a0f-478d-4c5e-b5d5-7535f211d064
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 967ccb49cd2bbaa805420e7c982cc11721931022
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702343"
---
# <a name="boundaries-of-a-recordset"></a>레코드 집합의 경계
**레코드 집합** 지원 합니다 **BOF** 하 고 **EOF** 를 데이터 집합의 시작과 끝을 각각 설명 하는 속성입니다. 생각할 수 있습니다 **BOF** 하 고 **EOF** 시작과 끝에 배치 되는 "가상" 레코드로 합니다 **레코드 집합**합니다. 계산 **BOF** 하 고 **EOF**, 샘플 **레코드 집합** 은 이제 다음과 같습니다.  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|BOF|||  
|7|대양 유기적 건과 (배)|30.0000|  
|14|두 부|23.2500|  
|28|Rssle 사워크라우트|45.6000|  
|51|나 주 배|53.0000|  
|74|유미 두 부|10.0000|  
|EOF|||  
  
 마지막 레코드를 지 나 커서를 움직이면 **EOF** 로 설정 되어 **True**이 고, 그렇지 않으면 해당 값이 **False**합니다. 마찬가지로, 커서를 이동할 때 첫 번째 레코드 앞 **BOF** 로 설정 된 **True**이 고, 그렇지 않으면 해당 값이 **False**합니다. 다음 JScript 코드 조각에서 볼 수 있듯이 이러한 속성, 데이터 집합에서 레코드를 열거 하려면 자주 사용 됩니다.  
  
```  
while (objRecordset.EOF != true)   
{  
   // Work on the current record.  
   ...  
   // Advance the cursor forward to the next record.  
   objRecordset.MoveNext();  
}  
or  
while (objRecordset.BOF != true)   
{  
   // Work on the current record.  
   ...  
   // Move the cursor to the previous record.  
   objRecordset.MovePrevious();  
}  
```  
  
 둘 다 **BOF** 및 **EOF** 됩니다 **True**, **레코드 집합** 개체가 비어 있습니다. 속성이 모두 **False** 에 새로 열린된 비어 있지 않은 **Recordset** 개체입니다. 사용할 수 있습니다를 **BOF** 및 **EOF** 함께 확인 하는 속성을 **레코드 집합** 개체가 비어 있거나 없습니다, 다음 JScript 코드 조각에 표시 된 것 처럼.  
  
```  
if (objRecordset.EOF == true && objRecordset.BOF == true)  
{  
   WScript.Echo("we got an empty dataset.");  
}  
else  
{  
   WScript.Echo("we got a full dataset.");  
}  
```  
  
 이 체계 커서의 모든 형식에 대 한 작동 및 기본 공급자와 무관 합니다. 작다는 것을 확인 하려는 경우는 **레코드 집합** 확인 하 여 개체 해당 **RecordCount** 속성 값 영 (0) 인지, 적절 한 커서 및 공급자를 사용 하 여 예방 조치를 수행 해야 하는 결과의 레코드 수의 반환을 지원 합니다.  
  
 마지막 남은 레코드를 삭제 하는 경우는 **레코드 집합** 개체 커서가 확정 상태로 남습니다. **BOF** 하 고 **EOF** 속성 유지 **False** 현재 레코드의 위치를 변경 하려고 할 때 까지는 공급자에 따라 합니다. 자세한 내용은 [Delete 메서드를 사용 하 여 삭제 레코드](../../../ado/guide/data/deleting-records-using-the-delete-method.md)합니다.
