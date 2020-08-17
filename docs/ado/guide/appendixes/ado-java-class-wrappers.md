---
description: ADO Java 클래스 래퍼
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c02865fc20d741fc8b3f80ccecd56fcb105ad45e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88355219"
---
# <a name="ado-java-class-wrappers"></a>ADO Java 클래스 래퍼
이 코드는 ADO [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 클래스의 인스턴스를 선언 하 고 동일한 코드 줄에서이를 초기화 합니다. 또한 [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드의 각 인수에 대 한 변수를 선언 합니다. 특히 [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) 및 [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) 의 경우에는 Java가 열거 형식을 지원 하지 않기 때문입니다. 이 메서드는 **레코드 집합** 개체를 열고 닫습니다. Rs1를 NULL로 설정 하면 Java가 사용 하지 않는 개체의 체계적이 고 일시적인 릴리스를 수행할 때 해당 변수가 해제 되도록 예약 하기만 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [Java용 Microsoft SDK 사용](../../../ado/guide/appendixes/using-the-microsoft-sdk-for-java.md)
