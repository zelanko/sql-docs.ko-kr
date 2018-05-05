---
title: 레코드 집합의 경계 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- EOF property [ADO], boundaries of a Recordset
- Recordset object [ADO], boundaries of a Recordset
- BOF property [ADO], boundaries of a Recordset
ms.assetid: c0dd4a0f-478d-4c5e-b5d5-7535f211d064
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20373bc374d1f5f5b75522ede5255a376ab6f657
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="boundaries-of-a-recordset"></a>레코드 집합의 경계
**레코드 집합** 지원는 **BOF** 및 **EOF** 속성을 데이터 집합의 시작과 끝을 각각 설명 합니다. 생각할 수 있으며 **BOF** 및 **EOF** 의 시작과 끝에 배치 됩니다 "팬텀" 레코드로 **레코드 집합**합니다. 계산 **BOF** 및 **EOF**, 샘플 **레코드 집합** 는 이제 다음과 같이 표시 됩니다.  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|BOF|||  
|7|유기적 건과 (배)|30.0000|  
|14|두 부|23.2500|  
|28|Rssle 사워크라우트 맛|45.6000|  
|51|나 주 배|53.0000|  
|74|유미 두 부|10.0000|  
|EOF|||  
  
 커서를 마지막 레코드를 지 나 이동 하면 **EOF** 로 설정 된 **True**, 그렇지 않으면 해당 값은 **False**합니다. 마찬가지로, 커서를 이동할 때 첫 번째 레코드 바로 앞 **BOF** 로 설정 된 **True**, 그렇지 않으면 해당 값은 **False**합니다. 이러한 속성 다음 JScript 코드 조각에 표시 된 것 처럼에 일반적으로 데이터 집합의 레코드를 열거 하는 데 사용 됩니다.  
  
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
  
 두 **BOF** 및 **EOF** 는 **True**, **레코드 집합** 개체가 비어 있습니다. 두 속성 모두 됩니다 **False** 새로 열린된 반드시에 대 한 **레코드 집합** 개체입니다. 사용할 수는 **BOF** 및 **EOF** 속성 결정 하는 경우는 **레코드 집합** 개체는 비어 있거나 다음 JScript 코드 조각에 표시 된 대로, 합니다.  
  
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
  
 이 체계 커서의 모든 형식에 사용할 수 있으며 기본 공급자와 무관 합니다. 비어 있는지를 확인 하려는 경우는 **레코드 집합** 확인 하 여 개체의 **RecordCount** 속성 값은 영 (0) 여부, 적절 한 커서 및 공급자를 사용 하는 조치를 수행 해야 하는 결과에서 레코드의 수를 반환 하도록 지원 합니다.  
  
 마지막 남은 레코드를 삭제 하는 경우는 **레코드 집합** 개체 커서는 결정 되지 않은 상태로 남아 있습니다. **BOF** 및 **EOF** 속성 유지 **False** 공급자에 따라 현재 레코드의 위치를 변경 하기 전 까지는 합니다. 자세한 내용은 참조 [Delete 메서드를 사용 하 여 삭제 레코드](../../../ado/guide/data/deleting-records-using-the-delete-method.md)합니다.
