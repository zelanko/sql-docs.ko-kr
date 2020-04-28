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
ms.openlocfilehash: 8f4efddad1b55ce57c62ce52418539ec06599bb8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925919"
---
# <a name="boundaries-of-a-recordset"></a>레코드 집합의 경계
**레코드** 집합은 데이터 집합의 시작과 끝을 각각 나타내며 **BOF** 및 **EOF** 속성을 지원 합니다. **BOF** 및 **EOF** 는 **레코드 집합**의 시작과 끝에 배치 되는 "가상" 레코드로 간주할 수 있습니다. **BOF** 및 **EOF**를 계산 하면 샘플 **레코드 집합** 은 다음과 같이 표시 됩니다.  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|BOF|||  
|7|열혈 삼촌 Bob의 유기적 Dried 배|30.0000|  
|14|Tofu|23.2500|  
|28|Rssle Sauerkraut|45.6000|  
|51|Manjimup Dried 사과|53.0000|  
|74|Tofu 라이프|10.0000|  
|EOF|||  
  
 커서가 마지막 레코드를 지 나 이동 하면 **EOF** 가 **True**로 설정 됩니다. 그렇지 않으면 해당 값은 **False**입니다. 마찬가지로 커서가 첫 번째 레코드 앞으로 이동 하는 경우에는 **BOF** 가 **True**로 설정 됩니다. 그렇지 않으면 해당 값은 **False**입니다. 다음 JScript 코드 조각에 나와 있는 것 처럼 이러한 속성은 일반적으로 데이터 집합의 레코드를 열거 하는 데 사용 됩니다.  
  
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
  
 **BOF** 와 **EOF** 가 모두 **True**인 경우에는 **레코드 집합** 개체가 비어 있습니다. 새로 열린 비어 있지 않은 **레코드 집합** 개체의 경우 두 속성 모두 **False** 가 됩니다. 다음 JScript 코드 조각에 나와 있는 것 처럼 **BOF** 및 **EOF** 속성을 함께 사용 하 여 **레코드 집합** 개체가 비어 있는지 여부를 확인할 수 있습니다.  
  
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
  
 이 체계는 모든 커서 형식에 대해 작동 하며 기본 공급자와는 독립적입니다. **RecordCount** 속성 값이 0 인지 여부를 확인 하 여 **레코드 집합** 개체의 비어 있는지 확인할 확인 하려고 시도 하는 경우 결과의 레코드 수를 반환 하는 데 필요한 적절 한 커서 및 공급자를 사용 하도록 예방 조치를 취해야 합니다.  
  
 **레코드 집합** 개체에서 마지막으로 남아 있는 레코드를 삭제 하면 커서는 결정 되지 않은 상태로 유지 됩니다. 공급자에 따라 현재 레코드의 위치를 변경할 때까지 **BOF** 및 **EOF** 속성을 **False로** 유지할 수 있습니다. 자세한 내용은 [Delete 메서드를 사용 하 여 레코드 삭제](../../../ado/guide/data/deleting-records-using-the-delete-method.md)를 참조 하세요.
