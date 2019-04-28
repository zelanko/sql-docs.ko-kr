---
title: ADO Java 클래스 래퍼 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- class wrappers [ADO]
ms.assetid: 1fc09dc1-9e32-412e-9f43-b8eb8bb483ca
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ddcbba246f0bdcfb5c3a22766f5d335a2bd5893e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62719971"
---
# <a name="ado-java-class-wrappers"></a>ADO Java 클래스 래퍼
이 코드는 ADO의 인스턴스를 선언 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 클래스 래퍼 동일한 코드 줄에 모두 초기화 합니다. 또한 각 인수에 대 한 변수를 선언 하는 [열기](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드, 특히 [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) 및 [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) (Java를 지원 하지 않으므로 열거 형식)입니다. 열리고 닫히는지 합니다 **레코드 집합** 개체입니다. Java 사용 되지 않는 개체의 체계적이 고 일시적인 출시를 수행 하는 경우 출시 될 해당 변수를 예약 Rs1을 단순히 NULL로 설정 합니다.  
  
```java
public static void main( String args[])  
{  
   msado15._Recordset   Rs1 = new msado15.Recordset();  
   Variant Source     = new Variant( "SELECT * FROM Authors" );  
   Variant Connect    = new Variant( "DSN=AdoDemo;UID=admin;PWD=;" );  
   int     LockType   = msado15.CursorTypeEnum.adOpenForwardOnly;  
   int     CursorType = msado15.LockTypeEnum.adLockReadOnly;  
   int     Options    = -1;  
  
   Rs1.Open( Source, Connect, LockType,  CursorType, Options );  
   Rs1.Close();  
   Rs1 = null;  
  
   System.out.println( "Success!\n" );  
}  
```  
  
## <a name="see-also"></a>관련 항목  
 [Java용 Microsoft SDK 사용](../../../ado/guide/appendixes/using-the-microsoft-sdk-for-java.md)
